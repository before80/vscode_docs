+++
title = "Environment variables"
date = 2024-01-13T13:53:43+08:00
weight = 10
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/environment-variables](https://code.visualstudio.com/remote/advancedcontainers/environment-variables)

# Environment variables 环境变量



You can set environment variables in your container without altering the container image by using one of the options below.

​​	您可以使用以下选项之一在容器中设置环境变量，而无需更改容器映像。

> You should verify **Terminal > Integrated: Inherit Env** is checked in settings or the variables you set may not appear in the Integrated Terminal. This setting is checked by default.
>
> ​​	您应该验证“终端”>“集成：继承环境”在设置中已选中，否则您设置的变量可能不会出现在集成终端中。此设置默认选中。

## [Option 1: Add individual variables 选项 1：添加单独变量]({{< ref "/Remote/advancedcontainers/Environmentvariables#_option-1-add-individual-variables" >}})

Depending on what you reference in `devcontainer.json`:

​​	根据您在 `devcontainer.json` 中引用的内容：

- **Dockerfile or image**: Add the `containerEnv` property to `devcontainer.json` to set variables that should apply to the entire container or `remoteEnv` to set variables for VS Code and related sub-processes (terminals, tasks, debugging, etc.):

  ​​	Dockerfile 或映像：将 `containerEnv` 属性添加到 `devcontainer.json` 以设置应应用于整个容器的变量，或 `remoteEnv` 以设置 VS Code 和相关子进程（终端、任务、调试等）的变量：

  ```
  "containerEnv": {
      "MY_CONTAINER_VAR": "some-value-here",
      "MY_CONTAINER_VAR2": "${localEnv:SOME_LOCAL_VAR}"
  },
  "remoteEnv": {
      "PATH": "${containerEnv:PATH}:/some/other/path",
      "MY_REMOTE_VARIABLE": "some-other-value-here",
      "MY_REMOTE_VARIABLE2": "${localEnv:SOME_LOCAL_VAR}"
  }
  ```

  As this example illustrates, `containerEnv` can reference local variables and `remoteEnv` can reference both local and existing container variables.

  ​​	如本示例所示， `containerEnv` 可以引用本地变量， `remoteEnv` 可以引用本地变量和现有容器变量。

### [Video: Modify PATH in a dev container 视频：修改开发容器中的 PATH]({{< ref "/Remote/advancedcontainers/Environmentvariables#_video-modify-path-in-a-dev-container" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/vEb7hKlagAU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>







- **Docker Compose**: Since Docker Compose has built-in support for updating container-wide variables, only `remoteEnv` is supported in `devcontainer.json`:

  ​​	Docker Compose：由于 Docker Compose 具有内置支持来更新容器范围变量，因此仅在 `devcontainer.json` 中支持 `remoteEnv` ：

  ```
  "remoteEnv": {
      "PATH": "${containerEnv:PATH}:/some/other/path",
      "MY_REMOTE_VARIABLE": "some-other-value-here",
      "MY_REMOTE_VARIABLE2": "${localEnv:SOME_LOCAL_VAR}"
  }
  ```

  As this example illustrates, `remoteEnv` can reference both local and existing container variables.

  ​​	如本示例所示， `remoteEnv` 可以引用本地和现有容器变量。

  To update variables that apply to the entire container, update (or [extend]({{< ref "/DevContainers/CreateaDevContainer#_extend-your-docker-compose-file-for-development" >}})) your `docker-compose.yml` with the following for the appropriate service:

  ​​	要更新适用于整个容器的变量，请使用以下内容更新（或扩展）您的 `docker-compose.yml` 以获取相应服务：

  ```
  version: '3'
  services:
    your-service-name-here:
      environment:
        - YOUR_ENV_VAR_NAME=your-value-goes-here
        - ANOTHER_VAR=another-value
       # ...
  ```

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。

## [Option 2: Use an env file 选项 2：使用 env 文件]({{< ref "/Remote/advancedcontainers/Environmentvariables#_option-2-use-an-env-file" >}})

If you have a large number of environment variables that you need to set, you can use a `.env` file instead.

​​	如果您需要设置大量环境变量，则可以使用 `.env` 文件。

First, create an environment file somewhere in your source tree. Consider this `.devcontainer/devcontainer.env` file:

​​	首先，在源树中的某个位置创建一个环境文件。考虑此 `.devcontainer/devcontainer.env` 文件：

```
YOUR_ENV_VAR_NAME=your-value-goes-here
ANOTHER_ENV_VAR_NAME=your-value-goes-here
```

Next, depending on what you reference in `devcontainer.json`:

​​	接下来，根据您在 `devcontainer.json` 中引用的内容：

- **Dockerfile or image**: Edit `devcontainer.json` and add a path to the `devcontainer.env` :

  ​​	Dockerfile 或映像：编辑 `devcontainer.json` 并添加 `devcontainer.env` 的路径：

  ```
  "runArgs": ["--env-file",".devcontainer/devcontainer.env"]
  ```

- **Docker Compose:** Edit `docker-compose.yml` and add a path to the `devcontainer.env` file relative to the Docker Compose file:

  ​​	Docker Compose：编辑 `docker-compose.yml` 并添加 `devcontainer.env` 文件相对于 Docker Compose 文件的路径：

  ```
  version: '3'
  services:
    your-service-name-here:
      env_file: devcontainer.env
      # ...
  ```

`docker compose` will automatically pick up a file called `.env` in the folder containing the `docker-compose.yml`, but you can also create one in another location.

​​	 `docker compose` 会自动在包含 `docker-compose.yml` 的文件夹中选择名为 `.env` 的文件，但您也可以在其他位置创建一个文件。

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板 (F1) 运行 Dev Containers: Rebuild Container 以选择更改。否则，请运行 Dev Containers: Open Folder in Container... 以连接到容器。

### [Video: Load variables from an .env file 视频：从 .env 文件加载变量]({{< ref "/Remote/advancedcontainers/Environmentvariables#_video-load-variables-from-an-env-file" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/qTU7w3bWrOk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>



