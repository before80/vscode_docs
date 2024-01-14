+++
title = "Develop on a remote Docker host"
date = 2024-01-13T13:53:43+08:00
weight = 120
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/develop-remote-host](https://code.visualstudio.com/remote/advancedcontainers/develop-remote-host)

# Develop on a remote Docker host 在远程 Docker 主机上开发



Sometimes you may want to use the Dev Containers extension to develop inside a container that sits on a remote server. Docker does **not** support mounting (binding) your local filesystem into a remote dev container, so Visual Studio Code's default `devcontainer.json` behavior to use your local source code will not work. While this is the default behavior, in this section we will cover connecting to a remote host so that you can either [use the Remote - SSH extension]({{< ref "/Remote/SSH" >}}) to open a folder on a remote host in a container, [attach to any running container]({{< ref "/DevContainers/AttachtoContainer" >}}), or use a **local** `devcontainer.json` file as a way to configure, create, and connect to a remote dev container using a socket.

​​	有时您可能希望使用 Dev Containers 扩展在位于远程服务器上的容器内进行开发。Docker 不支持将本地文件系统装入（绑定）到远程开发容器中，因此 Visual Studio Code 使用本地源代码的默认 `devcontainer.json` 行为将不起作用。虽然这是默认行为，但在本节中，我们将介绍如何连接到远程主机，以便您可以使用 Remote - SSH 扩展在容器中打开远程主机上的文件夹、附加到任何正在运行的容器，或使用本地 `devcontainer.json` 文件作为一种方式来配置、创建和连接到使用套接字的远程开发容器。

## [Connect using the Remote - SSH extension 使用 Remote - SSH 扩展进行连接]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-the-remote-ssh-extension" >}})

If you are using a Linux or macOS SSH host, you can use the [Remote - SSH]({{< ref "/Remote/SSH" >}}) and Dev Containers extensions together. You do not even need to have a Docker client installed locally. To do so:

​​	如果您使用的是 Linux 或 macOS SSH 主机，则可以同时使用 Remote - SSH 和 Dev Containers 扩展。您甚至不需要在本地安装 Docker 客户端。要做到这一点：

1. Follow the [installation]({{< ref "/Remote/SSH#_installation" >}}) and SSH [host setup]({{< ref "/Remote/SSH#_ssh-host-setup" >}}) steps for the Remote - SSH extension.
   按照 Remote - SSH 扩展的安装和 SSH 主机设置步骤操作。
2. **Optional:** Set up SSH [key based authentication]({{< ref "/Remote/TipsandTricks#_configuring-key-based-authentication" >}}) to the server so you do not need to enter your password multiple times.
   可选：设置基于 SSH 密钥的身份验证到服务器，以便您无需多次输入密码。
3. [Install Docker]({{< ref "/DevContainers/Overview#installation" >}}) on your SSH host. You do not need to install Docker locally.
   在您的 SSH 主机上安装 Docker。您无需在本地安装 Docker。
4. Follow the [quick start]({{< ref "/Remote/SSH#_connect-to-a-remote-host" >}}) for the Remote - SSH extension to connect to a host and open a folder there.
   按照 Remote - SSH 扩展的快速入门指南连接到主机并在其中打开文件夹。
5. Use the **Dev Containers: Reopen in Container** command from the Command Palette (F1, Ctrl+Shift+P).
   从命令面板（F1、Ctrl+Shift+P）中使用 Dev Containers：在容器中重新打开命令。

The rest of the Dev Containers quick start applies as-is. You can learn more about the [Remote - SSH extension in its documentation]({{< ref "/Remote/SSH" >}}).

​​	Dev Containers 快速入门指南的其余部分照常适用。您可以在其文档中了解有关 Remote - SSH 扩展的更多信息。

## [Connect using the Remote - Tunnels extension 使用 Remote - Tunnels 扩展进行连接]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-the-remote-tunnels-extension" >}})

You can use the [Remote - Tunnels]({{< ref "/Remote/Tunnels" >}}) and Dev Containers extensions together to open a folder on your remote host inside of a container. You do not even need to have a Docker client installed locally. This is similar to the SSH host scenario above, but uses Remote - Tunnels instead. To do so:

​​	您可以将 Remote - Tunnels 和 Dev Containers 扩展一起使用，以便在容器内打开远程主机上的文件夹。您甚至不需要在本地安装 Docker 客户端。这类似于上面的 SSH 主机方案，但使用的是 Remote - Tunnels。为此，请执行以下操作：

1. Follow the [Getting Started]({{< ref "/Remote/Tunnels#_getting-started" >}}) instructions for the Remote - Tunnels extension.
   按照 Remote - Tunnels 扩展的入门说明进行操作。
2. [Install Docker]({{< ref "/DevContainers/Overview#installation" >}}) on your tunnel host. You do not need to install Docker locally.
   在您的隧道主机上安装 Docker。您无需在本地安装 Docker。
3. Follow the [steps]({{< ref "/Remote/Tunnels#_remote-tunnels-extension" >}}) for the Remote - Tunnels extension to connect to a tunnel host and open a folder there.
   按照 Remote - Tunnels 扩展的步骤操作，以连接到隧道主机并在其中打开文件夹。
4. Use the **Dev Containers: Reopen in Container** command from the Command Palette (F1, Ctrl+Shift+P).
   从命令面板（F1、Ctrl+Shift+P）中使用 Dev Containers：在容器中重新打开命令。

The rest of the Dev Containers quick start applies as-is. You can learn more about the [Remote - Tunnels extension in its documentation]({{< ref "/Remote/Tunnels" >}}).

​​	Dev Containers 快速入门指南的其余部分照常适用。您可以在其文档中了解有关 Remote - Tunnels 扩展的更多信息。

## [Connect using the Docker CLI 使用 Docker CLI 连接]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-the-docker-cli" >}})

This model only requires that a Docker Engine be running on a remote host that your local Docker CLI can connect to. While using the Remote - SSH and Remote - Tunnels extensions is easier and doesn't require the Docker CLI to even be installed locally, this model can be useful for situations where you already have a host you are connecting to from the command line. This approach is also useful if you are looking to attach to already running containers on this remote server.

​​	此模型仅要求在远程主机上运行 Docker 引擎，以便本地 Docker CLI 可以连接到该引擎。虽然使用 Remote - SSH 和 Remote - Tunnels 扩展更简单，并且甚至不需要在本地安装 Docker CLI，但此模型对于您已经通过命令行连接到的主机的情况非常有用。如果您希望附加到此远程服务器上已在运行的容器，此方法也很有用。

### [A basic remote example 基本远程示例]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_a-basic-remote-example" >}})

Setting up VS Code to attach to a container on a remote Docker host can be as easy as setting the [Docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) `docker.environment` property in `settings.json` and restarting VS Code (or reloading the window).

​​	将 VS Code 设置为附加到远程 Docker 主机上的容器，可以像在 `settings.json` 中设置 Docker 扩展 `docker.environment` 属性并重新启动 VS Code（或重新加载窗口）一样简单。

For example:

​​	例如：

```
"docker.environment": {
    "DOCKER_HOST": "ssh://your-remote-user@your-remote-machine-fqdn-or-ip-here"
}
```

Using SSH requires a [supported SSH client]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-client" >}}), that you have [key based authentication]({{< ref "/Remote/TipsandTricks#_configuring-key-based-authentication" >}}) configured for the remote host, and that the **key is imported into your local SSH agent**. See the article on [using SSH Keys with Git]({{< ref "/DevContainers/Overview#_using-ssh-keys" >}}) for details on configuring the agent and adding your key.

​​	使用 SSH 需要受支持的 SSH 客户端，您必须为远程主机配置基于密钥的身份验证，并且密钥已导入到您的本地 SSH 代理中。有关配置代理和添加密钥的详细信息，请参阅有关将 SSH 密钥与 Git 配合使用的文章。

At this point, you can [attach]({{< ref "/DevContainers/AttachtoContainer" >}}) to containers on the remote host. We'll cover more on information on how you can connect using [settings and environment variables]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-vs-code-settings-or-local-environment-variables" >}}) or [Docker contexts]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-docker-contexts" >}}) later in this section.

​​	此时，您可以连接到远程主机上的容器。我们将在本节的后面介绍有关如何使用设置和环境变量或 Docker 上下文进行连接的更多信息。

For `devcontainer.json`, there is one additional step: You'll need to update any configured (or auto-configured) bind mounts so they no longer point to the local filesystem.

​​	对于 `devcontainer.json` ，还有一个额外的步骤：您需要更新任何已配置（或自动配置）的绑定挂载，以便它们不再指向本地文件系统。

There's two variations of this setup. The first is to **create your remote dev container first**, and then **clone your source code into a named volume** since this does not require you to have direct access to the filesystem on the remote host.

​​	此设置有两个变体。第一个是先创建远程开发容器，然后将源代码克隆到命名卷中，因为这不需要您直接访问远程主机上的文件系统。

Here is a basic `devcontainer.json` example of this setup:

​​	以下是一个基本的 `devcontainer.json` 示例设置：

```
{
  "image": "node", // Or "dockerFile"
  "workspaceFolder": "/workspace",
  "workspaceMount": "source=remote-workspace,target=/workspace,type=volume"
}
```

In fact, the **Dev Containers: Clone Repository in Container Volume...** command in the Command Palette (F1) uses this same technique. If you already have a `devcontainer.json` file in a GitHub repository that references an image or Dockerfile, the command will automatically use a named volume instead of a bind mount - which also works with remote hosts.

​​	事实上，“命令面板”（F1）中的“开发容器：在容器卷中克隆存储库...”命令使用了相同的技术。如果您已经在 GitHub 存储库中拥有一个引用映像或 Dockerfile 的 `devcontainer.json` 文件，该命令将自动使用命名卷而不是绑定挂载 - 这也适用于远程主机。

The second approach is to **bind mount a folder on the remote machine** into your container. This requires you to have access to the remote filesystem, but also allows you to work with **existing source code** on the remote machine.

​​	第二种方法是将远程计算机上的文件夹绑定挂载到容器中。这要求您能够访问远程文件系统，但还允许您使用远程计算机上的现有源代码。

Update the `workspaceMount` property in the example above to use this model instead:

​​	将上面示例中的 `workspaceMount` 属性更新为使用此模型：

```
"workspaceMount": "source=/absolute/path/on/remote/machine,target=/workspace,type=bind,consistency=cached"
```

In either case, to try it out, run **Dev Containers: Open Folder in Container...**, and select the local folder with the `.devcontainer.json` file in it.

​​	无论哪种情况，要试用它，请运行“开发容器：在容器中打开文件夹...”，然后选择其中包含 `.devcontainer.json` 文件的本地文件夹。

See [Converting an existing or pre-defined devcontainer.json]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_converting-an-existing-or-predefined-devcontainerjson" >}}) for information on other scenarios like Docker Compose.

​​	有关 Docker Compose 等其他方案的信息，请参阅转换现有或预定义的 devcontainer.json。

## [Connect using VS Code settings or local environment variables 使用 VS Code 设置或本地环境变量进行连接]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-vs-code-settings-or-local-environment-variables" >}})

If you already have a remote Docker host up and running, you can use the following properties in your workspace or user `settings.json` to specify the host.

​​	如果您已经启动并运行了远程 Docker 主机，则可以使用工作区或用户 `settings.json` 中的以下属性来指定主机。

### [SSH protocol SSH 协议]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_ssh-protocol" >}})

Recent versions of Docker (18.06+) have added support for the SSH protocol to connect to remote Docker Host. This is easy to configure as you only need to set one property in `settings.json` to use it.

​​	Docker 的最新版本（18.06+）已添加对 SSH 协议的支持，以连接到远程 Docker 主机。这很容易配置，因为您只需要在 `settings.json` 中设置一个属性即可使用它。

First, install a [supported SSH client]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-client" >}}), configure [key based authentication]({{< ref "/Remote/TipsandTricks#_configuring-key-based-authentication" >}})), and then **import your key into your local SSH agent** (which often is not running by default on Windows and Linux). See the article on [using SSH Keys with Git]({{< ref "/DevContainers/Overview#_using-ssh-keys" >}}) for details on configuring the agent and adding the key.

​​	首先，安装受支持的 SSH 客户端，配置基于密钥的身份验证，然后将您的密钥导入到本地 SSH 代理（通常在 Windows 和 Linux 上默认不运行）。有关配置代理和添加密钥的详细信息，请参阅有关将 SSH 密钥与 Git 配合使用的文章。

Then, add the following [Docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) `docker.environment` property to `settings.json` (replacing values as appropriate):

​​	然后，将以下 Docker 扩展 `docker.environment` 属性添加到 `settings.json` （根据需要替换值）：

```
"docker.environment": {
    "DOCKER_HOST": "ssh://your-remote-user@your-remote-machine-fqdn-or-ip-here"
}
```

After restarting VS Code (or reloading the window), you will now be able to [attach to any running container]({{< ref "/DevContainers/AttachtoContainer" >}}) on the remote host. You can also [use specialized, local `devcontainer.json` files to create / connect to a remote dev container]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_converting-an-existing-or-predefined-devcontainerjson" >}}).

​​	重新启动 VS Code（或重新加载窗口）后，您现在将能够连接到远程主机上的任何正在运行的容器。您还可以使用专门的本地 `devcontainer.json` 文件来创建/连接到远程开发容器。

> **Tip:** If this is not working for you but you are able to connect to the host using SSH from the command line, be sure you have the [SSH agent running with your authentication key]({{< ref "/DevContainers/Overview#_using-ssh-keys" >}}). If all else fails, you can use [an SSH tunnel as a fallback]({{< ref "/DevContainers/TipsandTricks#_using-an-ssh-tunnel-to-connect-to-a-remote-docker-host" >}}) instead.
>
> ​​	提示：如果这对您不起作用，但您能够从命令行使用 SSH 连接到主机，请确保 SSH 代理正在使用您的身份验证密钥运行。如果所有方法都失败，您可以改用 SSH 隧道作为后备。

### [Using the TCP protocol 使用 TCP 协议]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_using-the-tcp-protocol" >}})

While the SSH protocol has its own built-in authorization mechanism, using the TCP protocol often requires setting other [Docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) properties in your `settings.json`. These are:

​​	虽然 SSH 协议有其内置的授权机制，但使用 TCP 协议通常需要在 `settings.json` 中设置其他 Docker 扩展属性。这些属性包括：

```
"docker.environment": {
    "DOCKER_HOST": "tcp://your-remote-machine-fqdn-or-ip-here:port",
    "DOCKER_CERT_PATH": "/optional/path/to/folder/with/certificate/files",
    "DOCKER_TLS_VERIFY": "1" // or "0"
}
```

As with SSH, restart VS Code (or reload the window) for the settings to take effect.

​​	与 SSH 一样，重新启动 VS Code（或重新加载窗口）以使设置生效。

### [Using environment variables instead of settings.json 使用环境变量而不是 settings.json]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_using-environment-variables-instead-of-settingsjson" >}})

If you'd prefer not to use `settings.json`, you can set **environment variables** in a terminal instead. The steps to do so are:

​​	如果您不想使用 `settings.json` ，可以在终端中设置环境变量。具体步骤如下：

1. Shut down **all instances** of VS Code.
   关闭 VS Code 的所有实例。
2. Ensure VS Code is in your operating system `PATH`.
   确保 VS Code 在您的操作系统 `PATH` 中。
3. Set the environment variables (for example `DOCKER_HOST`) in a terminal / command prompt.
   在终端/命令提示符中设置环境变量（例如 `DOCKER_HOST` ）。
4. Type `code` in this same terminal / command prompt to launch VS Code with the variables set.
   在此终端/命令提示符中键入 `code` 以启动已设置变量的 VS Code。

## [Connect using Docker Contexts 使用 Docker 上下文进行连接]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_connect-using-docker-contexts" >}})

[Docker Contexts](https://docs.docker.com/engine/context/working-with-contexts/) allow you to interact with different hosts - you can set up contexts for each host and switch between them.

​​	Docker 上下文允许您与不同的主机进行交互 - 您可以为每个主机设置上下文并在它们之间切换。

You create new contexts with `docker context create`. The current context can be changed using `docker context use <context>`.

​​	您可以使用 `docker context create` 创建新上下文。可以使用 `docker context use <context>` 更改当前上下文。

The [Docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) comes with the `docker.environment` setting where environment variables like `DOCKER_HOST` or `DOCKER_CONTEXT` can be set that are also honored by the Dev Containers extension.

​​	Docker 扩展附带 `docker.environment` 设置，其中可以设置环境变量，例如 `DOCKER_HOST` 或 `DOCKER_CONTEXT` ，Dev Containers 扩展也会遵守这些变量。

> **Note:** The above settings are only visible when the Docker extension is installed. Without the Docker extension, Dev Containers will use the current context.
>
> ​​	注意：只有在安装了 Docker 扩展时，才能看到上述设置。如果没有 Docker 扩展，Dev Containers 将使用当前上下文。

## [Converting an existing or pre-defined devcontainer.json 转换现有或预定义的 devcontainer.json]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_converting-an-existing-or-predefined-devcontainerjson" >}})

To convert an existing or pre-defined, local `devcontainer.json` into a remote one, follow these steps:

​​	若要将现有或预定义的本地 `devcontainer.json` 转换为远程 `devcontainer.json`，请执行以下步骤：

1. Open a **local** folder in VS Code (not a remote one) where you want to convert the file.

   ​​	在 VS Code 中打开一个本地文件夹（不是远程文件夹），您要在其中转换文件。

2. If you did not select a folder with a `devcontainer.json` in it, you can pick a pre-defined one by running **Dev Containers: Add Container Configuration File...** from the Command Palette (F1).

   ​​	如果您没有选择包含 `devcontainer.json` 的文件夹，则可以通过从命令面板 (F1) 运行 Dev Containers: Add Container Configuration File... 来选择预定义的文件夹。

3. Follow these steps based on what your `.devcontainer/devcontainer.json` or `.devcontainer.json` references to alter the source code mount:

   ​​	根据 `.devcontainer/devcontainer.json` 或 `.devcontainer.json` 对源代码装入的引用，执行以下步骤进行更改：

   **Dockerfile or image**:

   ​​	Dockerfile 或映像：

   If you do **not** have login access to the remote host, use a Docker "volume" for your source code. Update `.devcontainer/devcontainer.json` as follows (replacing `remote-workspace` with a unique volume name if desired):

   ​​	如果您无权登录远程主机，请为源代码使用 Docker“卷”。按如下方式更新 `.devcontainer/devcontainer.json` （如果需要，请将 `remote-workspace` 替换为唯一的卷名称）：

   ```
   "workspaceMount": "source=remote-workspace,target=/workspace,type=volume"
   "workspaceFolder": "/workspace",
   ```

   If you **do** have login access, you can use a remote filesystem bind mount instead:

   ​​	如果您有登录访问权限，您可以改用远程文件系统绑定挂载：

   ```
   "workspaceMount": "source=/absolute/path/on/remote/machine,target=/workspace,type=bind,consistency=cached"
   "workspaceFolder": "/workspace",
   ```

   The `workspaceMount` property supports the same values as the [Docker CLI `--mount` flag](https://docs.docker.com/engine/reference/commandline/run/#add-bind-mounts-or-volumes-using-the---mount-flag) if you have a different scenario in mind.

   ​​	如果您有不同的方案， `workspaceMount` 属性支持与 Docker CLI `--mount` 标志相同的值。

   **Docker Compose**:

   ​​	Docker Compose：

   If you do **not** have login access to the remote host, update (or [extend]({{< ref "/DevContainers/CreateaDevContainer#_extend-your-docker-compose-file-for-development" >}})) your `docker-compose.yml`. Replace `your-service-name-here` with the value specified for the `"service"` property in `devcontainer.json` and appropriate and `remote-workspace` with a unique volume name:

   ​​	如果您没有远程主机的登录访问权限，请更新（或扩展）您的 `docker-compose.yml` 。将 `your-service-name-here` 替换为在 `devcontainer.json` 中为 `"service"` 属性指定的值，并将 `remote-workspace` 替换为唯一的卷名称：

   ```
   version: '3'
   services:
     your-service-name-here:
       volumes:
           - remote-workspace:/workspace
       # ...
   
   volumes:
     remote-workspace:
   ```

   If you **do** have login access, you can use a remote filesystem bind mount instead:

   ​​	如果您有登录访问权限，您可以改用远程文件系统绑定挂载：

   ```
   version: '3'
   services:
     your-service-name-here:
       volumes:
         - /absolute/path/on/remote/machine:/workspace:cached
       # ...
   ```

   See the [Docker Compose documentation on `volumes`](https://docs.docker.com/compose/compose-file/#volumes) if you need to support a different scenario.

   ​​	如果您需要支持不同的方案，请参阅 Docker Compose 关于 `volumes` 的文档。

4. Run the **Dev Containers: Reopen in Container** command from the Command Palette (F1) or **Dev Containers: Rebuild Container**.

   ​​	从命令面板 (F1) 或 Dev Containers: Rebuild Container 运行 Dev Containers: Reopen in Container 命令。

5. If you used a volume instead of a bind mount, use Ctrl+Shift+` to open a terminal inside the container. You can run `git clone` from here to pull down your source code and use **File > Open... / Open Folder...** to open the cloned repository.

   ​​	如果您使用卷而不是绑定挂载，请使用 Ctrl+Shift+` 在容器内打开一个终端。您可以从此处运行 `git clone` 以提取源代码，并使用文件 > 打开... / 打开文件夹... 打开克隆的存储库。

Next time you want to connect to this same container, run **Dev Containers: Open Folder in Container...** and select the same local folder in a VS Code window.

​​	下次您想要连接到此同一容器时，请运行 Dev Containers: Open Folder in Container...，并在 VS Code 窗口中选择相同的本地文件夹。

## [Optional: Making the remote source code available locally 可选：使远程源代码在本地可用]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost#_optional-making-the-remote-source-code-available-locally" >}})

If you store your source code on the remote host's filesystem instead of inside a Docker volume, there are several ways you can access the files locally:

​​	如果您将源代码存储在远程主机的文件系统中，而不是 Docker 卷中，则有几种方法可以本地访问文件：

1. [Mount the remote filesystem using SSHFS]({{< ref "/Remote/TipsandTricks#_using-sshfs-to-access-files-on-your-remote-host" >}}).
   使用 SSHFS 挂载远程文件系统。
2. [Sync files from the remote host to your local machine using `rsync`]({{< ref "/Remote/TipsandTricks#_using-rsync-to-maintain-a-local-copy-of-your-source-code" >}}).
   使用 `rsync` 将文件从远程主机同步到本地计算机。
3. [Use the mount command](https://docs.docker.com/machine/reference/mount/) if you are using [Docker Machine](https://docs.docker.com/machine/).
   如果您使用的是 Docker Machine，请使用 mount 命令。

Using SSHFS or Docker Machine's mount command are the more convenient options and do not require any file sync'ing. However, performance will be significantly slower than working through VS Code, so they are best used for single file edits and uploading/downloading content. If you need to use an application that bulk reads/write to many files at once (like a local source control tool), rsync is a better choice.

​​	使用 SSHFS 或 Docker Machine 的 mount 命令是更方便的选择，并且不需要任何文件同步。但是，性能将比通过 VS Code 工作慢得多，因此最适合用于编辑单个文件和上传/下载内容。如果您需要使用一次批量读/写多个文件的应用程序（例如本地源代码管理工具），则 rsync 是更好的选择。
