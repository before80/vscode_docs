+++
title = "Additional Components"
date = 2024-01-12T22:36:24+08:00
weight = 60
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/additional-components](https://code.visualstudio.com/docs/setup/additional-components)

# Additional components and tools 其他组件和工具



Visual Studio Code is a small download by design and only includes the minimum number of components shared across most development workflows. Basic functionality like the editor, file management, window management, and preference settings are included. A JavaScript/TypeScript language service and Node.js debugger are also part of the base install.

​​	Visual Studio Code 设计时下载量小，并且仅包含大多数开发工作流中共享的最小组件数。包括编辑器、文件管理、窗口管理和首选项设置等基本功能。JavaScript/TypeScript 语言服务和 Node.js 调试器也是基本安装的一部分。

If you are used to working with larger, monolithic development tools (IDEs), you may be surprised that your scenarios aren't completely supported out of the box. For example, there isn't a **File** > **New Project** dialog with pre-installed project templates. Most VS Code users will need to install additional components depending on their specific needs.

​​	如果您习惯使用更大的单片式开发工具 (IDE)，您可能会惊讶地发现您的方案并未完全开箱即用地得到支持。例如，没有预装项目模板的文件 > 新建项目对话框。大多数 VS Code 用户需要根据其特定需求安装其他组件。

## [Commonly used components 常用组件]({{< ref "/Setup/AdditionalComponents#_commonly-used-components" >}})

Here are a few commonly installed components:

​​	以下是一些常用的已安装组件：

- [Git](https://git-scm.com/download) - VS Code has built-in support for source code control using Git but requires Git to be installed separately.
  Git - VS Code 内置了使用 Git 进行源代码控制的支持，但需要单独安装 Git。
- [Node.js (includes npm)](https://nodejs.org/) - A cross platform runtime for building and running JavaScript applications.
  Node.js（包括 npm） - 用于构建和运行 JavaScript 应用程序的跨平台运行时。
- [TypeScript](https://www.typescriptlang.org/) - The TypeScript compiler, `tsc`, for transpiling TypeScript to JavaScript.
  TypeScript - TypeScript 编译器， `tsc` ，用于将 TypeScript 转换为 JavaScript。

You'll find the components above mentioned often in our documentation and walkthroughs.

​​	您将在我们的文档和演练中经常发现上面提到的组件。

## [VS Code extensions VS Code 扩展]({{< ref "/Setup/AdditionalComponents#_vs-code-extensions" >}})

You can extend the VS Code editor itself through [extensions]({{< ref "/UserGuide/ExtensionMarketplace" >}}). The VS Code community has built hundreds of useful extensions available on the VS Code [Marketplace](https://marketplace.visualstudio.com/VSCode).

​​	您可以通过扩展来扩展 VS Code 编辑器本身。VS Code 社区已经构建了数百个有用的扩展，可在 VS Code Marketplace 上获取。

![Python](./AdditionalComponents_img/Microsoft.VisualStudio.Services.Icons.png)

Python

109.0M

ms-python

![C/C++](./AdditionalComponents_img/Microsoft.VisualStudio.Services.Icons-1705074104129-12.png)

C/C++

58.3M

ms-vscode

![Extension Pack for Java](./AdditionalComponents_img/Microsoft.VisualStudio.Services.Icons-1705074104129-13.png)

Extension Pack for Java
适用于 Java 的扩展包

24.2M

vscjava

![GitHub Copilot](./AdditionalComponents_img/Microsoft.VisualStudio.Services.Icons-1705074104129-14.png)

GitHub Copilot

12.1M

GitHub

The extensions shown above are the current most popular on Marketplace. Click on an extension tile above to read the description and reviews of the extension.

​​	上面显示的扩展是 Marketplace 上当前最受欢迎的扩展。单击上面的扩展磁贴以阅读扩展的说明和评论。

## [Additional tools 其他工具]({{< ref "/Setup/AdditionalComponents#_additional-tools" >}})

Visual Studio Code integrates with existing tool chains. We think the following tools will enhance your development experiences.

​​	Visual Studio Code 与现有工具链集成。我们认为以下工具将增强您的开发体验。

- [Yeoman](https://yeoman.io/) - An application scaffolding tool, a command line version of **File** > **New Project**.
  Yeoman - 一个应用程序脚手架工具，是“文件”>“新建项目”的命令行版本。
- [generator-hottowel](https://github.com/johnpapa/generator-hottowel) - A Yeoman generator for quickly creating AngularJS applications.
  generator-hottowel - 一个 Yeoman 生成器，用于快速创建 AngularJS 应用程序。
- [Express](https://expressjs.com/) - An application framework for Node.js applications using the Pug template engine.
  Express - 一个使用 Pug 模板引擎的 Node.js 应用程序的应用程序框架。
- [Gulp](https://gulpjs.com/) - A streaming task runner system which integrates easily with VS Code tasks.
  Gulp - 一个流任务运行程序系统，可轻松与 VS Code 任务集成。
- [Mocha](https://mochajs.org/) - A JavaScript test framework that runs on Node.js.
  Mocha - 一个运行在 Node.js 上的 JavaScript 测试框架。
- [Yarn](https://yarnpkg.com/) - A dependency manager and alternative to npm.
  Yarn - 一个依赖管理器和 npm 的替代品。

> **Note:** Most of these tools require Node.js and the npm package manager to install and use.
>
> ​​	注意：大多数这些工具都需要 Node.js 和 npm 包管理器才能安装和使用。

## [Next steps 后续步骤]({{< ref "/Setup/AdditionalComponents#_next-steps" >}})

- [User Interface]({{< ref "/GetStarted/UserInterface" >}}) - A quick orientation around VS Code.
  用户界面 - VS Code 的快速入门。
- [User/Workspace Settings]({{< ref "/GetStarted/Settings" >}}) - Learn how to configure VS Code to your preferences through settings.
  用户/工作区设置 - 了解如何通过设置将 VS Code 配置为您的首选项。
- [Languages]({{< ref "/Languages/Overview" >}}) - VS Code supports many programming languages out-of-the-box as well as many more through community created extensions.
  语言 - VS Code 开箱即用支持多种编程语言，还可通过社区创建的扩展支持更多语言。
