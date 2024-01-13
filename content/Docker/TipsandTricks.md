+++
title = "Tips and Tricks"
date = 2024-01-12T22:36:24+08:00
weight = 110
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/containers/troubleshooting](https://code.visualstudio.com/docs/containers/troubleshooting)

# Docker Tools Tips and Tricks Docker 工具提示和技巧



This article covers troubleshooting tips and tricks for the Visual Studio Code [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) extension. See the [Overview](https://code.visualstudio.com/docs/containers/overview) and quickstart articles for [Node.js](https://code.visualstudio.com/docs/containers/quickstart-node), [Python](https://code.visualstudio.com/docs/containers/quickstart-python), or [ASP.NET](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core) for details on setting up and working with Docker.

​​	本文介绍了 Visual Studio Code Docker 扩展的故障排除提示和技巧。有关设置和使用 Docker 的详细信息，请参阅 Node.js、Python 或 ASP.NET 的概述和快速入门文章。

## [Running as a non-root user 以非 root 用户身份运行](https://code.visualstudio.com/docs/containers/troubleshooting#_running-as-a-nonroot-user)

For security reasons, we recommend selecting the default ports when executing the **Add Dockerfiles to Workspace** command, or otherwise opting for a port **greater than** 1023 whenever possible. This will allow VS Code to configure the Dockerfile with non-root access and prevent a malicious user from elevating permissions in the container. In some cases, there is no port selection, so the Docker extension configures non-root access by default. In all cases, you must ensure each resource (such as ports and files) modified or used by your application can be accessed by a non-root user in your container.

​​	出于安全原因，我们建议在执行“将 Dockerfile 添加到工作区”命令时选择默认端口，或者尽可能选择大于 1023 的端口。这将允许 VS Code 使用非 root 访问权限配置 Dockerfile，并防止恶意用户提升容器中的权限。在某些情况下，没有端口选择，因此 Docker 扩展默认配置非 root 访问权限。在所有情况下，您都必须确保容器中的非 root 用户可以访问应用程序修改或使用的每个资源（例如端口和文件）。

If you select a port less than 1024 when adding Dockerfiles to the workspace, the Docker extension **cannot** create a Dockerfile that runs the container as a non-root user. This is because ports in this range are called **well-known** or **system** ports and must execute with root privileges in order to bind a network socket to an IP address.

​​	如果在将 Dockerfile 添加到工作区时选择小于 1024 的端口，则 Docker 扩展无法创建将容器作为非 root 用户运行的 Dockerfile。这是因为此范围内的端口称为众所周知的端口或系统端口，并且必须使用 root 权限才能将网络套接字绑定到 IP 地址。

The **Add Dockerfiles to Workspace** command sets up non-root privileges if you choose a non-system port. If your current Dockerfile and `tasks.json` is not set up for non-root usage, try running the command **Add Dockerfiles to Workspace**, and select a port **greater than** 1023. This command overwrites your current Dockerfile and `tasks.json`. For some project types, such as **Python: General**, you might still need to modify your Dockerfile and `tasks.json`. Within the Dockerfile, you must expose a **non-system port**, create a working directory for your app code, and then add a non-root user with access to the app directory. Ensure that your exposed port is updated wherever it is referenced. In the example below, the Gunicorn port had to be updated to match the exposed port:

​​	如果选择非系统端口，“将 Dockerfile 添加到工作区”命令会设置非 root 权限。如果当前的 Dockerfile 和 `tasks.json` 未设置为非 root 使用，请尝试运行命令“将 Dockerfile 添加到工作区”，并选择大于 1023 的端口。此命令会覆盖当前的 Dockerfile 和 `tasks.json` 。对于某些项目类型（例如 Python：常规），您可能仍需要修改 Dockerfile 和 `tasks.json` 。在 Dockerfile 中，您必须公开一个非系统端口，为您的应用代码创建一个工作目录，然后添加一个对应用目录具有访问权限的非 root 用户。确保在引用的任何位置更新公开的端口。在下面的示例中，必须更新 Gunicorn 端口以匹配公开的端口：

```
# 1024 or higher
EXPOSE 1024

# ... other directives such as installing requirements.txt file

# Creates /app in container if it does not already exist
# Ports code into /app
WORKDIR /app
ADD . /app

# Creates a non-root user and adds permission to access the /app folder
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
USER appuser

CMD ["gunicorn", "--bind", "0.0.0.0:1024", "pythonPath.to.wsgi"]
```

Next, ensure the `docker run` task in `tasks.json` also expects the same port. You can usually search for any occurrences of the old port number in `tasks.json` and replace it with the new port number. The following example shows the required changes in the case of a Python Django app:

​​	接下来，确保 `tasks.json` 中的 `docker run` 任务也预期相同的端口。您通常可以在 `tasks.json` 中搜索旧端口号的任何出现并用新端口号替换它。以下示例显示了 Python Django 应用中所需更改：

```
{
  "type": "docker-run",
  "label": "docker-run: debug",
  "dependsOn": ["docker-build"],
  "python": {
    "args": [
      "runserver",
      "0.0.0.0:1024", //<- Change the number after the colon
      "--nothreading",
      "--noreload"
    ],
    "file": "manage.py"
  }
}
```

## [Error "connect EACCES /var/run/docker.sock" on Linux Linux 上的错误“connect EACCES /var/run/docker.sock”](https://code.visualstudio.com/docs/containers/troubleshooting#_error-connect-eacces-varrundockersock-on-linux)

Since VS Code runs as a non-root user, you will need to follow the steps in "Manage Docker as a non-root user" from [Post-installation steps for Linux](https://aka.ms/AA37yk6) to access Docker from the extension.

​​	由于 VS Code 以非 root 用户身份运行，因此您需要按照 Linux 安装后步骤中的“以非 root 用户身份管理 Docker”中的步骤操作，才能从扩展访问 Docker。

## [Docker containers and images have disappeared from Docker view Docker 容器和映像已从 Docker 视图中消失](https://code.visualstudio.com/docs/containers/troubleshooting#_docker-containers-and-images-have-disappeared-from-docker-view)

This is most likely caused by a conflict with another extension called `Docker Explorer` (not authored by Microsoft). To resolve this issue, use a workaround described [vscode-docker issue #1609](https://github.com/microsoft/vscode-docker/issues/1609#issuecomment-586331394).

​​	这很可能是由于与另一个名为 `Docker Explorer` 的扩展（非 Microsoft 创作）发生冲突所致。要解决此问题，请使用 vscode-docker 问题 #1609 中描述的解决方法。

## [The extension does not find Docker on a remote machine 扩展在远程计算机上找不到 Docker](https://code.visualstudio.com/docs/containers/troubleshooting#_the-extension-does-not-find-docker-on-a-remote-machine)

Error message "Failed to connect. Is Docker installed and running?"

​​	错误消息“连接失败。Docker 是否已安装并正在运行？”

1. Make sure Docker engine **is installed** on the remote machine and that Docker CLI works (run `docker ps` from the terminal and ensure it does not return any errors).
   确保 Docker 引擎已安装在远程计算机上，并且 Docker CLI 可正常工作（从终端运行 `docker ps` ，并确保它不会返回任何错误）。
2. If you are using a remote development environment (remote machine via SSH, WSL subsystem, GitHub Codespace), make sure the Docker extension is installed remotely as well as locally.
   如果您使用的是远程开发环境（通过 SSH、WSL 子系统、GitHub Codespace 的远程计算机），请确保 Docker 扩展已在远程和本地安装。

## [Invalid URL errors 无效的 URL 错误](https://code.visualstudio.com/docs/containers/troubleshooting#_invalid-url-errors)

If you have a need to connect to a remote Docker daemon, we recommend using Docker contexts instead of a `docker.environment` attribute in the settings. Check out this guide to learn how to [create and use a context](https://docs.docker.com/engine/context/working-with-contexts/) to communicate with a remote Docker daemon.

​​	如果您需要连接到远程 Docker 守护程序，我们建议使用 Docker 上下文，而不是设置中的 `docker.environment` 属性。查看本指南，了解如何创建和使用上下文与远程 Docker 守护程序通信。

If you still need to override the Docker context you are currently using, make sure your `DOCKER_HOST` environment variable or `docker.environment.DOCKER_HOST` attribute includes a protocol in the URL (for example, `ssh://myuser@mymachine` or `tcp://1.2.3.4`).

​​	如果您仍需要覆盖当前使用的 Docker 上下文，请确保您的 `DOCKER_HOST` 环境变量或 `docker.environment.DOCKER_HOST` 属性在 URL 中包含协议（例如， `ssh://myuser@mymachine` 或 `tcp://1.2.3.4` ）。

> **Note:** Keep in mind that your `docker.environment.DOCKER_HOST` attribute will override your Docker context and the `DOCKER_HOST` environment variable will override both the `docker.environment.DOCKER_HOST` attribute and your Docker context.
>
> ​​	注意：请记住，您的 `docker.environment.DOCKER_HOST` 属性将覆盖您的 Docker 上下文，而 `DOCKER_HOST` 环境变量将同时覆盖 `docker.environment.DOCKER_HOST` 属性和您的 Docker 上下文。

> **Tip**: In Powershell you can change your Docker environment variable with `$ENV:DOCKER_HOST = 'ssh://username@1.2.3.4'`
>
> ​​	提示：在 Powershell 中，您可以使用 `$ENV:DOCKER_HOST = 'ssh://username@1.2.3.4'` 更改 Docker 环境变量

## [Questions and feedback 问题和反馈](https://code.visualstudio.com/docs/containers/troubleshooting#_questions-and-feedback)

We love your feedback! If you have any ideas or suggestions, [report an issue](https://github.com/microsoft/vscode-docker/issues/new).

​​	我们非常欢迎您的反馈！如果您有任何想法或建议，请报告问题。
