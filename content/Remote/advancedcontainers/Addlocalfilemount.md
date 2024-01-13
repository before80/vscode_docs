+++
title = "Add local file mount"
date = 2024-01-13T13:53:43+08:00
weight = 30
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount)

# Add another local file mount 添加另一个本地文件挂载



> **Note:** Mounting the local file system is not supported in GitHub Codespaces. See [developing inside a container on a remote Docker host](https://code.visualstudio.com/remote/advancedcontainers/develop-remote-host) for information on mounting remote folders in this scenario.
>
> ​​	注意：在 GitHub Codespaces 中不支持挂载本地文件系统。有关在此方案中挂载远程文件夹的信息，请参阅在远程 Docker 主机上的容器内进行开发。

You can add a volume bound to any local folder by using the following appropriate steps, based on what you reference in `devcontainer.json`:

​​	您可以通过执行以下适当的步骤来添加绑定到任何本地文件夹的卷，具体取决于您在 `devcontainer.json` 中引用的内容：

- **Dockerfile or image**: Add the following to the `mounts` property (VS Code 1.41+) in this same file:

  ​​	Dockerfile 或映像：将以下内容添加到此相同文件中的 `mounts` 属性（VS Code 1.41+）：

  ```
  "mounts": [
    "source=/local/source/path/goes/here,target=/target/path/in/container/goes/here,type=bind,consistency=cached"
  ]
  ```

  You can also reference local environment variables or the local path of the workspace. For example, this will bind mount `~` (`$HOME`) on macOS/Linux and the user's folder (`%USERPROFILE%`) on Windows and a sub-folder in the workspace to a different location:

  ​​	您还可以引用本地环境变量或工作区的本地路径。例如，这将在 macOS/Linux 上绑定挂载 `~` ( `$HOME` )，在 Windows 上绑定挂载用户的文件夹 ( `%USERPROFILE%` )，并将工作区中的子文件夹绑定挂载到其他位置：

  ```
  "mounts": [
      "source=${localEnv:HOME}${localEnv:USERPROFILE},target=/host-home-folder,type=bind,consistency=cached",
      "source=${localWorkspaceFolder}/app-data,target=/data,type=bind,consistency=cached"
  ]
  ```

### [Video: Add additional folders from your local machine to a dev container 视频：将本地计算机中的其他文件夹添加到开发容器](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount#_video-add-additional-folders-from-your-local-machine-to-a-dev-container)

<iframe width="560" height="315" src="https://www.youtube.com/embed/L1-dx-ZD0Ao" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>







- **Docker Compose:** Update (or [extend](https://code.visualstudio.com/docs/devcontainers/create-dev-container#_extend-your-docker-compose-file-for-development)) your `docker-compose.yml` with the following for the appropriate service:

  ​​	Docker Compose：使用以下内容更新（或扩展）您的 `docker-compose.yml` 以适用于相应服务：

  ```
  version: '3'
  services:
    your-service-name-here:
      volumes:
        - /local/source/path/goes/here:/target/path/in/container/goes/here:cached
        - ~:/host-home-folder:cached
        - ./data-subfolder:/data:cached
       # ...
  ```

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。
