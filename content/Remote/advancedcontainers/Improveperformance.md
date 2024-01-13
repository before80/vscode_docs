+++
title = "Improve performance"
date = 2024-01-13T13:53:43+08:00
weight = 60
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/improve-performance](https://code.visualstudio.com/remote/advancedcontainers/improve-performance)

# Improve disk performance 改善磁盘性能



The Dev Containers extension uses "bind mounts" to source code in your local filesystem by default. While this is the simplest option, on macOS and Windows, you may encounter slower disk performance when running commands like `yarn install` from inside the container. There are few things you can do to resolve these type of issues.

​​	默认情况下，Dev Containers 扩展使用“绑定挂载”来获取本地文件系统中的源代码。虽然这是最简单的选项，但在 macOS 和 Windows 上，您在容器内运行命令（如 `yarn install` ）时可能会遇到较慢的磁盘性能。您可以采取一些措施来解决此类问题。

## [Store your source code in the WSL 2 filesystem on Windows 将源代码存储在 Windows 上的 WSL 2 文件系统中](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_store-your-source-code-in-the-wsl-2-filesystem-on-windows)

Windows 10 2004 and up includes an improved version of the Windows Subsystem for Linux (WSL 2) that provides a full Linux kernel and has significantly improved performance over WSL 1. Docker Desktop 2.3+ includes a new WSL 2 Engine that runs Docker in WSL rather than in a VM. Therefore, if you store your source code in the WSL 2 filesystem, you will see improved performance along with better compatibility for things like setting permissions.

​​	Windows 10 2004 及更高版本包含改进版的适用于 Linux 的 Windows 子系统 (WSL 2)，它提供了一个完整的 Linux 内核，并且性能比 WSL 1 有了显著提升。Docker Desktop 2.3+ 包含一个新的 WSL 2 引擎，它在 WSL 中而不是在 VM 中运行 Docker。因此，如果您将源代码存储在 WSL 2 文件系统中，您将看到性能提升，并且在设置权限等方面具有更好的兼容性。

See [Open a WSL 2 folder in a container on Windows](https://code.visualstudio.com/docs/devcontainers/containers#_open-a-wsl-2-folder-in-a-container-on-windows) for details on using this new engine from VS Code.

​​	有关从 VS Code 使用此新引擎的详细信息，请参阅在 Windows 上的容器中打开 WSL 2 文件夹。

### [Video: Speed up Dev Containers on Windows 视频：加快 Windows 上的 Dev Containers 速度](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_video-speed-up-dev-containers-on-windows)

<iframe width="560" height="315" src="https://www.youtube.com/embed/MUsROtVmPJM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>



## [Use Clone Repository in Container Volume 在容器卷中使用克隆存储库](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_use-clone-repository-in-container-volume)

The **Dev Containers: Clone Repository in Container Volume...** command uses an isolated, local Docker named volume instead of binding to the local filesystem. In addition to not polluting your file tree, local volumes have the added benefit of improved performance on Windows and macOS.

​​	Dev Containers: 在容器卷中克隆存储库... 命令使用一个隔离的本地 Docker 命名卷，而不是绑定到本地文件系统。除了不会污染您的文件树之外，本地卷还具有在 Windows 和 macOS 上提高性能的额外好处。

See [Open a Git repository or GitHub PR in an isolated container volume](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume) for details on using this approach.

​​	有关使用此方法的详细信息，请参阅在隔离的容器卷中打开 Git 存储库或 GitHub PR。

The next two sections will outline how to use a named volume in other scenarios.

​​	接下来的两个部分将概述如何在其他场景中使用命名卷。

## [Use a targeted named volume 使用目标命名卷](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_use-a-targeted-named-volume)

Since macOS and Windows run containers in a VM, "bind" mounts are not as fast as using the container's filesystem directly. Fortunately, Docker has the concept of a local "named volume" that can act like the container's filesystem but survives container rebuilds. This makes it ideal for storing package folders like `node_modules`, data folders, or output folders like `build` where write performance is critical. Follow the appropriate steps below based on what you reference in `devcontainer.json`.

​​	由于 macOS 和 Windows 在 VM 中运行容器，“绑定”挂载不如直接使用容器的文件系统快。幸运的是，Docker 有一个本地“命名卷”的概念，它可以像容器的文件系统一样工作，但可以在容器重建后继续存在。这使其非常适合存储包文件夹（如 `node_modules` ）、数据文件夹或输出文件夹（如 `build` ），在这些文件夹中，写入性能至关重要。根据您在 `devcontainer.json` 中引用的内容，请按照以下适当的步骤操作。

**Dockerfile or image**:

​​	Dockerfile 或映像：

Let's use the [vscode-remote-try-node](https://github.com/microsoft/vscode-remote-try-node) repository to illustrate how to speed up `yarn install`.

​​	让我们使用 vscode-remote-try-node 存储库来说明如何加速 `yarn install` 。

Follow these steps:

​​	请按照以下步骤操作：

1. Use the `workspaceMount` property in `devcontainer.json` to tell VS Code where to bind your source code. Then use the `mounts` property (VS Code 1.41+) to mount the `node_modules` sub-folder into a named local volume instead.

   ​​	在 `devcontainer.json` 中使用 `workspaceMount` 属性告诉 VS Code 在何处绑定源代码。然后使用 `mounts` 属性（VS Code 1.41+）将 `node_modules` 子文件夹装入命名的本地卷中。

   ```
   "mounts": [
       "source=${localWorkspaceFolderBasename}-node_modules,target=${containerWorkspaceFolder}/node_modules,type=volume"
   ]
   ```

   > **Note**: You may use `${localWorkspaceFolderBasename}`, `${devcontainerId}`, or a hardcoded name in the `source`.
   >
   > ​​	注意：您可以在 `source` 中使用 `${localWorkspaceFolderBasename}` 、 `${devcontainerId}` 或硬编码名称。

2. Since this repository [runs VS Code as the non-root "node" user](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user), we need to add a `postCreateCommand` to be sure the user can access the folder.

   ​​	由于此存储库将 VS Code 作为非根“node”用户运行，因此我们需要添加 `postCreateCommand` 以确保用户可以访问该文件夹。

   ```
   "remoteUser": "node",
   "mounts": [
       "source=${localWorkspaceFolderBasename}-node_modules,target=${containerWorkspaceFolder}/node_modules,type=volume"
   ],
   "postCreateCommand": "sudo chown node node_modules"
   ```

   This second step is not required if you will be running in the container as `root`.

   ​​	如果您将在容器中作为 `root` 运行，则不需要此第二步。

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。

Two notes on this approach:

​​	关于此方法的两个注意事项：

1. If you delete the `node_modules` folder in the container, it may lose the connection to the volume. Delete the contents of the `node_modules` folder instead when needed (`rm -rf node_modules/* node_modules/.*`).

   ​​	如果您删除容器中的 `node_modules` 文件夹，它可能会失去与卷的连接。在需要时删除 `node_modules` 文件夹的内容（ `rm -rf node_modules/* node_modules/.*` ）。

2. You'll find that an empty `node_modules` folder gets created locally with this method. This is because the volume mount point in the container is inside the local filesystem bind mount. This is expected and harmless.

   ​​	您会发现使用此方法会在本地创建一个空的 `node_modules` 文件夹。这是因为容器中的卷装入点位于本地文件系统绑定装入点内。这是预期的，并且无害。

**Docker Compose**:

​​	Docker Compose：

While vscode-remote-try-node does not use Docker Compose, the steps are similar, but the volume mount configuration is placed in a different file.

​​	虽然 vscode-remote-try-node 不使用 Docker Compose，但步骤类似，但卷装入配置位于不同的文件中。

1. In your Docker Compose file (or an [extended one](https://code.visualstudio.com/docs/devcontainers/create-dev-container#_extend-your-docker-compose-file-for-development)), add a named local volume mount to the `node_modules` sub-folder for the appropriate service(s). For example:

   ​​	在您的 Docker Compose 文件（或扩展文件）中，为适当的服务添加一个命名本地卷挂载到 `node_modules` 子文件夹。例如：

   ```
   version: '3'
   services:
     your-service-name-here:
       volumes:
         # Or wherever you've mounted your source code
         - .:/workspace:cached
         - try-node-node_modules:/workspace/node_modules
       # ...
   
   volumes:
     try-node-node_modules:
   ```

2. Next, be sure the `workspaceFolder` property in `devcontainer.json` matches the place your actual source code is mounted:

   ​​	接下来，确保 `devcontainer.json` 中的 `workspaceFolder` 属性与实际源代码挂载的位置匹配：

   ```
   "workspaceFolder": "/workspace"
   ```

3. If you're running in the container with a [user other than root](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user), add a `postCreateCommand` to update the owner of the folder you mount since it may have been mounted as root. Replace `user-name-goes-here` with the appropriate user.

   ​​	如果您在容器中以非 root 用户身份运行，请添加 `postCreateCommand` 来更新您挂载的文件夹的所有者，因为它可能已作为 root 挂载。用适当的用户替换 `user-name-goes-here` 。

   ```
   "remoteUser": "node",
   "workspaceFolder": "/workspace",
   "postCreateCommand": "sudo chown user-name-goes-here node_modules"
   ```

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。

### [Video: Speed up npm install in a dev container 视频：在开发容器中加速 npm 安装](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_video-speed-up-npm-install-in-a-dev-container)

<iframe width="560" height="315" src="https://www.youtube.com/embed/iDdJWIPRUx4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>



## [Use a named volume for your entire source tree 为您的整个源树使用命名卷](https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_use-a-named-volume-for-your-entire-source-tree)

Finally, if none of the above options meet your needs, you can go one step further and **clone your entire source tree inside of a named volume** rather than locally. You can set up a named volume by taking an existing `devcontainer.json` configuration and modifying it as follows (updating `your-volume-name-here` with whatever you want to call the volume).

​​	最后，如果以上选项均无法满足您的需求，您可以更进一步，在命名卷中克隆整个源树，而不是在本地。您可以通过获取现有的 `devcontainer.json` 配置并按如下方式修改它来设置命名卷（用您想要调用的任何内容更新 `your-volume-name-here` ）。

Depending on what you reference in `devcontainer.json`:

​​	根据您在 `devcontainer.json` 中引用的内容：

- **Dockerfile or image**: Use the following properties in `devcontainer.json` to mount a local named volume into the container:

  ​​	Dockerfile 或映像：在 `devcontainer.json` 中使用以下属性将本地命名卷挂载到容器中：

  ```
  "workspaceMount": "source=your-volume-name-here,target=/workspace,type=volume"
  "workspaceFolder": "/workspace",
  ```

- **Docker Compose**: Update (or [extend](https://code.visualstudio.com/docs/devcontainers/create-dev-container#_extend-your-docker-compose-file-for-development)) your `docker-compose.yml` with the following for the appropriate service(s):

  ​​	Docker Compose：使用以下内容更新（或扩展）您的 `docker-compose.yml` 以获取适当的服务：

  ```
  version: '3'
  services:
    your-service-name-here:
      volumes:
          - your-volume-name-here:/workspace
      # ...
  
  volumes:
    your-volume-name-here:
  ```

  You'll also want to be sure the `workspaceFolder` property in `devcontainer.json` matches the place the volume is mounted (or a sub-folder inside the volume):

  ​​	您还需要确保 `workspaceFolder` 中的 `devcontainer.json` 属性与装载卷的位置（或卷内的子文件夹）匹配：

  ```
  "workspaceFolder": "/workspace"
  ```

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。

Next, either use the **Git: Clone** command from the Command Palette or **start an integrated terminal** (Ctrl+Shift+`) and use the `git clone` command to clone your source code into the `/workspace` folder.

​​	接下来，要么从命令面板中使用 Git：克隆命令，要么启动一个集成终端（Ctrl+Shift+`），并使用 `git clone` 命令将源代码克隆到 `/workspace` 文件夹中。

Finally, use the **File > Open... / Open Folder...** command to open the cloned repository in the container.

​​	最后，使用文件 > 打开... / 打开文件夹... 命令在容器中打开克隆的存储库。
