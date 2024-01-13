+++
title = "Debug"
date = 2024-01-12T22:36:24+08:00
weight = 40
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/containers/debug-common](https://code.visualstudio.com/docs/containers/debug-common)

# Debug containerized apps 调试容器化应用程序



The Docker extension provides more support for debugging applications within Docker containers, such as scaffolding `launch.json` configurations for attaching a debugger to applications running within a container.

​​	Docker 扩展为 Docker 容器中的调试应用程序提供了更多支持，例如用于将调试器附加到容器中运行的应用程序的脚手架 `launch.json` 配置。

The Docker extension provides a `docker` debug configuration provider that manages how VS Code will launch an application and/or attach a debugger to the application in a running Docker container. This provider is configured via entries within `launch.json`, with configuration being specific to each application platform supported by the provider.

​​	Docker 扩展提供了一个 `docker` 调试配置提供程序，该提供程序管理 VS Code 将如何启动应用程序和/或将调试器附加到正在运行的 Docker 容器中的应用程序。此提供程序通过 `launch.json` 中的条目进行配置，配置特定于提供程序支持的每个应用程序平台。

The Docker extension currently supports debugging [Node.js](https://code.visualstudio.com/docs/containers/debug-common#_nodejs), [Python](https://code.visualstudio.com/docs/containers/debug-common#_python), and [.NET](https://code.visualstudio.com/docs/containers/debug-common#_net) applications within Docker containers.

​​	Docker 扩展目前支持在 Docker 容器中调试 Node.js、Python 和 .NET 应用程序。

## [Requirements 要求](https://code.visualstudio.com/docs/containers/debug-common#_requirements)

Scaffolding or pasting a launch configuration into `launch.json` is **not sufficient** to build and debug a Docker container. To successfully run a Docker launch configuration, you must have:

​​	将启动配置粘贴或添加到 `launch.json` 中不足以构建和调试 Docker 容器。若要成功运行 Docker 启动配置，您必须具有：

- A Dockerfile.
  Dockerfile。
- `docker-build` and `docker-run` tasks in `tasks.json`.
  `docker-build` 和 `docker-run` 任务在 `tasks.json` 中。
- A launch configuration that invokes these tasks.
  调用这些任务的启动配置。

We recommend using the **Docker: Add Docker Files to Workspace...** command to create these items, if none of these assets already exist. If you already have a functional Dockerfile, we recommend using the **Docker: Initialize for Docker debugging** command to scaffold a launch configuration and Docker-related tasks.

​​	如果这些资产尚不存在，我们建议使用 Docker：将 Docker 文件添加到工作区... 命令来创建这些项目。如果您已经拥有一个可用的 Dockerfile，我们建议使用 Docker：初始化 Docker 调试命令来构建启动配置和与 Docker 相关的任务。

## [Node.js](https://code.visualstudio.com/docs/containers/debug-common#_nodejs)

More information about debugging Node.js applications within Docker containers can be found at [Debug Node.js within a container](https://code.visualstudio.com/docs/containers/debug-node).

​​	有关在 Docker 容器中调试 Node.js 应用程序的更多信息，请参阅在容器中调试 Node.js。

Example `launch.json` configuration for debugging a Node.js application:

​​	示例 `launch.json` 配置，用于调试 Node.js 应用程序：

```
{
  "configurations": [
    {
      "name": "Docker Node.js Launch",
      "type": "docker",
      "request": "launch",
      "preLaunchTask": "docker-run: debug",
      "platform": "node"
    }
  ]
}
```

## [Python](https://code.visualstudio.com/docs/containers/debug-common#_python)

More information about debugging Python applications within Docker containers can be found at [Debug Python within a container](https://code.visualstudio.com/docs/containers/debug-python).

​​	有关在 Docker 容器中调试 Python 应用程序的更多信息，请参阅在容器中调试 Python。

Example `launch.json` configuration for debugging a Python application:

​​	示例 `launch.json` 配置，用于调试 Python 应用程序：

```
{
  "configurations": [
    {
      "name": "Docker: Python - Django",
      "type": "docker",
      "request": "launch",
      "preLaunchTask": "docker-run: debug",
      "python": {
        "pathMappings": [
          {
            "localRoot": "${workspaceFolder}",
            "remoteRoot": "/app"
          }
        ],
        "projectType": "django"
      }
    }
  ]
}
```

## [.NET](https://code.visualstudio.com/docs/containers/debug-common#_net)

You can choose between two ways of building and debugging your project within Docker containers:

​​	您可以在 Docker 容器中构建和调试项目的两种方式之间进行选择：

- **With .NET SDK**: If you are familiar with `MSBuild` or want to containerize your project without a Dockerfile, this is the recommended choice.

  ​​	使用 .NET SDK：如果您熟悉 `MSBuild` 或想在没有 Dockerfile 的情况下将项目容器化，这是推荐的选择。

  > **Note**: This option is only available for .NET SDK 7 and above and uses the `dotnet publish` command to build the image.
  >
  > ​​	注意：此选项仅适用于 .NET SDK 7 及更高版本，并使用 `dotnet publish` 命令来构建映像。

- **With a Dockerfile**: If you prefer customizing your project with a `Dockerfile`, choose this option.

  ​​	使用 Dockerfile：如果您更喜欢使用 `Dockerfile` 自定义项目，请选择此选项。

For more details about these two options, refer to [Debug .NET within Docker containers](https://code.visualstudio.com/docs/containers/debug-netcore).

​​	有关这两个选项的更多详细信息，请参阅在 Docker 容器中调试 .NET。

Example `launch.json` configuration for debugging a .NET application using `Dockerfile`:

​​	使用 `Dockerfile` 调试 .NET 应用程序的示例 `launch.json` 配置：

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch .NET Core in Docker",
      "type": "docker",
      "request": "launch",
      "preLaunchTask": "Run Docker Container",
      "netCore": {
        "appProject": "${workspaceFolder}/project.csproj"
      }
    }
  ]
}
```

## [Configuration reference 配置参考](https://code.visualstudio.com/docs/containers/debug-common#_configuration-reference)

| Property 属性               | Description 说明                                             |
| :-------------------------- | :----------------------------------------------------------- |
| `containerName`             | Name of the container used for debugging. 用于调试的容器的名称。 |
| `dockerServerReadyAction`   | Options for launching a browser to the Docker container. Similar to serverReadyAction, but replaces container ports with host ports. 用于向 Docker 容器启动浏览器的选项。类似于 serverReadyAction，但用主机端口替换容器端口。 |
| `removeContainerAfterDebug` | Whether to remove the debug container after debugging. 是否在调试后删除调试容器。 |
| `platform`                  | The target platform for the application. Can be `netCore` or `node`. 应用程序的目标平台。可以是 `netCore` 或 `node` 。 |
| `netCore`                   | Options for debugging .NET projects in Docker. 在 Docker 中调试 .NET 项目的选项。 |
| `node`                      | Options for debugging Node.js projects in Docker. 在 Docker 中调试 Node.js 项目的选项。 |
| `python`                    | Options for debugging Python projects in Docker. 在 Docker 中调试 Python 项目的选项。 |

### [dockerServerReadyAction object properties dockerServerReadyAction 对象属性](https://code.visualstudio.com/docs/containers/debug-common#_dockerserverreadyaction-object-properties)

| Property 属性   | Description 说明                                             |
| :-------------- | :----------------------------------------------------------- |
| `action`        | The action to take when the pattern is found. Can be `debugWithChrome` or `openExternally`. 在找到模式时要执行的操作。可以是 `debugWithChrome` 或 `openExternally` 。 |
| `containerName` | The container name to match the host port. 与主机端口匹配的容器名称。 |
| `pattern`       | The regex pattern to look for in Debug console output. 在调试控制台输出中要查找的正则表达式模式。 |
| `uriFormat`     | The URI format to launch. 要启动的 URI 格式。                |
| `webRoot`       | The root folder from which web pages are served. Used only when `action` is set to `debugWithChrome`. 提供网页的根文件夹。仅在将 `action` 设置为 `debugWithChrome` 时使用。 |

### [node object properties node 对象属性](https://code.visualstudio.com/docs/containers/debug-common#_node-object-properties)

> These properties are the same as those described in the [VS Code documentation](https://code.visualstudio.com/docs/nodejs/nodejs-debugging#_launch-configuration-attributes) for attaching a debugger to Node.js applications. All properties passed in the `node` object will be passed on to the Node.js debug adaptor, even if not specifically listed below.
>
> ​​	这些属性与 VS Code 文档中用于将调试器附加到 Node.js 应用程序的属性相同。在 `node` 对象中传递的所有属性都将传递给 Node.js 调试适配器，即使下面没有专门列出。

| Property 属性              | Description 说明                                             | Default 默认                                |
| :------------------------- | :----------------------------------------------------------- | :------------------------------------------ |
| `port`                     | Optional. The debug port to use. 可选。要使用的调试端口。    | `9229`                                      |
| `address`                  | Optional. TCP/IP address of the debug port. 可选。调试端口的 TCP/IP 地址。 |                                             |
| `sourceMaps`               | Optional. Enable source maps by setting this to `true`. 可选。通过将此项设置为 `true` 来启用源映射。 |                                             |
| `outFiles`                 | Optional. Array of glob patterns for locating generated JavaScript files. 可选。用于查找生成的 JavaScript 文件的 glob 模式数组。 |                                             |
| `autoAttachChildProcesses` | Optional. Track all subprocesses of debuggee and automatically attach to those that are launched in debug mode. 可选。跟踪调试程序的所有子进程，并自动附加到以调试模式启动的子进程。 |                                             |
| `timeout`                  | Optional. When restarting a session, give up after this number of milliseconds. 可选。重新启动会话时，在此毫秒数后放弃。 |                                             |
| `stopOnEntry`              | Optional. Break immediately when the program launches. 可选。程序启动时立即中断。 |                                             |
| `localRoot`                | Optional. VS Code's root directory. 可选。VS Code 的根目录。 | The root workspace folder. 根工作区文件夹。 |
| `remoteRoot`               | Optional. Node's root directory within the Docker container. 可选。Docker 容器中的 Node 根目录。 | `/usr/src/app`                              |
| `smartStep`                | Optional. Try to automatically step over code that doesn't map to source files. 可选。尝试自动跳过未映射到源文件的代码。 |                                             |
| `skipFiles`                | Optional. Automatically skip files covered by these glob patterns. 可选。自动跳过这些 glob 模式涵盖的文件。 |                                             |
| `trace`                    | Optional. Enable diagnostic output. 可选。启用诊断输出。     |                                             |

### [python object properties python 对象属性](https://code.visualstudio.com/docs/containers/debug-common#_python-object-properties)

| Property 属性  | Description 说明                                             | Default 默认 |
| :------------- | :----------------------------------------------------------- | :----------- |
| `host`         | The host for remote debugging. 远程调试的主机。              |              |
| `port`         | The port for remote debugging. 远程调试的端口。              | `5678`       |
| `pathMappings` | Maps the project path between local machine and remote host. 在本地计算机和远程主机之间映射项目路径。 |              |
| `projectType`  | The type of your Python project, `flask` for Flask projects, `django` for Django, `fastapi` for FastAPI, and general for others. The project type will be used to set the port and commands used for debugging. Python 项目的类型，Flask 项目为 `flask` ，Django 为 `django` ，FastAPI 为 `fastapi` ，其他为通用。项目类型将用于设置用于调试的端口和命令。 |              |
| `justMyCode`   | Debug only user-written code. 仅调试用户编写的代码。         |              |
| `django`       | Django debugging. Django 调试。                              | `false`      |
| `jinja`        | Jinja template debugging (such as Flask). Jinja 模板调试（例如 Flask）。 | `false`      |

### [netCore object properties netCore 对象属性](https://code.visualstudio.com/docs/containers/debug-common#_netcore-object-properties)

> Properties passed in the `netCore` object are generally passed on to the .NET debug adaptor, even if not specifically listed below. The complete list of debugger properties is in the [OmniSharp VS Code extension documentation](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger-launchjson.md).
>
> ​​	传递给 `netCore` 对象的属性通常会传递给 .NET 调试适配器，即使下面没有专门列出。调试器属性的完整列表位于 OmniSharp VS Code 扩展文档中。

| Property 属性 | Description 说明                                             |
| :------------ | :----------------------------------------------------------- |
| `appProject`  | The .NET project (.csproj, .fsproj, etc.) to debug. .NET 项目（.csproj、.fsproj 等）进行调试。 |

## [Next steps 后续步骤](https://code.visualstudio.com/docs/containers/debug-common#_next-steps)

Read on to learn more about:

​​	继续阅读以了解有关以下内容的更多信息：

- [Debugging Node.js within Docker containers
  在 Docker 容器中调试 Node.js](https://code.visualstudio.com/docs/containers/debug-node)
- [Debugging Python within Docker containers
  在 Docker 容器中调试 Python](https://code.visualstudio.com/docs/containers/debug-python)
- [Debugging .NET within Docker containers
  在 Docker 容器中调试 .NET](https://code.visualstudio.com/docs/containers/debug-netcore)
- [Debugging with Docker Compose
  使用 Docker Compose 进行调试](https://code.visualstudio.com/docs/containers/docker-compose#_debug)
- [Troubleshooting
  故障排除](https://code.visualstudio.com/docs/containers/troubleshooting)
