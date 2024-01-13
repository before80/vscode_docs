+++
title = "advanced containers"
date = 2024-01-13T13:53:43+08:00
type = "docs"
description = ""
isCJKLanguage = true
draft = false
weight = 5
+++

> 原文: [https://code.visualstudio.com/#advancedcontainers-articles](https://code.visualstudio.com/#advancedcontainers-articles)

# Advanced container configuration 高级容器配置



The articles in this section cover advanced container configuration when working with the Visual Studio Code [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension.

​​	本部分中的文章介绍在使用 Visual Studio Code Dev Containers 扩展时的高级容器配置。

## [Working with containers 使用容器](https://code.visualstudio.com/remote/advancedcontainers/overview#_working-with-containers)

The **Visual Studio Code Dev Containers** extension lets you use a [Docker container](https://docker.com/) as a full-featured development environment. It allows you to open any folder inside (or mounted into) a container and take advantage of Visual Studio Code's full feature set. A [devcontainer.json file](https://code.visualstudio.com/docs/devcontainers/containers#_create-a-devcontainerjson-file) in your project tells VS Code how to access (or create) a **development container** with a well-defined tool and runtime stack. This container can be used to run an application or to separate tools, libraries, or runtimes needed for working with a codebase.

​​	Visual Studio Code Dev Containers 扩展允许您将 Docker 容器用作功能齐全的开发环境。它允许您在容器内（或挂载到容器内）打开任何文件夹，并利用 Visual Studio Code 的全套功能。项目中的 devcontainer.json 文件告诉 VS Code 如何使用明确定义的工具和运行时堆栈来访问（或创建）开发容器。此容器可用于运行应用程序或分离处理代码库所需工具、库或运行时。

Workspace files are mounted from the local file system or copied or cloned into the container. Extensions are installed and run inside the container, where they have full access to the tools, platform, and file system. This means that you can seamlessly switch your entire development environment just by connecting to a different container.

​​	工作区文件从本地文件系统挂载或复制或克隆到容器中。扩展安装并运行在容器内，在容器内它们可以完全访问工具、平台和文件系统。这意味着您只需连接到不同的容器，即可无缝切换整个开发环境。

This lets VS Code provide a **local-quality development experience** — including full IntelliSense (completions), code navigation, and debugging — **regardless of where your tools (or code) are located**.

​​	这使 VS Code 能够提供本地质量的开发体验——包括完整的 IntelliSense（自动完成）、代码导航和调试——无论你的工具（或代码）位于何处。

## [Getting Started 入门](https://code.visualstudio.com/remote/advancedcontainers/overview#_getting-started)

If you are new to Docker containers and using the VS Code [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension, we recommend starting with the introductory [Containers](https://code.visualstudio.com/docs/devcontainers/containers) article. There you will find:

​​	如果你不熟悉 Docker 容器和使用 VS Code Dev Containers 扩展，我们建议从介绍性容器文章开始。在那里你会找到：

- [System requirements](https://code.visualstudio.com/docs/devcontainers/containers#_system-requirements) - What's needed to run on Windows, macOS, and Linux.
  系统要求 - 在 Windows、macOS 和 Linux 上运行所需的内容。
- [Installation](https://code.visualstudio.com/docs/devcontainers/containers#_installation) - How to install Docker, VS Code, and the Remote Development Extension Pack.
  安装 - 如何安装 Docker、VS Code 和远程开发扩展包。
- [Quick starts](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-try-a-development-container) - Step-by-step instructions for common container scenarios.
  快速入门 - 常见容器场景的分步说明。

Once you have your machine configured, try the [Containers tutorial](https://code.visualstudio.com/docs/devcontainers/tutorial) for an in-depth tour of working with containers.

​​	一旦你配置好你的机器，请尝试容器教程，深入了解如何使用容器。

## [Advanced Containers topics 高级容器主题](https://code.visualstudio.com/remote/advancedcontainers/overview#_advanced-containers-topics)

The articles listed in the table of contents below, describe advanced container usage and cover specific configurations in detail. You may not need to apply these for your development workflow but it is good to quickly review the articles, in case you might need them in the future.

​​	下表中列出的文章介绍了高级容器用法，并详细介绍了特定配置。你可能不需要将它们应用于你的开发工作流，但快速查看这些文章是件好事，以防你将来可能需要它们。

You can learn how to:

​​	你可以学习如何：

- [Set environment variables
  设置环境变量](https://code.visualstudio.com/remote/advancedcontainers/environment-variables)
- [Mount local disk drives
  挂载本地磁盘驱动器](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount)
- [Add a non-root user
  添加非 root 用户](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user)
- [Work with multiple containers
  使用多个容器](https://code.visualstudio.com/remote/advancedcontainers/connect-multiple-containers)
- And more...
  更多...

## [Feedback and questions 反馈和问题](https://code.visualstudio.com/remote/advancedcontainers/overview#_feedback-and-questions)

You can also provide [feedback](https://code.visualstudio.com/remote/advancedcontainers/questions-feedback#_feedback) on the Remote Development experience or reach out with [questions](https://code.visualstudio.com/remote/advancedcontainers/questions-feedback#_resources).

​​	您还可以提供有关远程开发体验的反馈或提出问题。
