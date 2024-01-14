+++
title = "Customize"
date = 2024-01-12T22:36:24+08:00
weight = 90
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/containers/reference](https://code.visualstudio.com/docs/containers/reference)

# Customize the Docker extension 自定义 Docker 扩展



The Docker extension includes several Visual Studio Code tasks to control the behavior of Docker [build]({{< ref "/Docker/Customize#_docker-build-task" >}}) and [run]({{< ref "/Docker/Customize#_docker-run-task" >}}), and form the basis of container startup for debugging.

​​	Docker 扩展包括几个 Visual Studio Code 任务，用于控制 Docker 构建和运行的行为，并形成用于调试的容器启动的基础。

The tasks allow for a great deal of control and customization. The final configuration is a combination of general defaults, platform-specific defaults (such as Node.js, Python, or .NET), and user input. User input takes precedence when it conflicts with defaults.

​​	这些任务允许进行大量的控制和自定义。最终配置是常规默认值、特定于平台的默认值（例如 Node.js、Python 或 .NET）和用户输入的组合。当用户输入与默认值冲突时，用户输入优先。

All common features of Visual Studio Code tasks (for example, grouping tasks into compound tasks) are supported by Docker extension tasks. For more information on common task features and properties, see the Visual Studio Code [custom task]({{< ref "/UserGuide/Tasks#_custom-tasks" >}}) documentation.

​​	Docker 扩展任务支持 Visual Studio Code 任务的所有常见功能（例如，将任务分组到复合任务中）。有关常见任务功能和属性的详细信息，请参阅 Visual Studio Code 自定义任务文档。

## [Docker build task Docker 构建任务]({{< ref "/Docker/Customize#_docker-build-task" >}})

The `docker-build` task builds Docker images using the Docker command line (CLI). The task can be used by itself, or as part of a chain of tasks to run and/or debug an application within a Docker container.

​​	 `docker-build` 任务使用 Docker 命令行 (CLI) 构建 Docker 映像。该任务可以单独使用，也可以作为任务链的一部分，在 Docker 容器内运行和/或调试应用程序。

The most important configuration settings for the `docker-build` task are `dockerBuild` and `platform`:

​​	 `docker-build` 任务最重要的配置设置是 `dockerBuild` 和 `platform` ：

- The `dockerBuild` object specifies parameters for the Docker build command. Values specified by this object are applied directly to Docker build CLI invocation.
  `dockerBuild` 对象为 Docker 构建命令指定参数。由此对象指定的值直接应用于 Docker 构建 CLI 调用。
- The `platform` property is a hint that changes how the `docker-build` task determines Docker build defaults.
  属性 `platform` 是一个提示，它会更改 `docker-build` 任务确定 Docker 构建默认值的方式。

See [property reference]({{< ref "/Docker/Customize#_build-task-reference" >}}) for full list of all task properties.

​​	有关所有任务属性的完整列表，请参阅属性参考。

### [Platform support 平台支持]({{< ref "/Docker/Customize#_platform-support" >}})

While the `docker-build` task in `tasks.json` can be used to build any Docker image, the extension has explicit support (and simplified configuration) for Node.js, Python, and .NET Core.

​​	虽然 `tasks.json` 中的 `docker-build` 任务可用于构建任何 Docker 映像，但该扩展名对 Node.js、Python 和 .NET Core 提供了显式支持（以及简化的配置）。

### [Node.js (docker-build)]({{< ref "/Docker/Customize#_nodejs-dockerbuild" >}})

**Minimal configuration using defaults
使用默认值进行最小配置**

A Node.js based Docker image with no specific platform options can just set the `platform` property to `node`:

​​	一个没有特定平台选项的基于 Node.js 的 Docker 映像可以将 `platform` 属性设置为 `node` ：

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Build Node Image",
      "type": "docker-build",
      "platform": "node"
    }
  ]
}
```

**Platform defaults
平台默认值**

For Node.js Docker images, the `docker-build` task infers the following options:

​​	对于 Node.js Docker 映像， `docker-build` 任务会推断以下选项：

| Property 属性            | Inferred Value 推断值                                        |
| :----------------------- | :----------------------------------------------------------- |
| `dockerBuild.context`    | The same directory in which the `package.json` resides. 与 `package.json` 所在的同一目录。 |
| `dockerBuild.dockerfile` | The file `Dockerfile` in the same directory as the `package.json` resides. 与 `package.json` 所在的同一目录中的 `Dockerfile` 文件。 |
| `dockerBuild.tag`        | The application's `name` property in `package.json` (if defined), else the base name of the folder in which `package.json` resides. 应用程序在 `package.json` 中的 `name` 属性（如果已定义），否则为 `package.json` 所在文件夹的基本名称。 |

### [Python (docker-build)]({{< ref "/Docker/Customize#_python-dockerbuild" >}})

**Minimal configuration using defaults
使用默认值进行最小配置**

A Python based Docker image with no specific platform options can just set the `platform` property to `python`:

​​	没有特定平台选项的基于 Python 的 Docker 映像可以将 `platform` 属性设置为 `python` ：

```
{
  "tasks": [
    {
      "type": "docker-build",
      "label": "docker-build",
      "platform": "python"
    }
  ]
}
```

**Platform defaults
平台默认值**

For Python Docker images, the `docker-build` task infers the following options:

​​	对于 Python Docker 映像， `docker-build` 任务推断以下选项：

| Property 属性            | Inferred Value 推断值                                        |
| :----------------------- | :----------------------------------------------------------- |
| `dockerBuild.context`    | The default context is the workspace folder. 默认上下文是工作区文件夹。 |
| `dockerBuild.dockerfile` | The default `Dockerfile` path will be in the root of the workspace folder. 默认 `Dockerfile` 路径将位于工作区文件夹的根目录中。 |
| `dockerBuild.tag`        | The base name of the root workspace folder. 根工作区文件夹的基本名称。 |
| `dockerBuild.pull`       | Defaults to true in order to pull new base images before building. 在构建之前拉取新的基础映像时，默认为 true。 |

### [.NET (docker-build)]({{< ref "/Docker/Customize#_net-dockerbuild" >}})

**Minimal configuration using defaults
使用默认值进行最小配置**

When you build a .NET-based Docker image, you can omit the `platform` property and just set the `netCore` object (`platform` is implicitly set to `netcore` when `netCore` object is present). Note that `appProject` is a required property:

​​	在构建基于 .NET 的 Docker 映像时，您可以省略 `platform` 属性，只需设置 `netCore` 对象（当存在 `netCore` 对象时， `platform` 会隐式设置为 `netcore` ）。请注意， `appProject` 是必需属性：

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Build Node Image",
      "type": "docker-build",
      "netCore": {
        "appProject": "${workspaceFolder}/project.csproj"
      }
    }
  ]
}
```

**Platform defaults
平台默认值**

For .NET-based images, the `docker-build` task infers the following options:

​​	对于基于 .NET 的映像， `docker-build` 任务推断以下选项：

| Property 属性            | Inferred Value 推断值                                        |
| :----------------------- | :----------------------------------------------------------- |
| `dockerBuild.context`    | The root workspace folder. 根工作区文件夹。                  |
| `dockerBuild.dockerfile` | The file `Dockerfile` in the root workspace folder. 根工作区文件夹中的文件 `Dockerfile` 。 |
| `dockerBuild.tag`        | The base name of the root workspace folder. 根工作区文件夹的基本名称。 |

## [Build task reference 生成任务参考]({{< ref "/Docker/Customize#_build-task-reference" >}})

Here are all properties available for configuring `docker-build` task. All properties are optional unless indicated otherwise.

​​	以下是可用于配置 `docker-build` 任务的所有属性。除非另有说明，否则所有属性都是可选的。

| Property 属性 | Description 说明                                             |
| :------------ | :----------------------------------------------------------- |
| `dockerBuild` | Options for controlling the `docker build` command executed ([see below]({{< ref "/Docker/Customize#_dockerbuild-object-properties" >}})). 用于控制执行的 `docker build` 命令的选项（请参见下文）。 Required unless `platform` is set. 除非设置了 `platform` ，否则是必需的。 |
| `platform`    | Determines the platform: .NET (`netcore`) or Node.js (`node`) and default settings for `docker build` command. 确定平台：.NET ( `netcore` ) 或 Node.js ( `node` ) 以及 `docker build` 命令的默认设置。 |
| `node`        | Determines options specific for Node.js projects ([see below]({{< ref "/Docker/Customize#_node-object-properties-dockerbuild-task" >}})). 确定适用于 Node.js 项目的特定选项（请参见下文）。 |
| `python`      | There are no object properties for Python in the `docker-build` task. `docker-build` 任务中没有适用于 Python 的对象属性。 |
| `netCore`     | Determines options specific for .NET projects ([see below]({{< ref "/Docker/Customize#_netcore-object-properties-dockerbuild-task" >}})). 确定适用于 .NET 项目的特定选项（请参见下文）。 |

### [dockerBuild object properties dockerBuild 对象属性]({{< ref "/Docker/Customize#_dockerbuild-object-properties" >}})

| Property 属性   | Description 说明                                             | `docker build` CLI Equivalent `docker build` CLI 等效项 |
| :-------------- | :----------------------------------------------------------- | :------------------------------------------------------ |
| `context`       | The path to the Docker build context. Docker 构建上下文的路径。 Required, unless inferred from the platform. 必需，除非从平台推断出来。 | `PATH`                                                  |
| `dockerfile`    | The path to the Dockerfile. Dockerfile 的路径。 Required, unless inferred from the platform. 必需，除非从平台推断出来。 | `-f` or `--file` `-f` 或 `--file`                       |
| `tag`           | The tag applied to the Docker image. 应用于 Docker 映像的标签。 Required, unless inferred from the platform. 必需，除非从平台推断出来。 | `-t` or `--tag` `-t` 或 `--tag`                         |
| `buildArgs`     | Build arguments applied to the command line. This is a list of key-value pairs. 应用于命令行的构建参数。这是一个键值对列表。 | `--build-arg`                                           |
| `labels`        | Labels added to the Docker image. This is a list of key-value pairs (a JSON object). 添加到 Docker 映像的标签。这是一个键值对列表（JSON 对象）。 In addition to labels specified here, a label `com.microsoft.created-by`, set to `visual-studio-code` is added to the image. This behavior can be turned off by setting `includeDefaults` property of the `labels` object to false. 除了此处指定的标签外，还会将标签 `com.microsoft.created-by` （设置为 `visual-studio-code` ）添加到映像。可以通过将 `labels` 对象的 `includeDefaults` 属性设置为 false 来关闭此行为。 | `--label`                                               |
| `target`        | The target in the Dockerfile to build to. Dockerfile 中要构建到的目标。 | `--target`                                              |
| `pull`          | Whether or not to pull new base images before building. 在构建之前是否拉取新的基础映像。 | `--pull`                                                |
| `customOptions` | Any extra parameters to add before the context argument. No attempt is made to resolve conflicts with other options or validate this option. 在上下文参数之前添加的任何额外参数。不会尝试解决与其他选项的冲突或验证此选项。 | (any) （任何）                                          |

### [node object properties (docker-build task) 节点对象属性（docker-build 任务）]({{< ref "/Docker/Customize#_node-object-properties-dockerbuild-task" >}})

| Property 属性 | Description 说明                                             | Default 默认                                                 |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `package`     | The path to the `package.json` file associated with the Dockerfile and `docker-build` task. 与 Dockerfile 和 `docker-build` 任务关联的 `package.json` 文件的路径。 | The file `package.json` in the root workspace folder. 根工作区文件夹中的 `package.json` 文件。 |

### [netCore object properties (docker-build task) netCore 对象属性（docker-build 任务）]({{< ref "/Docker/Customize#_netcore-object-properties-dockerbuild-task" >}})

| Property 属性 | Description 说明                                             |
| :------------ | :----------------------------------------------------------- |
| `appProject`  | The .NET project file (`.csproj`, `.fsproj`, etc.) associated with the Dockerfile and `docker-build` task. 与 Dockerfile 和 `docker-build` 任务关联的 .NET 项目文件 ( `.csproj` 、 `.fsproj` 等)。 Required always. 始终必需。 |

## [Docker run task Docker 运行任务]({{< ref "/Docker/Customize#_docker-run-task" >}})

The `docker-run` task in `tasks.json` creates and starts a Docker container using the Docker command line (CLI). The task can be used by itself, or as part of a chain of tasks to debug an application within a Docker container.

​​	 `docker-run` 中的 `tasks.json` 任务使用 Docker 命令行 (CLI) 创建并启动 Docker 容器。该任务可以单独使用，也可以作为任务链的一部分，以便在 Docker 容器内调试应用程序。

The most important configuration settings for the `docker-run` task are `dockerRun` and `platform`:

​​	 `docker-run` 任务最重要的配置设置是 `dockerRun` 和 `platform` ：

- The `dockerRun` object specifies parameters for the Docker run command. Values specified by this object are applied directly to Docker run CLI invocation.
  `dockerRun` 对象为 Docker run 命令指定参数。此对象指定的值直接应用于 Docker run CLI 调用。
- The `platform` property is a hint that changes how the `docker-run` task determines Docker run defaults.
  `platform` 属性是一个提示，它会改变 `docker-run` 任务确定 Docker run 默认值的方式。

See [property reference]({{< ref "/Docker/Customize#_run-task-reference" >}}) for full list of all task properties.

​​	有关所有任务属性的完整列表，请参阅属性参考。

### [Docker run platform support Docker 运行平台支持]({{< ref "/Docker/Customize#_docker-run-platform-support" >}})

While the `docker-run` task can be used to run any Docker image, the extension has explicit support (and simplified configuration) for Node.js, Python, and .NET.

​​	虽然 `docker-run` 任务可用于运行任何 Docker 映像，但该扩展名明确支持（且配置简化）Node.js、Python 和 .NET。

### [Node.js (docker-run)]({{< ref "/Docker/Customize#_nodejs-dockerrun" >}})

**Minimal configuration using defaults
使用默认值的最小配置**

A Node.js based Docker image with no specific platform options can just set the `platform` property to `node`.

​​	一个没有特定平台选项的基于 Node.js 的 Docker 镜像可以将 `platform` 属性设置为 `node` 。

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run Node Image",
      "node": "docker-run",
      "platform": "node"
    }
  ]
}
```

**Platform defaults
平台默认值**

For Node.js-based Docker images, the `docker-run` task infers the following options:

​​	对于基于 Node.js 的 Docker 镜像， `docker-run` 任务推断以下选项：

| Property 属性             | Inferred Value 推断值                                        |
| :------------------------ | :----------------------------------------------------------- |
| `dockerRun.command`       | Generated from the npm `start` script in the `package.json` (if it exists), else generated from the `main` property in the `package.json`. 从 `package.json` 中的 npm `start` 脚本生成（如果存在），否则从 `package.json` 中的 `main` 属性生成。 |
| `dockerRun.containerName` | Derived from the application package name. 从应用程序包名称派生。 |
| `dockerRun.image`         | The tag from a dependent `docker-build` task (if one exists) or derived from the application package name, itself derived from the `name` property within `package.json` or the base name of the folder in which it resides. 来自依赖 `docker-build` 任务的标签（如果存在）或从应用程序包名称派生，应用程序包名称本身派生自 `package.json` 中的 `name` 属性或其所在文件夹的基本名称。 |

### [Python (docker-run)]({{< ref "/Docker/Customize#_python-dockerrun" >}})

When building a Python-based Docker image, you can omit the `platform` property and just set the `python` object (`platform` is implicitly set to `python` when `python` object is present)

​​	在构建基于 Python 的 Docker 映像时，您可以省略 `platform` 属性，只需设置 `python` 对象（当 `python` 对象存在时， `platform` 会隐式设置为 `python` ）

**Minimal configuration for Django Apps
Django 应用的最小配置**

```
{
  "type": "docker-run",
  "label": "docker-run: debug",
  "dependsOn": ["docker-build"],
  "python": {
    "args": ["runserver", "0.0.0.0:8000", "--nothreading", "--noreload"],
    "file": "path_to/manage.py"
  }
}
```

**Minimal configuration for Flask Apps
Flask 应用的最小配置**

```
{
  "type": "docker-run",
  "label": "docker-run: debug",
  "dependsOn": ["docker-build"],
  "dockerRun": {
    "env": {
      "FLASK_APP": "path_to/flask_entry_point.py"
    }
  },
  "python": {
    "args": ["run", "--no-debugger", "--no-reload", "--host", "0.0.0.0", "--port", "5000"],
    "module": "flask"
  }
}
```

**Minimal configuration for General Apps
通用应用的最小配置**

```
{
  "type": "docker-run",
  "label": "docker-run: debug",
  "dependsOn": ["docker-build"],
  "python": {
    "file": "path_to/app_entry_point.py"
  }
}
```

**Platform defaults
平台默认值**

For Python-based Docker images, the `docker-run` task infers the following options:

​​	对于基于 Python 的 Docker 映像， `docker-run` 任务推断以下选项：

| Property 属性             | Inferred Value 推断值                                        |
| :------------------------ | :----------------------------------------------------------- |
| `dockerRun.command`       | Generated by the Python object and is called by the Python Debugger. 由 Python 对象生成，并由 Python 调试器调用。 |
| `dockerRun.containerName` | Derived from the base name of the root workspace folder. 派生自根工作区文件夹的基本名称。 |
| `dockerRun.image`         | The tag from a dependent docker-build task (if one exists) or derived from the base name of the root workspace folder. 来自相关 docker-build 任务的标签（如果存在）或派生自根工作区文件夹的基本名称。 |

### [.NET (docker-run)]({{< ref "/Docker/Customize#_net-dockerrun" >}})

**Minimal configuration using defaults
使用默认值的最小配置**

When building a .NET-based Docker image, you can omit the `platform` property and just set the `netCore` object (`platform` is implicitly set to `netcore` when `netCore` object is present). Note that `appProject` is a required property:

​​	在构建基于 .NET 的 Docker 映像时，您可以省略 `platform` 属性，而只设置 `netCore` 对象（当 `netCore` 对象存在时， `platform` 会隐式设置为 `netcore` ）。请注意， `appProject` 是一个必需的属性：

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run .NET Core Image",
      "type": "docker-run",
      "netCore": {
        "appProject": "${workspaceFolder}/project.csproj"
      }
    }
  ]
}
```

**Platform defaults
平台默认值**

For .NET-based images, the `docker-run` task infers the following options:

​​	对于基于 .NET 的映像， `docker-run` 任务会推断以下选项：

| Property 属性             | Inferred Value 推断值                                        |
| :------------------------ | :----------------------------------------------------------- |
| `dockerRun.containerName` | Derived from the base name of the root workspace folder. 派生自根工作区文件夹的基本名称。 |
| `dockerRun.env`           | Adds the following environment variables as required: `ASPNETCORE_ENVIRONMENT`, `ASPNETCORE_URLS`, and `DOTNET_USE_POLLING_FILE_WATCHER`. 根据需要添加以下环境变量： `ASPNETCORE_ENVIRONMENT` 、 `ASPNETCORE_URLS` 和 `DOTNET_USE_POLLING_FILE_WATCHER` 。 |
| `dockerRun.image`         | The tag from a dependent `docker-build` task (if one exists) or derived from the base name of the root workspace folder. 来自依赖 `docker-build` 任务的标记（如果存在）或派生自根工作区文件夹的基本名称。 |
| `dockerRun.os`            | `Linux`                                                      |
| `dockerRun.volumes`       | Adds the following volumes as required: the local application folder, the source folder, the debugger folder, the NuGet package folder, and NuGet fallback folder. 根据需要添加以下卷：本地应用程序文件夹、源文件夹、调试器文件夹、NuGet 包文件夹和 NuGet 回退文件夹。 |

## [Run task reference 运行任务参考]({{< ref "/Docker/Customize#_run-task-reference" >}})

Here are all properties available for configuring `docker-run` task. All properties are optional unless indicated otherwise.

​​	此处列出了可用于配置 `docker-run` 任务的所有属性。除非另有说明，否则所有属性都是可选的。

| Property 属性 | Description 说明                                             |
| :------------ | :----------------------------------------------------------- |
| `dockerRun`   | Options for controlling the `docker run` command executed ([see below]({{< ref "/Docker/Customize#_dockerrun-object-properties" >}})). 用于控制执行的 `docker run` 命令的选项（请参见下文）。 Required unless `platform` is set. 除非设置了 `platform` ，否则为必需。 |
| `platform`    | Determines the platform: .NET (`netcore`) or Node.js (`node`) and default settings for `docker run` command. 确定平台：.NET ( `netcore` ) 或 Node.js ( `node` ) 以及 `docker run` 命令的默认设置。 |
| `node`        | For Node.js projects, this controls various options ([see below]({{< ref "/Docker/Customize#_node-object-properties-dockerrun-task" >}})). 对于 Node.js 项目，此选项控制各种选项（请参见下文）。 |
| `python`      | For Python projects, this controls various options ([see below]({{< ref "/Docker/Customize#_python-object-properties-dockerrun-task" >}})). 对于 Python 项目，此选项控制各种选项（请参见下文）。 |
| `netCore`     | For .NET projects, this controls various options ([see below]({{< ref "/Docker/Customize#_netcore-object-properties-dockerrun-task" >}})). 对于 .NET 项目，此选项控制各种选项（请参见下文）。 |

### [dockerRun object properties dockerRun 对象属性]({{< ref "/Docker/Customize#_dockerrun-object-properties" >}})

| Property 属性     | Description 说明                                             | CLI Equivalent CLI 等效项               |
| :---------------- | :----------------------------------------------------------- | :-------------------------------------- |
| `image`           | The name (tag) of the image to run. 要运行的镜像的名称（标签）。 Required unless inferred from the platform. 必需，除非从平台推断出来。 | `IMAGE`                                 |
| `command`         | The command to run upon starting the container. 容器启动时要运行的命令。 Required, unless inferred from the platform. 必需，除非从平台推断出来。 | `COMMAND [ARG...]`                      |
| `containerName`   | The name given to the started container. 启动的容器的名称。 Required, unless inferred from the platform. 必需，除非从平台推断出来。 | `--name`                                |
| `env`             | Environment variables set in the container. This is a list of key-value pairs. 在容器中设置的环境变量。这是一个键值对列表。 | `-e` or `--env` `-e` 或 `--env`         |
| `envFiles`        | This is a list of `.env` files. 这是一个 `.env` 文件列表。   | `--env-file`                            |
| `labels`          | Labels given to the started container. This is a list of key-value pairs. 启动的容器的标签。这是一个键值对列表。 | `--label`                               |
| `network`         | The name of the network to which the container will be connected. 容器将连接到的网络的名称。 | `--network`                             |
| `networkAlias`    | The network-scoped alias for the started container. 已启动容器的网络范围别名。 | `--network-alias`                       |
| `os`              | Default is `Linux`, the other option is `Windows`. The container operating system used. 默认值为 `Linux` ，另一个选项是 `Windows` 。容器操作系统已使用。 | N/A                                     |
| `ports`           | The ports to publish (map) from container to host. This is a list of objects ([see below]({{< ref "/Docker/Customize#_ports-object-properties" >}})). 从容器发布（映射）到主机的端口。这是一个对象列表（见下文）。 | `-p` or `--publish` `-p` 或 `--publish` |
| `portsPublishAll` | Whether to publish all ports exposed by the Docker image. Defaults to `true` if no ports are explicitly published. 是否发布 Docker 镜像公开的所有端口。如果未明确发布任何端口，则默认为 `true` 。 | `-P`                                    |
| `extraHosts`      | The hosts to add to the container for DNS resolution. This is a list of objects ([see below]({{< ref "/Docker/Customize#_extrahosts-object-properties" >}})). 要添加到容器中以进行 DNS 解析的主机。这是一个对象列表（见下文）。 | `--add-host`                            |
| `volumes`         | The volumes to map into the started container. This is a list of objects ([see below]({{< ref "/Docker/Customize#_volumes-object-properties" >}})). 要映射到已启动容器的卷。这是一个对象列表（见下文）。 | `-v` or `--volume` `-v` 或 `--volume`   |
| `remove`          | Whether or not to remove the container after it stops. 容器停止后是否将其删除。 | `--rm`                                  |
| `customOptions`   | Any extra parameters to add before the image argument. No attempt is made to resolve conflicts with other options or validate this option. 在图像参数之前添加任何额外的参数。不会尝试解决与其他选项的冲突或验证此选项。 | (any)                                   |

### [ports object properties 端口对象属性]({{< ref "/Docker/Customize#_ports-object-properties" >}})

| Property 属性   | Description 说明                                             | Default 默认                                       |
| :-------------- | :----------------------------------------------------------- | :------------------------------------------------- |
| `containerPort` | The port number bound on the container. 绑定到容器上的端口号。 Required. 必需。 |                                                    |
| `hostPort`      | The port number bound on the host. 绑定到主机上的端口号。    | (randomly selected by Docker) (由 Docker 随机选择) |
| `protocol`      | The protocol for the binding (`tcp` or `udp`). 绑定协议 ( `tcp` 或 `udp` )。 | `tcp`                                              |

### [extraHosts object properties extraHosts 对象属性]({{< ref "/Docker/Customize#_extrahosts-object-properties" >}})

| Property 属性 | Description 说明                                             |
| :------------ | :----------------------------------------------------------- |
| `hostname`    | The hostname for DNS resolution. 用于 DNS 解析的主机名。 Required. 必填。 |
| `ip`          | The IP address associated with the above hostname. 与上述主机名关联的 IP 地址。 Required. 必填。 |

### [volumes object properties volumes 对象属性]({{< ref "/Docker/Customize#_volumes-object-properties" >}})

| Property 属性   | Description 说明                                             | Default 默认                    |
| :-------------- | :----------------------------------------------------------- | :------------------------------ |
| `localPath`     | The path on the local machine that will be mapped. 将在本地计算机上映射的路径。 Required. 必填。 |                                 |
| `containerPath` | The path in the container to which the local path will be mapped. 将本地路径映射到的容器中的路径。 Required. 必填。 |                                 |
| `permissions`   | Permissions the container has on the mapped path. Can be `ro` (read-only) or `rw` (read-write). 容器对映射路径的权限。可以是 `ro` （只读）或 `rw` （读写）。 | Container dependent. 容器相关。 |

### [node object properties (docker-run task) node 对象属性（docker-run 任务）]({{< ref "/Docker/Customize#_node-object-properties-dockerrun-task" >}})

| Property 属性     | Description 说明                                             | Default 默认                                                 |
| :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `package`         | The path to the `package.json` file associated with the `docker-run` task. 与 `docker-run` 任务关联的 `package.json` 文件的路径。 | The file `package.json` in the root workspace folder. 根工作区文件夹中的 `package.json` 文件。 |
| `enableDebugging` | Whether or not to enable debugging within the container. 是否在容器内启用调试。 | `false`                                                      |
| `inspectMode`     | Defines the initial interaction between the application and the debugger (`default` or `break`). 定义应用程序与调试器之间的初始交互（ `default` 或 `break` ）。 The value `default` allows the application to run until the debugger attaches. 值 `default` 允许应用程序运行，直到调试器附加。 The value `break` prevents the application from running until the debugger attaches. 值 `break` 阻止应用程序运行，直到调试器附加。 | `default`                                                    |
| `inspectPort`     | The port on which debugging should occur. 应进行调试的端口。 | `9229`                                                       |

### [python object properties (docker-run task) python 对象属性（docker-run 任务）]({{< ref "/Docker/Customize#_python-object-properties-dockerrun-task" >}})

| Property 属性 | Description 说明                                             | Default 默认                                                 |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `args`        | Arguments passed to the Python app. 传递给 Python 应用程序的参数。 | Platform dependent. Defaults of scaffolding shown [above]({{< ref "/Docker/Customize#_python-docker-run" >}}) 平台相关。上面显示的脚手架的默认值 |
| `debugPort`   | The port that the debugger will listen on. 调试器将侦听的端口。 | `5678`                                                       |
| `wait`        | Whether to wait for debugger to attach. 是否等待调试器附加。 | `true`                                                       |
| `module`      | The Python module to run (only module **or** file should be chosen). 要运行的 Python 模块（仅应选择模块或文件）。 |                                                              |
| `file`        | The Python file to run (only module **or** file should be chosen). 要运行的 Python 文件（仅应选择模块或文件）。 |                                                              |

### [netCore object properties (docker-run task) netCore 对象属性（docker-run 任务）]({{< ref "/Docker/Customize#_netcore-object-properties-dockerrun-task" >}})

| Property 属性     | Description 说明                                             |
| :---------------- | :----------------------------------------------------------- |
| `appProject`      | The .NET project file (`.csproj`, `.fsproj`, etc.) associated with `docker-run` task. 与 `docker-run` 任务关联的 .NET 项目文件（ `.csproj` 、 `.fsproj` 等）。 Required. 必需。 |
| `configureSsl`    | Whether to configure ASP.NET Core SSL certificates and other settings to enable SSL on the service in the container. 是否配置 ASP.NET Core SSL 证书和其他设置以在容器中的服务上启用 SSL。 |
| `enableDebugging` | Whether to enable the started container for debugging. This will infer additional volume mappings and other options necessary for debugging. 是否启用已启动容器进行调试。这将推断出调试所需的额外卷映射和其他选项。 |

## [Docker Compose task Docker Compose 任务]({{< ref "/Docker/Customize#_docker-compose-task" >}})

The `docker-compose` task in `tasks.json` creates and starts Docker containers using the Docker Compose command line (CLI). The task can be used by itself, or as part of a chain of tasks to debug an application within a Docker container.

​​	在 `tasks.json` 中的 `docker-compose` 任务使用 Docker Compose 命令行 (CLI) 创建并启动 Docker 容器。该任务可以单独使用，也可以作为任务链的一部分，以便在 Docker 容器内调试应用程序。

The most important configuration setting for the `docker-compose` task is `dockerCompose`:

​​	对于 `docker-compose` 任务，最重要的配置设置是 `dockerCompose` ：

- The `dockerCompose` object specifies parameters for the Docker Compose command. Values specified by this object are applied directly to Docker Compose CLI invocation.
  `dockerCompose` 对象指定 Docker Compose 命令的参数。此对象指定的值直接应用于 Docker Compose CLI 调用。

See [property reference]({{< ref "/Docker/Customize#_compose-task-reference" >}}) for full list of all task properties.

​​	有关所有任务属性的完整列表，请参阅属性参考。

**Example configuration
示例配置**

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run docker-compose up",
      "type": "docker-compose",
      "dockerCompose": {
        "up": {
          "detached": true,
          "build": true,
          "services": ["myservice"]
        },
        "files": [
          "${workspaceFolder}/docker-compose.yml",
          "${workspaceFolder}/docker-compose.debug.yml"
        ]
      }
    }
  ]
}
```

## [Compose task reference Compose 任务参考]({{< ref "/Docker/Customize#_compose-task-reference" >}})

Here are all properties available for configuring `docker-compose` task. All properties are optional unless indicated otherwise.

​​	以下是可用于配置 `docker-compose` 任务的所有属性。除非另有说明，否则所有属性都是可选的。

| Property 属性   | Description 说明                                             |
| :-------------- | :----------------------------------------------------------- |
| `dockerCompose` | Options for controlling the `docker-compose` command executed ([see below]({{< ref "/Docker/Customize#_dockercompose-object-properties" >}})). 用于控制执行的 `docker-compose` 命令的选项（请参阅下文）。 Required. 必需。 |

### [dockerCompose object properties dockerCompose 对象属性]({{< ref "/Docker/Customize#_dockercompose-object-properties" >}})

| Property 属性 | Description 说明                                             | CLI Equivalent CLI 等效项 |
| :------------ | :----------------------------------------------------------- | :------------------------ |
| `up`          | Run a `docker-compose up` command. 运行 `docker-compose up` 命令。 Either this or `down` must be specified, but not both. 必须指定此项或 `down` ，但不能同时指定两者。 | `docker-compose up`       |
| `down`        | Run a `docker-compose down` command. 运行 `docker-compose down` 命令。 Either this or `up` must be specified, but not both. 必须指定此项或 `up` ，但不能同时指定两者。 | `docker-compose down`     |
| `files`       | The list of Docker Compose YAML files to use in the `docker-compose` command. If not specified, the Docker Compose CLI looks for `docker-compose.yml` and `docker-compose.override.yml`. 在 `docker-compose` 命令中要使用的 Docker Compose YAML 文件列表。如果未指定，Docker Compose CLI 会查找 `docker-compose.yml` 和 `docker-compose.override.yml` 。 | `-f <file>`               |
| `envFile`     | File of environment variables read in and applied to the containers. 读取并应用到容器的环境变量文件。 | `--env-file <file>`       |
| `projectName` | Alternate project name to use when naming and labeling Docker objects. If using an alternate project name when composing up, the same project name must be specified when composing down. 在命名和标记 Docker 对象时要使用的备用项目名称。如果在组合时使用备用项目名称，则在组合时必须指定相同的项目名称。 | `--project-name <name>`   |

### [up object properties up 对象属性]({{< ref "/Docker/Customize#_up-object-properties" >}})

| Property 属性   | Description 说明                                             | CLI Equivalent CLI 等效 | Default 默认 |
| :-------------- | :----------------------------------------------------------- | :---------------------- | :----------- |
| `detached`      | Whether or not to run detached. 是否以分离模式运行。         | `-d`                    | `true`       |
| `build`         | Whether or not to build before running. 是否在运行前构建。   | `--build`               | `true`       |
| `scale`         | Number of instances of each service to run. This is a list of key-value pairs. 要运行的每个服务的实例数。这是一个键值对列表。 | `--scale SERVICE=NUM`   |              |
| `services`      | A subset of the services to start. Cannot be combined with `profiles`. 要启动的服务的子集。不能与 `profiles` 组合使用。 | `[SERVICE...]`          | (all) (全部) |
| `profiles`      | A subset of the profiles to start. Cannot be combined with `services`. 要启动的配置文件的子集。不能与 `services` 组合使用。 | `--profile <profile>`   | (all) (全部) |
| `customOptions` | Any extra parameters to add after the `up` argument. No attempt is made to resolve conflicts with other options or validate this option. 要在 `up` 参数后添加的任何额外参数。不会尝试解决与其他选项的冲突或验证此选项。 | (any) (任意)            |              |

### [down object properties 下载对象属性]({{< ref "/Docker/Customize#_down-object-properties" >}})

| Property 属性   | Description 说明                                             | CLI Equivalent CLI 等效项 | Default 默认 |
| :-------------- | :----------------------------------------------------------- | :------------------------ | :----------- |
| `removeImages`  | Whether to remove images, and which. `all` will remove all images used by any service, `local` will remove only images without a custom tag. Leaving this unset will remove no images. 是否删除图像，以及删除哪些图像。 `all` 将删除任何服务使用的所有图像， `local` 将仅删除没有自定义标记的图像。如果不设置此项，则不会删除任何图像。 | `--rmi`                   |              |
| `removeVolumes` | Whether or not to remove named volumes. 是否删除命名卷。     | `-v`                      | `false`      |
| `customOptions` | Any extra parameters to add after the `down` argument. No attempt is made to resolve conflicts with other options or validate this option. 在 `down` 参数后添加的任何额外参数。不会尝试解决与其他选项的冲突或验证此选项。 | (any) (任何)              |              |

## [Command customization 命令自定义]({{< ref "/Docker/Customize#_command-customization" >}})

The Docker extension executes a number of Docker CLI commands when you perform various operations, such as to build images, run containers, attach to containers, and view container logs. Some of these commands have a large number of optional arguments, often used in very specific scenarios. As an alternative to the above Visual Studio Code tasks, several commands can be customized when tasks are not in use.

​​	当您执行各种操作（例如构建映像、运行容器、附加到容器和查看容器日志）时，Docker 扩展将执行许多 Docker CLI 命令。其中一些命令具有大量可选参数，通常用于非常特定的场景。作为上述 Visual Studio Code 任务的替代方法，可以在不使用任务时自定义多个命令。

For example, the tokens `${serviceList}` and `${profileList}` in the [Compose Up]({{< ref "/Docker/Customize#_docker-compose-up" >}}) command allows for easily starting a subset of the services within your Docker Compose YAML file(s).

​​	例如，Compose Up 命令中的标记 `${serviceList}` 和 `${profileList}` 允许轻松启动 Docker Compose YAML 文件中的服务子集。

For each of these customizable Docker commands, a configuration setting is available to set the template of what to execute. Alternatively, you can define multiple templates, optionally with a regular expression, which when matched, hints the context in which a template should be used. The templates support some tokens similar to `launch.json` and `tasks.json`, for example, `${workspaceFolder}`.

​​	对于这些可自定义的 Docker 命令中的每一个，都有一个配置设置可用于设置要执行的模板。或者，您可以定义多个模板，也可以使用正则表达式，当匹配时，提示应在其中使用模板的上下文。这些模板支持一些类似于 `launch.json` 和 `tasks.json` 的标记，例如 `${workspaceFolder}` 。

### [Settings JSON schema 设置 JSON 架构]({{< ref "/Docker/Customize#_settings-json-schema" >}})

You have two options for configuring each of the templates (listed below). The first option is a single template that overrides the default behavior:

​​	您有两种选择来配置每个模板（如下所列）。第一个选项是覆盖默认行为的单个模板：

```
{
  "docker.commands.build": "docker build --rm -f \"${dockerfile}\" -t ${tag} \"${context}\""
}
```

The second option is multiple templates that will be chosen based on the `match` regular expression, as well as user input.

​​	第二个选项是将根据 `match` 正则表达式以及用户输入来选择的多个模板。

For example, three templates are shown in the following example:

​​	例如，以下示例中显示了三个模板：

```
{
  "docker.commands.build": [
    {
      "label": "Default build command",
      "template": "docker build --rm -f \"${dockerfile}\" -t ${tag} \"${context}\""
    },
    {
      "label": "Alpine-specific build command",
      "template": "docker build -p 1234:1234 -f \"${dockerfile}\" -t ${tag} \"${context}\"",
      "match": "alpine"
    }
  ]
}
```

### [Selection behavior 选择行为]({{< ref "/Docker/Customize#_selection-behavior" >}})

The command template chosen to execute is selected based on the following rules:

​​	根据以下规则选择要执行的命令模板：

1. If no setting is configured, the default command template is chosen.
   如果未配置任何设置，则选择默认命令模板。

2. If only a single template is configured (the first example above), that template is chosen.
   如果仅配置了一个模板（上面的第一个示例），则选择该模板。

3. If multiple templates are configured:

   
   如果配置了多个模板：

   1. Constrained templates are checked. A constrained template has `match`. The `match` regular expression is compared against contextual hints--for example, image name, container name, etc.
      检查受限模板。受限模板具有 `match` 。 `match` 正则表达式与上下文提示（例如，映像名称、容器名称等）进行比较。
   2. If multiple constrained templates apply, the user will be prompted to choose. If only one applies, the user will not be prompted.
      如果应用多个受限模板，系统将提示用户选择。如果只应用一个，则不会提示用户。
   3. If there no applicable constrained templates, unconstrained templates are checked. An unconstrained template does not have `match`, and is therefore always applicable.
      如果没有适用的受限模板，则检查不受限模板。不受限模板没有 `match` ，因此始终适用。
   4. If multiple unconstrained templates apply, the user will be prompted to choose. If only one applies, the user will not be prompted.
      如果应用多个不受限模板，系统将提示用户选择。如果只应用一个，则不会提示用户。

### [Docker Build Docker 构建]({{< ref "/Docker/Customize#_docker-build" >}})

| Configuration Setting 配置设置 | Default Value 默认值                                         |
| :----------------------------- | :----------------------------------------------------------- |
| `docker.commands.build`        | `${containerCommand} build --rm -f "${dockerfile}" -t ${tag} "${context}"` |

Supported tokens:

​​	支持的标记：

| Token 标记            | Description 说明                                             |
| :-------------------- | :----------------------------------------------------------- |
| `${containerCommand}` | The CLI command / executable used to execute container commands. 用于执行容器命令的 CLI 命令/可执行文件。 |
| `${dockerfile}`       | The workspace-relative path of the selected `Dockerfile`. 所选 `Dockerfile` 的工作区相对路径。 |
| `${tag}`              | The value entered/confirmed by the user upon invoking the build command. If previously built, defaults to the previously entered value for that `Dockerfile`. 用户在调用构建命令时输入/确认的值。如果之前已构建，则默认为该 `Dockerfile` 的先前输入值。 |
| `${context}`          | If set, the value of the `docker.imageBuildContextPath` configuration setting. Otherwise, the workspace-relative folder in which the `Dockerfile` resides. 如果已设置，则为 `docker.imageBuildContextPath` 配置设置的值。否则，为 `Dockerfile` 所在的工作区相关文件夹。 |

> **Note**: If the `docker.commands.build` setting does not contain the `${tag}` token, the user will **not** be prompted to enter/confirm a tag.
>
> ​​	注意：如果 `docker.commands.build` 设置不包含 `${tag}` 令牌，则不会提示用户输入/确认标签。

> **Note**: The `match` regular expression will be compared against the selected Dockerfile name and the workspace folder name.
>
> ​​	注意：将针对所选 Dockerfile 名称和工作区文件夹名称比较 `match` 正则表达式。

### [Docker Run Docker 运行]({{< ref "/Docker/Customize#_docker-run" >}})

| Configuration Setting 配置设置   | Default Value 默认值                                      |
| :------------------------------- | :-------------------------------------------------------- |
| `docker.commands.run`            | `${containerCommand} run --rm -d ${exposedPorts} ${tag}`  |
| `docker.commands.runInteractive` | `${containerCommand} run --rm -it ${exposedPorts} ${tag}` |

Supported tokens:

​​	支持的令牌：

| Token 令牌            | Description 说明                                             |
| :-------------------- | :----------------------------------------------------------- |
| `${containerCommand}` | The CLI command / executable used to execute container commands. 用于执行容器命令的 CLI 命令/可执行文件。 |
| `${exposedPorts}`     | Generated from the list of exposed ports in the image (ultimately from the `Dockerfile`), where each exposed port is mapped to the same port on the local machine. For example, `"EXPOSE 5000 5001"` would generate `"-p 5000:5000 -p 5001:5001"`. 从镜像中公开的端口列表（最终来自 `Dockerfile` ）生成，其中每个公开的端口都映射到本地计算机上的相同端口。例如， `"EXPOSE 5000 5001"` 会生成 `"-p 5000:5000 -p 5001:5001"` 。 |
| `${tag}`              | The full tag of the selected image. 所选镜像的完整标记。     |

> **Note**: The `match` regular expression will be compared against the full tag of the selected image.
>
> ​​	注意： `match` 正则表达式将与所选镜像的完整标记进行比较。

### [Docker Attach]({{< ref "/Docker/Customize#_docker-attach" >}})

| Configuration Setting 配置设置 | Default Value 默认值                                         |
| :----------------------------- | :----------------------------------------------------------- |
| `docker.commands.attach`       | `${containerCommand} exec -it ${containerId} ${shellCommand}` |

Supported tokens:

​​	支持的标记：

| Token 标记            | Description 说明                                             |
| :-------------------- | :----------------------------------------------------------- |
| `${containerCommand}` | The CLI command / executable used to execute container commands. 用于执行容器命令的 CLI 命令/可执行文件。 |
| `${containerId}`      | The ID of the container to attach to. 要附加到的容器的 ID。  |
| `${shellCommand}`     | If `bash` is present in the container, it is substituted here, otherwise `sh`. In Windows containers, `cmd` is always used. 如果容器中存在 `bash` ，则在此处替换，否则为 `sh` 。在 Windows 容器中，始终使用 `cmd` 。 |

> **Note**: The `match` regular expression will be compared against the container name and full tag of the container image.
>
> ​​	注意： `match` 正则表达式将与容器名称和容器镜像的完整标记进行比较。

### [Docker Logs Docker 日志]({{< ref "/Docker/Customize#_docker-logs" >}})

| Configuration Setting 配置设置 | Default Value 默认值                         |
| :----------------------------- | :------------------------------------------- |
| `docker.commands.logs`         | `${containerCommand} logs -f ${containerId}` |

Supported tokens:

​​	支持的令牌：

| Token 令牌            | Description 说明                                             |
| :-------------------- | :----------------------------------------------------------- |
| `${containerCommand}` | The CLI command / executable used to execute container commands. 用于执行容器命令的 CLI 命令/可执行文件。 |
| `${containerId}`      | The ID of the container to view the logs for. 要查看其日志的容器的 ID。 |

> **Note**: The `match` regular expression will be compared against the container name and full tag of the container image.
>
> ​​	注意： `match` 正则表达式将与容器名称和容器映像的完整标记进行比较。

### [Docker Compose Up]({{< ref "/Docker/Customize#_docker-compose-up" >}})

| Configuration Setting 配置设置 | Default Value 默认值                                         |
| :----------------------------- | :----------------------------------------------------------- |
| `docker.commands.composeUp`    | `${composeCommand} ${configurationFile} up ${detached} ${build}` |

Supported tokens:

​​	支持的令牌：

| Token 令牌             | Description 说明                                             |
| :--------------------- | :----------------------------------------------------------- |
| `${configurationFile}` | Set to `-f` plus the workspace-relative path to the selected Docker Compose YAML file. 设置为 `-f` ，加上选定的 Docker Compose YAML 文件相对于工作空间的路径。 |
| `${detached}`          | Set to `-d` if the configuration setting `docker.dockerComposeDetached` is set to `true`. Otherwise, set to `""`. 如果配置设置 `docker.dockerComposeDetached` 设置为 `true` ，则设置为 `-d` 。否则，设置为 `""` 。 |
| `${build}`             | Set to `--build` if the configuration setting `docker.dockerComposeBuild` is set to `true`. Otherwise, set to `""`. 如果配置设置 `docker.dockerComposeBuild` 设置为 `true` ，则设置为 `--build` 。否则，设置为 `""` 。 |
| `${serviceList}`       | If specified, prompts for a subset of the services to start when the command is run. 如果指定，则在运行命令时提示启动服务的子集。 |
| `${profileList}`       | If specified and the Docker Compose YAML file contains profiles, prompts for a subset of the profiles to start when the command is run. 如果指定并且 Docker Compose YAML 文件包含配置文件，则在运行命令时提示启动配置文件的子集。 |
| `${composeCommand}`    | Set to the value of the `docker.composeCommand` setting if set, otherwise the extension will try to automatically determine the command to use (`docker compose` or `docker-compose`). 如果设置了 `docker.composeCommand` 设置的值，则设置为该值，否则扩展程序将尝试自动确定要使用的命令（ `docker compose` 或 `docker-compose` ）。 |

### [Docker Compose Down]({{< ref "/Docker/Customize#_docker-compose-down" >}})

| Configuration Setting 配置设置 | Default Value 默认值                          |
| :----------------------------- | :-------------------------------------------- |
| `docker.commands.composeDown`  | `${composeCommand} ${configurationFile} down` |

Supported tokens:

​​	支持的令牌：

| Token 令牌             | Description 说明                                             |
| :--------------------- | :----------------------------------------------------------- |
| `${configurationFile}` | Set to `-f` plus the workspace-relative path to the selected Docker Compose YAML file. 设置为 `-f` ，外加选定的 Docker Compose YAML 文件相对于工作区路径。 |
| `${composeCommand}`    | Set to the value of the `docker.composeCommand` setting if set, otherwise the extension will try to automatically determine the command to use (`docker compose` or `docker-compose`). 如果已设置，则设置为 `docker.composeCommand` 设置的值，否则扩展程序将尝试自动确定要使用的命令（ `docker compose` 或 `docker-compose` ）。 |

### [Additional supported tokens 其他受支持的令牌]({{< ref "/Docker/Customize#_additional-supported-tokens" >}})

In addition to the command-specific supported tokens, the following tokens are supported in all command templates:

​​	除了特定于命令的受支持令牌外，所有命令模板中还支持以下令牌：

| Token 令牌                          | Description 说明                                             |
| :---------------------------------- | :----------------------------------------------------------- |
| `${workspaceFolder}`                | The selected workspace folder path. 选定的工作区文件夹路径。 |
| `${config:some.setting.identifier}` | The value of any configuration setting, as long as it is a string, number, or boolean. These setting identifiers can be arbitrarily defined and do not need to belong to Visual Studio Code or to any extension. 任何配置设置的值，只要它是字符串、数字或布尔值。这些设置标识符可以任意定义，不必属于 Visual Studio Code 或任何扩展程序。 |
| `${env:Name}`                       | The value of an environment variable. 环境变量的值。         |
| `${command:commandID}`              | The string return value of a command. 命令的字符串返回值。   |
