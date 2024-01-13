+++
title = "Add non-root user"
date = 2024-01-13T13:53:43+08:00
weight = 70
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user)

# Add a non-root user to a container 向容器添加非 root 用户



Many Docker images use root as the default user, but there are cases where you may prefer to use a non-root user instead. If you do so, there are some **quirks with local filesystem (bind) mounts** that you should know about. Specifically:

​​	许多 Docker 镜像使用 root 作为默认用户，但在某些情况下，您可能更喜欢使用非 root 用户。如果您这样做，则应该了解本地文件系统（绑定）挂载的一些怪癖。具体来说：

- **Docker Desktop for Mac**: Inside the container, any mounted files/folders will act as if they are owned by the container user you specify. Locally, all filesystem operations will use the permissions of your local user instead.

  ​​	Docker Desktop for Mac：在容器内，任何挂载的文件/文件夹都将表现得好像它们归您指定的容器用户所有。在本地，所有文件系统操作都将使用您本地用户的权限。

- **Docker Desktop for Windows**: Inside the container, any mounted files/folders will appear as if they are owned by `root` but the user you specify will still be able to read/write them and all files will be executable. Locally, all filesystem operations will use the permissions of your local user instead. This is because there is fundamentally no way to directly map Windows-style file permissions to Linux.

  ​​	Docker Desktop for Windows：在容器内，任何挂载的文件/文件夹都将显示为归 `root` 所有，但您指定的用户仍将能够读/写它们，并且所有文件都将可执行。在本地，所有文件系统操作都将使用您本地用户的权限。这是因为从根本上没有办法将 Windows 风格的文件权限直接映射到 Linux。

- **Docker CE/EE on Linux**: Inside the container, any mounted files/folders will have the exact same permissions as outside the container - including the owner user ID (UID) and group ID (GID). Because of this, your container user will either need to have the same UID or be in a group with the same GID. The actual name of the user / group does not matter. The first user on a machine typically gets a UID of 1000, so most containers use this as the ID of the user to try to avoid this problem.

  ​​	Linux 上的 Docker CE/EE：在容器内，任何已挂载的文件/文件夹都将具有与容器外完全相同的权限 - 包括所有者用户 ID (UID) 和组 ID (GID)。因此，您的容器用户要么需要具有相同的 UID，要么属于具有相同 GID 的组。用户/组的实际名称无关紧要。机器上的第一个用户通常会获得 1000 的 UID，因此大多数容器都使用此 ID 作为用户 ID 来尝试避免此问题。

## [Specifying a user for VS Code 为 VS Code 指定用户](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_specifying-a-user-for-vs-code)

If the image or Dockerfile you are using **already provides an optional non-root user** (like the `node` image) but still defaults to root, you can opt into having Visual Studio Code (server) and any sub-processes (terminals, tasks, debugging) use it by specifying the `remoteUser` property in `devcontainer.json`:

​​	如果您正在使用的映像或 Dockerfile 已提供可选的非 root 用户（如 `node` 映像），但仍默认为 root，您可以选择让 Visual Studio Code（服务器）和任何子进程（终端、任务、调试）通过在 `devcontainer.json` 中指定 `remoteUser` 属性来使用它：

```
"remoteUser": "user-name-goes-here"
```

On Linux, if you are referencing a **Dockerfile, image, or Docker Compose** in `devcontainer.json`, this will also automatically update the container user's UID/GID to match your local user to avoid the bind mount permissions problem that exists in this environment (unless you set `"updateRemoteUserUID": false`).

​​	在 Linux 上，如果您在 `devcontainer.json` 中引用 Dockerfile、映像或 Docker Compose，这还将自动更新容器用户的 UID/GID 以匹配您的本地用户，以避免此环境中存在的绑定挂载权限问题（除非您设置 `"updateRemoteUserUID": false` ）。

Since this setting only affects VS Code and related sub-processes, VS Code needs to be restarted (or the window reloaded) for it to take effect. However, UID/GID updates are only applied when the container is created and requires a rebuild to change.

​​	由于此设置仅影响 VS Code 和相关的子进程，因此需要重新启动 VS Code（或重新加载窗口）才能使其生效。但是，UID/GID 更新仅在创建容器时应用，并且需要重建才能更改。

## [Specifying the default container user 指定默认容器用户](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_specifying-the-default-container-user)

In some cases, you may need all processes in the container to run as a different user (for example, due to startup requirements) rather than just VS Code. How you do this varies slightly depending on whether or not you are using Docker Compose.

​​	在某些情况下，您可能需要容器中的所有进程作为其他用户（例如，由于启动要求）而不是 VS Code 运行。您执行此操作的方式会根据您是否使用 Docker Compose 而略有不同。

- **Dockerfile and image**: Add the `containerUser` property to this same file.

  ​​	Dockerfile 和映像：将 `containerUser` 属性添加到此相同的文件。

  ```
  "containerUser": "user-name-goes-here"
  ```

  On Linux, like `remoteUser`, this will also automatically update the container user's UID/GID to match your local user to avoid the bind mount permissions problem that exists in this environment (unless you set `"updateRemoteUserUID": false`).

  ​​	在 Linux 上，如 `remoteUser` ，这还将自动更新容器用户的 UID/GID 以匹配您的本地用户，以避免此环境中存在的绑定挂载权限问题（除非您设置 `"updateRemoteUserUID": false` ）。

- **Docker Compose**: Update (or [extend](https://code.visualstudio.com/docs/devcontainers/create-dev-container#_extend-your-docker-compose-file-for-development)) your `docker-compose.yml` with the following for the appropriate service:

  ​​	Docker Compose：使用以下内容更新（或扩展）您的 `docker-compose.yml` 以适用于相应服务：

  ```
  user: user-name-or-UID-goes-here
  ```

## [Creating a non-root user 创建非 root 用户](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user)

While any images or Dockerfiles that come from the Dev Containers extension will include a non-root user with a UID/GID of 1000 (typically either called `vscode` or `node`), many base images and Dockerfiles do not. Fortunately, you can update or create a Dockerfile that adds a non-root user into your container.

​​	虽然来自 Dev Containers 扩展的任何映像或 Dockerfile 都将包含 UID/GID 为 1000 的非 root 用户（通常称为 `vscode` 或 `node` ），但许多基本映像和 Dockerfile 并不包含。幸运的是，您可以更新或创建一个 Dockerfile，将非 root 用户添加到容器中。

Running your application as a non-root user is recommended even in production (since it is more secure), so this is a good idea even if you're reusing an existing Dockerfile. For example, this snippet for a Debian/Ubuntu container will create a user called `user-name-goes-here`, give it the ability to use `sudo`, and set it as the default:

​​	即使在生产环境中，也建议以非 root 用户身份运行应用程序（因为这样更安全），因此即使您要重用现有的 Dockerfile，这也是一个好主意。例如，此 Debian/Ubuntu 容器的代码段将创建一个名为 `user-name-goes-here` 的用户，授予其使用 `sudo` 的权限，并将其设置为默认值：

```
ARG USERNAME=user-name-goes-here
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
```

> **Tip:** If you hit an error when building about the GID or UID already existing, the image you selected likely already has a non-root user you can take advantage of directly.
>
> ​​	提示：如果您在构建时遇到有关 GID 或 UID 已存在的错误，则您选择的映像可能已经具有您可以直接利用的非 root 用户。

In either case, if you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	无论哪种情况，如果您已经构建了容器并连接到它，请从命令面板 (F1) 运行“开发容器：从容器重建”，以获取更改。否则，请运行“开发容器：在容器中打开文件夹...”以连接到容器。

## [Change the UID/GID of an existing container user 更改现有容器用户的 UID/GID](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_change-the-uidgid-of-an-existing-container-user)

While the `remoteUser` property tries to automatically update the UID/GID as appropriate on Linux when using a **Dockerfile or image**, you can use this snippet in your Dockerfile to manually change the UID/GID of a user instead. Update the `ARG` values as appropriate.

​​	虽然 `remoteUser` 属性会尝试在使用 Dockerfile 或映像时在 Linux 上自动更新 UID/GID，但您可以在 Dockerfile 中使用此代码段来手动更改用户的 UID/GID。根据需要更新 `ARG` 值。

```
ARG USERNAME=user-name-goes-here
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupmod --gid $USER_GID $USERNAME \
    && usermod --uid $USER_UID --gid $USER_GID $USERNAME \
    && chown -R $USER_UID:$USER_GID /home/$USERNAME
```

Note that on Alpine Linux, you'll need to install the `shadow` package first.

​​	请注意，在 Alpine Linux 上，您需要先安装 `shadow` 软件包。

```
RUN apk add --no-cache shadow
```

