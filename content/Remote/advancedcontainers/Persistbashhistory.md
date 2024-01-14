+++
title = "Persist bash history"
date = 2024-01-13T13:53:43+08:00
weight = 40
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/persist-bash-history](https://code.visualstudio.com/remote/advancedcontainers/persist-bash-history)

# Persist bash history 保留 bash 历史记录



You can also use a mount to persist your `bash` command history across sessions / container rebuilds.

​​	您还可以使用挂载来使您的 `bash` 命令历史记录在会话/容器重建之间保持持久性。

First, update your `Dockerfile` so that each time a command is used in `bash`, the history is updated and stored in a location we will persist.

​​	首先，更新您的 `Dockerfile` ，以便每次在 `bash` 中使用命令时，都会更新历史记录并将其存储在我们持久保存的位置。

If you have a root user, update your `Dockerfile` with the following:

​​	如果您有 root 用户，请使用以下内容更新您的 `Dockerfile` ：

```
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && echo "$SNIPPET" >> "/root/.bashrc"
```

If you have a non-root user, update your `Dockerfile` with the following. Replace `user-name-goes-here` with the name of a [non-root user]({{< ref "/Remote/advancedcontainers/Addnon-rootuser" >}}) in the container.

​​	如果您有非 root 用户，请使用以下内容更新您的 `Dockerfile` 。将 `user-name-goes-here` 替换为容器中非 root 用户的名称。

```
ARG USERNAME=user-name-goes-here

RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && mkdir /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown -R $USERNAME /commandhistory \
    && echo "$SNIPPET" >> "/home/$USERNAME/.bashrc"
```

Next, add a local volume to store the command history. This step varies depending on whether or not you are using Docker Compose.

​​	接下来，添加一个本地卷来存储命令历史记录。此步骤会根据您是否使用 Docker Compose 而有所不同。

- **Dockerfile or image**: Use the `mounts` property (VS Code 1.41+) in your `devcontainer.json` file.

  ​​	Dockerfile 或映像：在您的 `devcontainer.json` 文件中使用 `mounts` 属性（VS Code 1.41+）。

  ```
    "mounts": [
        "source=projectname-bashhistory,target=/commandhistory,type=volume"
    ]
  ```

- **Docker Compose:** Update (or [extend]({{< ref "/DevContainers/CreateaDevContainer#_extend-your-docker-compose-file-for-development" >}})) your `docker-compose.yml` with the following for the appropriate service.

  ​​	Docker Compose：使用以下内容为相应服务更新（或扩展）您的 `docker-compose.yml` 。

  ```
  version: '3'
  services:
    your-service-name-here:
      volumes:
        - projectname-bashhistory:/commandhistory
       # ...
  volumes:
    projectname-bashhistory:
  ```

Finally, if you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	最后，如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers: Rebuild Container 来获取更改。否则，运行 Dev Containers: Open Folder in Container... 来连接到容器。

### [Video: How to make your bash history persist in a dev container 视频：如何在开发容器中使您的 bash 历史记录保持持久性]({{< ref "/Remote/advancedcontainers/Persistbashhistory#_video-how-to-make-your-bash-history-persist-in-a-dev-container" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/12nZz-TjoZg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

