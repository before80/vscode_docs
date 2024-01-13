+++
title = "Set Docker Compose project name"
date = 2024-01-13T13:53:43+08:00
weight = 80
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/set-docker-compose-project-name](https://code.visualstudio.com/remote/advancedcontainers/set-docker-compose-project-name)

# Set Docker Compose project name 设置 Docker Compose 项目名称



Visual Studio Code will respect the value of the [COMPOSE_PROJECT_NAME](https://docs.docker.com/compose/reference/envvars/#compose_project_name) environment variable if set for the VS Code process or in a `.env` file in the root of the project.

​​	如果为 VS Code 进程或项目根目录中的 `.env` 文件设置了 COMPOSE_PROJECT_NAME 环境变量的值，Visual Studio Code 将尊重该值。

For example, after shutting down all VS Code windows, you can start VS Code from the command line as follows:

​​	例如，关闭所有 VS Code 窗口后，您可以通过以下方式从命令行启动 VS Code：

```
# from bash
COMPOSE_PROJECT_NAME=foo code .
# from PowerShell
$env:COMPOSE_PROJECT_NAME=foo
code .
```

Or add the following to a `.env` file in the root of the project (**not** in the `.devcontainer` folder):

​​	或者将以下内容添加到项目根目录中的 `.env` 文件（不在 `.devcontainer` 文件夹中）：

```
COMPOSE_PROJECT_NAME=foo
```
