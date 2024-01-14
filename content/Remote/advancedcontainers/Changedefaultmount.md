+++
title = "Change default mount"
date = 2024-01-13T13:53:43+08:00
weight = 50
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/change-default-source-mount](https://code.visualstudio.com/remote/advancedcontainers/change-default-source-mount)

# Change the default source code mount 更改默认源代码挂载



If you add the `image` or `dockerFile` properties to `devcontainer.json`, VS Code will automatically "bind" mount your current workspace folder into the container. If `git` is present on the host's `PATH` and the folder containing `.devcontainer/devcontainer.json` is within a `git` repository, the current workspace mounted will be the root of the repository. If `git` is not present on the host's `PATH`, the current workspace mounted will be the folder containing `.devcontainer/devcontainer.json`.

​​	如果向 `devcontainer.json` 添加 `image` 或 `dockerFile` 属性，VS Code 会自动将当前工作区文件夹“绑定”挂载到容器中。如果 `git` 存在于主机的 `PATH` 中，并且包含 `.devcontainer/devcontainer.json` 的文件夹位于 `git` 存储库中，则当前挂载的工作区将是存储库的根目录。如果 `git` 不存在于主机的 `PATH` 中，则当前挂载的工作区将是包含 `.devcontainer/devcontainer.json` 的文件夹。

While this is convenient, you may want to change [mount settings](https://docs.docker.com/engine/reference/commandline/service_create/#add-bind-mounts-volumes-or-memory-filesystems), alter the type of mount, location, or [run in a remote dev container]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost" >}}).

​​	虽然这很方便，但您可能需要更改挂载设置、更改挂载类型、位置或在远程开发容器中运行。

You can use the `workspaceMount` property in `devcontainer.json` to change the automatic mounting behavior. It expects the same value as the [Docker CLI `--mount` flag](https://docs.docker.com/engine/reference/commandline/run/#add-bind-mounts-or-volumes-using-the---mount-flag).

​​	您可以在 `devcontainer.json` 中使用 `workspaceMount` 属性来更改自动挂载行为。它期望的值与 Docker CLI `--mount` 标志相同。

For example:

​​	例如：

```
"workspaceMount": "source=${localWorkspaceFolder}/sub-folder,target=/workspace,type=bind",
"workspaceFolder": "/workspace"
```

This also allows you to do something like a named volume mount instead of a bind mount, which can be useful particularly when [using a remote Docker Host]({{< ref "/Remote/advancedcontainers/DeveloponaremoteDockerhost" >}}) or you [want to store your entire source tree in a volume]({{< ref "/Remote/advancedcontainers/Improveperformance#_use-a-named-volume-for-your-entire-source-tree" >}}).

​​	这也允许您执行类似于命名卷挂载而不是绑定挂载的操作，这在使用远程 Docker 主机或您想将整个源树存储在卷中时特别有用。

If you've already built the container and connected to it, run **Dev Containers: Rebuild Container** from the Command Palette (F1) to pick up the change. Otherwise run **Dev Containers: Open Folder in Container...** to connect to the container.

​​	如果您已经构建了容器并连接到它，请从命令面板（F1）运行 Dev Containers：重新构建容器以获取更改。否则，运行 Dev Containers：在容器中打开文件夹... 以连接到容器。

### [Video : Work with Monorepos in a dev container by changing default mount 视频：通过更改默认挂载在开发容器中使用单一存储库]({{< ref "/Remote/advancedcontainers/Changedefaultmount#_video-work-with-monorepos-in-a-dev-container-by-changing-default-mount" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/o5coAL7oE0o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>







### [Video : Change the default location of your project in a container 视频：更改项目在容器中的默认位置]({{< ref "/Remote/advancedcontainers/Changedefaultmount#_video-change-the-default-location-of-your-project-in-a-container" >}})

<iframe width="560" height="315" src="https://www.youtube.com/embed/4zX2XWTmr3c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; width: 616.662px; max-width: 100%; height: 400px; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>

