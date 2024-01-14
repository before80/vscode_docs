+++
title = "Connect to multiple containers"
date = 2024-01-13T13:53:43+08:00
weight = 100
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/connect-multiple-containers](https://code.visualstudio.com/remote/advancedcontainers/connect-multiple-containers)

# Connect to multiple containers 连接到多个容器



Currently you can only connect to one container per Visual Studio Code window. However, you can spin up multiple VS Code windows to [attach to them]({{< ref "/DevContainers/AttachtoContainer" >}}).

​​	目前您只能连接到每个 Visual Studio Code 窗口的一个容器。但是，您可以启动多个 VS Code 窗口以连接到它们。

If you'd prefer to use `devcontainer.json` instead and are using Docker Compose, you can create separate `devcontainer.json` files for each service in your source tree, each pointing to a common `docker-compose.yml`.

​​	如果您更愿意使用 `devcontainer.json` 并且正在使用 Docker Compose，则可以为源树中的每个服务创建单独的 `devcontainer.json` 文件，每个文件都指向一个公共 `docker-compose.yml` 。

To see how this works, consider this example source tree:

​​	要了解此工作原理，请考虑此示例源树：

```
📁 project-root
    📁 .git
    📁 .devcontainer
      📁 python-container
        📄 devcontainer.json
      📁 node-container
        📄 devcontainer.json
    📁 python-src
        📄 hello.py
    📁 node-src
        📄 hello.js
    📄 docker-compose.yml
```

The location of the `.git` folder is important, since we will need to ensure the containers can see this path for source control to work properly.

​​	 `.git` 文件夹的位置很重要，因为我们需要确保容器可以看到此路径才能正常工作源代码管理。

Next, assume the `docker-compose.yml` in the root is as follows:

​​	接下来，假设根目录中的 `docker-compose.yml` 如下所示：

```
version: '3'
services:
  python-api:
    image: mcr.microsoft.com/devcontainers/python:1-3.12-bookworm
    volumes:
      # Mount the root folder that contains .git
      - .:/workspace:cached
    command: sleep infinity
    links:
      - node-app
    # ...

  node-app:
    image: mcr.microsoft.com/devcontainers/typescript-node:1-20-bookworm
    volumes:
      # Mount the root folder that contains .git
      - .:/workspace:cached
    command: sleep infinity
    # ...
```

You can then set up `./devcontainer/python-container/devcontainer.json` for Python development as follows:

​​	然后，您可以按照如下方式设置 `./devcontainer/python-container/devcontainer.json` 以进行 Python 开发：

```
{
  "name": "Python Container",
  "dockerComposeFile": ["../../docker-compose.yml"],
  "service": "python-api",
  "shutdownAction": "none",
  "workspaceFolder": "/workspace/python-src"
}
```

Next, you can set up `./devcontainer/node-container/devcontainer.json` for Node.js development by changing `workspaceFolder`.

​​	接下来，您可以通过更改 `workspaceFolder` 来设置 `./devcontainer/node-container/devcontainer.json` 以进行 Node.js 开发。

```
{
  "name": "Node Container",
  "dockerComposeFile": ["../../docker-compose.yml"],
  "service": "node-app",
  "shutdownAction": "none",
  "workspaceFolder": "/workspace/node-src"
}
```

The `"shutdownAction":"none"` in the `devcontainer.json` files is optional, but will leave the containers running when VS Code closes -- which prevents you from accidentally shutting down both containers by closing one window.

​​	 `"shutdownAction":"none"` 中的 `devcontainer.json` 文件是可选的，但会在关闭 VS Code 时使容器保持运行状态——这可以防止您通过关闭一个窗口而意外关闭两个容器。

## [Connect to multiple containers in multiple VS Code windows 在多个 VS Code 窗口中连接到多个容器]({{< ref "/Remote/advancedcontainers/Connecttomultiplecontainers#_connect-to-multiple-containers-in-multiple-vs-code-windows" >}})

1. Open a VS Code window at the root level of the project.
   在项目的根级别打开一个 VS Code 窗口。
2. Run **Dev Containers: Reopen in Container** from the Command Palette (F1) and select `Python Container`.
   运行开发容器：从命令面板（F1）中重新在容器中打开，然后选择 `Python Container` 。
3. VS Code will then start up both containers, reload the current window and connect to the selected container.
   然后，VS Code 将启动两个容器，重新加载当前窗口并连接到所选容器。
4. Next, open a new window using **File** > **New Window**.
   接下来，使用“文件”>“新建窗口”打开一个新窗口。
5. Open your project at root level in the current window.
   在当前窗口中以根级别打开项目。
6. Run **Dev Containers: Reopen in Container** from the Command Palette (F1) and select `Node Container`.
   运行开发容器：从命令面板（F1）中重新在容器中打开，然后选择 `Node Container` 。
7. The current VS Code window will reload and connect to the selected container.
   当前 VS Code 窗口将重新加载并连接到所选容器。

You can now interact with both containers from separate windows.

​​	现在，您可以从单独的窗口与两个容器进行交互。

## [Connect to multiple containers in a single VS Code window 在单个 VS Code 窗口中连接到多个容器]({{< ref "/Remote/advancedcontainers/Connecttomultiplecontainers#_connect-to-multiple-containers-in-a-single-vs-code-window" >}})

1. Open a VS Code window at the root level of the project.
   在项目的根级别打开一个 VS Code 窗口。
2. Run **Dev Containers: Reopen in Container** from the Command Palette (F1) and select `Python Container`.
   运行开发容器：从命令面板（F1）中重新在容器中打开，然后选择 `Python Container` 。
3. VS Code will then start up both containers, reload the current window and connect to the selected container.
   VS Code 随后将启动两个容器，重新加载当前窗口并连接到所选容器。
4. Run **Dev Containers: Switch Container** from the Command Palette (F1) and select `Node Container`.
   运行开发容器：从命令面板 (F1) 切换容器并选择 `Node Container` 。
5. The current VS Code window will reload and connect to the selected container.
   当前 VS Code 窗口将重新加载并连接到所选容器。
6. You can switch back with the same command.
   您可以使用相同的命令切换回去。

## [Extending a Docker Compose file when connecting to two containers 连接到两个容器时扩展 Docker Compose 文件]({{< ref "/Remote/advancedcontainers/Connecttomultiplecontainers#_extending-a-docker-compose-file-when-connecting-to-two-containers" >}})

If you want to [extend your Docker Compose file for development]({{< ref "/DevContainers/CreateaDevContainer#_extend-your-docker-compose-file-for-development" >}}), you should use a single `docker-compose.yml` that extends **both** services (as needed) and is referenced in **both** `devcontainer.json` files.

​​	如果您想扩展 Docker Compose 文件以进行开发，则应使用一个 `docker-compose.yml` ，它扩展了两个服务（根据需要），并在两个 `devcontainer.json` 文件中引用。

For example, consider this `docker-compose.devcontainer.yml` file:

​​	例如，考虑此 `docker-compose.devcontainer.yml` 文件：

```
version: '3'
services:
  python-api:
    volumes:
      - ~:~/local-home-folder:cached # Additional bind mount
    # ...

  node-app:
    volumes:
      - ~/some-folder:~/some-folder:cached # Additional bind mount
    # ...
```

Both `.devcontainer.json` files would be updated as follows:

​​	两个 `.devcontainer.json` 文件将按如下方式更新：

```
"dockerComposeFile": [
  "../../docker-compose.yml",
  "../../docker-compose.devcontainer.yml",
]
```

This list of compose files is used when starting the containers, so referencing different files in each `devcontainer.json` can have unexpected results.

​​	此组合文件列表在启动容器时使用，因此在每个 `devcontainer.json` 中引用不同的文件可能会产生意外结果。
