+++
title = "Reduce Docker warnings"
date = 2024-01-13T13:53:43+08:00
weight = 130
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings](https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings)

# Reduce Docker build warnings 减少 Docker 构建警告



The following are some tips for eliminating warnings that may be appearing in your Dockerfile builds.

​​	以下是一些消除 Dockerfile 构建中可能出现的警告的提示。

## [debconf: delaying package configuration, since apt-utils is not installed debconf: 延迟软件包配置，因为未安装 apt-utils](https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings#_debconf-delaying-package-configuration-since-aptutils-is-not-installed)

This error can typically be safely ignored and is tricky to get rid of completely. However, you can reduce it to one message in stdout when installing the needed package by adding the following to your Dockerfile:

​​	此错误通常可以安全地忽略，并且很难完全消除。但是，您可以在安装所需软件包时将其减少到 stdout 中的一条消息，方法是将以下内容添加到 Dockerfile 中：

```
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1
```

## [Warning: apt-key output should not be parsed (stdout is not a terminal) 警告：不应解析 apt-key 输出（stdout 不是终端）](https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings#_warning-aptkey-output-should-not-be-parsed-stdout-is-not-a-terminal)

This non-critical warning tells you not to parse the output of `apt-key`, so as long as your script doesn't, there's no problem. You can safely ignore it.

​​	此非关键警告告诉您不要解析 `apt-key` 的输出，因此只要您的脚本不解析，就没有问题。您可以安全地忽略它。

This occurs in Dockerfiles because the `apt-key` command is not running from a terminal. Unfortunately, this error cannot be eliminated completely, but can be hidden unless the `apt-key` command returns a non-zero exit code (indicating a failure).

​​	这发生在 Dockerfile 中，因为 `apt-key` 命令不是从终端运行的。不幸的是，此错误无法完全消除，但可以隐藏，除非 `apt-key` 命令返回非零退出代码（指示失败）。

For example:

​​	例如：

```
# (OUT=$(apt-key add - 2>&1) || echo $OUT) will only print the output with non-zero exit code is hit
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | (OUT=$(apt-key add - 2>&1) || echo $OUT)
```

You can also set the `APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE` environment variable to suppress the warning, but it looks a bit scary so be sure to add comments in your Dockerfile if you use it:

​​	您还可以设置 `APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE` 环境变量来禁止警告，但看起来有点可怕，因此如果您使用它，请务必在 Dockerfile 中添加注释：

```
# Suppress an apt-key warning about standard out not being a terminal. Use in this script is safe.
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn
```

## [Information messages appearing in red 以红色显示的信息消息](https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings#_information-messages-appearing-in-red)

Some CLIs output certain information (like debug details) to standard error instead of standard out. These will appear in red in Visual Studio Code's terminal and output logs.

​​	某些 CLI 将某些信息（如调试详细信息）输出到标准错误，而不是标准输出。这些信息将以红色显示在 Visual Studio Code 的终端和输出日志中。

If the messages are harmless, you can pipe the output of the command from standard error to standard out instead by appending `2>&1` to the end of the command.

​​	如果这些消息无害，您可以通过在命令末尾追加 `2>&1` 将命令的输出从标准错误管道传输到标准输出。

For example:

​​	例如：

```
RUN apt-get -y install --no-install-recommends apt-utils dialog 2>&1
```

If the command fails, you will still be able to see the errors but they won't be in red.

​​	如果命令失败，您仍然可以看到错误，但它们不会显示为红色。

## [Avoiding problems with images built using Docker 避免使用 Docker 构建的映像出现问题](https://code.visualstudio.com/remote/advancedcontainers/reduce-docker-warnings#_avoiding-problems-with-images-built-using-docker)

Given Dockerfiles and Docker Compose files can be used without VS Code or the `devcontainer` CLI, you may want to let users know that they should not try to build the image directly if it will not work as expected. To solve this problem, you can add a build argument that needs to be specified for things to work.

​​	鉴于 Dockerfile 和 Docker Compose 文件可以在没有 VS Code 或 `devcontainer` CLI 的情况下使用，您可能希望让用户知道，如果映像无法按预期工作，他们不应尝试直接构建该映像。要解决此问题，您可以添加一个构建参数，该参数需要指定才能使各项功能正常工作。

For example, you could add the following to your Dockerfile:

​​	例如，您可以将以下内容添加到 Dockerfile 中：

```
ARG vscode
RUN if [[ -z "$devcontainercli" ]] ; then printf "\nERROR: This Dockerfile needs to be built with VS Code !" && exit 1; else printf "VS Code is detected: $devcontainercli"; fi
```

And the following in your `devcontainer.json`:

​​	以及以下内容添加到 `devcontainer.json` 中：

```
"build": {
      "dockerfile": "Dockerfile",
      "args": {
          // set devcontainer-cli arg for Dockerfile
          "devcontainercli": "true"
      },
    }
```

In the Docker Compose case, you can add this argument to a separate [override file to extend your configuration](https://code.visualstudio.com/docs/devcontainers/create-dev-container#_extend-your-docker-compose-file-for-development) that is located in a different place in your source tree than the primary Docker Compose file.

​​	在 Docker Compose 的情况下，您可以将此参数添加到一个单独的覆盖文件中，以扩展位于源树中与主 Docker Compose 文件不同的位置的配置。
