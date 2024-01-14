+++
title = "Start processes"
date = 2024-01-13T13:53:43+08:00
weight = 20
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/start-processes](https://code.visualstudio.com/remote/advancedcontainers/start-processes)

# Start a process when the container starts 容器启动时启动进程



When you are working in a development container, you may want to execute a command or start something each time the container starts. The easiest way to do this is using the `postStartCommand` property in `devcontainer.json`. For example, if you wanted to run `yarn install` every time you connected to the container to keep dependencies up to date, you could add the following:

​​	当您在开发容器中工作时，您可能希望在每次容器启动时执行一个命令或启动某些内容。最简单的方法是使用 `postStartCommand` 属性在 `devcontainer.json` 中。例如，如果您想在每次连接到容器时运行 `yarn install` 以保持依赖项是最新的，您可以添加以下内容：

```
"postStartCommand": "yarn install"
```

### [Video: Run npm install when a container is created 视频：在创建容器时运行 npm install]({{< ref "/Remote/advancedcontainers/Startprocesses#_video-run-npm-install-when-a-container-is-created" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/9qRy_kxVCK8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>







In other cases, you may want to start up a process and leave it running. This can be accomplished by using `nohup` and putting the process into the background using `&`. For example:

​​	在其他情况下，您可能希望启动一个进程并使其保持运行。这可以通过使用 `nohup` 并使用 `&` 将进程置于后台来实现。例如：

```
"postStartCommand": "nohup bash -c 'your-command-here &'"
```

### [Video: Run 'npm start' whenever the container is started 视频：每当容器启动时运行“npm start”]({{< ref "/Remote/advancedcontainers/Startprocesses#_video-run-npm-start-whenever-the-container-is-started" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/zFzPnWgBx_I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>







Those familiar with Linux may expect to be able to use the `systemctl` command to start and stop background services managed by something called `systemd`. Unfortunately, `systemd` has overhead and is generally not used in containers as a result.

​​	熟悉 Linux 的人可能希望能够使用 `systemctl` 命令来启动和停止由称为 `systemd` 的内容管理的后台服务。不幸的是， `systemd` 有开销，因此通常不会在容器中使用它。

In many cases, there is a command you can run instead (for example, `sshd`). And on Debian/Ubuntu, there are often scripts under `/etc/init.d` that you can run directly.

​​	在许多情况下，您可以运行一个命令来代替（例如， `sshd` ）。在 Debian/Ubuntu 上，通常在 `/etc/init.d` 下有您可以直接运行的脚本。

```
"postStartCommand": "/etc/init.d/ssh start"
```

These systems also include a `service` command that will use `systemctl` or `/etc/init.d` scripts based on what is installed.

​​	这些系统还包括一个 `service` 命令，它将根据已安装的内容使用 `systemctl` 或 `/etc/init.d` 脚本。

```
"postStartCommand": "service ssh start"
```

### [Video: Start SSH service in a container 视频：在容器中启动 SSH 服务]({{< ref "/Remote/advancedcontainers/Startprocesses#_video-start-ssh-service-in-a-container" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/KuSNpZgDYDs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>



## [Adding startup commands to the Docker image instead 相反，将启动命令添加到 Docker 镜像]({{< ref "/Remote/advancedcontainers/Startprocesses#_adding-startup-commands-to-the-docker-image-instead" >}})

While `postStartCommand` is convenient and allows you to execute commands in your source tree, you can also add these steps instead to a Dockerfile using a custom [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) or [CMD](https://docs.docker.com/engine/reference/builder/#cmd).

​​	虽然 `postStartCommand` 很方便，允许您在源树中执行命令，但您也可以使用自定义 ENTRYPOINT 或 CMD 将这些步骤添加到 Dockerfile 中。

When referencing a Dockerfile in `devcontainer.json`, the default entrypoint and command is overridden. First, disable this behavior using the `overrideCommand` property.

​​	在 `devcontainer.json` 中引用 Dockerfile 时，默认入口点和命令会被覆盖。首先，使用 `overrideCommand` 属性禁用此行为。

```
"overrideCommand": false
```

The `overrideCommand` property defaults to `true` because many images will immediately exit if a command is not specified. Instead, we will need to handle this in our Dockerfile.

​​	 `overrideCommand` 属性默认为 `true` ，因为如果未指定命令，许多镜像会立即退出。相反，我们需要在 Dockerfile 中处理此问题。

Next, consider this Dockerfile:

​​	接下来，考虑此 Dockerfile：

```
FROM mcr.microsoft.com/devcontainers/base:1-ubuntu

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT [ "/docker-entrypoint.sh" ]
CMD [ "sleep", "infinity" ]
```

The `CMD` here makes sure the container stays running by default. Keeping your startup steps in the `ENTRYPOINT` allows you to safely override the command when using `docker run` with your image or using Docker Compose. This resolves to the following:

​​	这里的 `CMD` 确保容器默认保持运行状态。将启动步骤保留在 `ENTRYPOINT` 中允许您在使用 `docker run` 与您的镜像或使用 Docker Compose 时安全地覆盖命令。这解析为以下内容：

```
/docker-entrypoint.sh sleep infinity
```

Next, create a `docker-entrypoint.sh` script:

​​	接下来，创建一个 `docker-entrypoint.sh` 脚本：

```
#!/usr/bin/env bash

echo "Hello from our entrypoint!"

exec "$@"
```

Anything you execute in this file will then fire each time the container starts. However, it's important to include the last `exec "$@"` line since this is what will cause the command `sleep infinity` in our example to fire.

​​	您在此文件中执行的任何操作都将在每次容器启动时触发。但是，包含最后一个 `exec "$@"` 行很重要，因为这是导致我们示例中的命令 `sleep infinity` 触发的操作。

Finally, if you are using Docker Compose, be sure that neither the [entrypoint](https://docs.docker.com/compose/compose-file/compose-file-v3/#entrypoint) nor [command](https://docs.docker.com/compose/compose-file/compose-file-v3/#command) properties are set for your container.

​​	最后，如果您正在使用 Docker Compose，请确保未为容器设置 entrypoint 或 command 属性。
