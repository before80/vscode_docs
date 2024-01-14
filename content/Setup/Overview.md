+++
title = "Overview"
date = 2024-01-12T22:36:24+08:00
weight = 1
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/setup-overview](https://code.visualstudio.com/docs/setup/setup-overview)

# Setting up Visual Studio Code 设置 Visual Studio Code



Getting up and running with Visual Studio Code is quick and easy. It is a small download so you can install in a matter of minutes and give VS Code a try.

​​	使用 Visual Studio Code 快速轻松地启动并运行。它是一个小巧的下载程序，因此您可以在几分钟内安装并试用 VS Code。

## [Cross platform 跨平台]({{< ref "/Setup/Overview#_cross-platform" >}})

VS Code is a free code editor, which runs on the macOS, Linux, and Windows operating systems.

​​	VS Code 是一款免费的代码编辑器，可在 macOS、Linux 和 Windows 操作系统上运行。

Follow the platform-specific guides below:

​​	请按照以下特定于平台的指南操作：

- [macOS]({{< ref "/Setup/macOS" >}})
- [Linux]({{< ref "/Setup/Linux" >}})
- [Windows]({{< ref "/Setup/Windows" >}})

VS Code is lightweight and should run on most available hardware and platform versions. You can review the [System Requirements](https://code.visualstudio.com/docs/supporting/requirements) to check if your computer configuration is supported.

​​	VS Code 非常轻巧，应该可以在大多数可用硬件和平台版本上运行。您可以查看系统要求以检查您的计算机配置是否受支持。

## [Update cadence 更新节奏]({{< ref "/Setup/Overview#_update-cadence" >}})

VS Code releases a new version [each month](https://code.visualstudio.com/updates) with new features and important bug fixes. Most platforms support auto updating and you will be prompted to install the new release when it becomes available. You can also manually check for updates by running **Help** > **Check for Updates** on Linux and Windows or running **Code** > **Check for Updates** on macOS.

​​	VS Code 每月发布一个新版本，其中包含新功能和重要的错误修复。大多数平台支持自动更新，当新版本可用时，系统会提示您安装。您还可以通过在 Linux 和 Windows 上运行“帮助”>“检查更新”或在 macOS 上运行“代码”>“检查更新”来手动检查更新。

> Note: You can [disable auto-update](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates) if you prefer to update VS Code on your own schedule.
>
> ​​	注意：如果您希望按照自己的时间表更新 VS Code，则可以禁用自动更新。

## [Insiders nightly build Insiders 夜间版本]({{< ref "/Setup/Overview#_insiders-nightly-build" >}})

If you'd like to try our nightly builds to see new features early or verify bug fixes, you can install our [Insiders build](https://code.visualstudio.com/insiders). The Insiders build installs side-by-side with the monthly Stable build and you can freely work with either on the same machine. The Insiders build is the same one the VS Code development team uses on a daily basis and we really appreciate people trying out new features and providing feedback.

​​	如果您想尝试我们的夜间版本以提前了解新功能或验证错误修复，则可以安装我们的 Insiders 版本。Insiders 版本与每月稳定版本并行安装，您可以在同一台计算机上自由使用任一版本。Insiders 版本与 VS Code 开发团队每天使用的版本相同，我们非常感谢大家试用新功能并提供反馈。

## [Portable mode 便携模式]({{< ref "/Setup/Overview#_portable-mode" >}})

Visual Studio Code supports [Portable mode](https://en.wikipedia.org/wiki/Portable_application) installation. This mode enables all data created and maintained by VS Code to live near itself, so it can be moved around across environments, for example, on a USB drive. See the [VS Code Portable Mode](https://code.visualstudio.com/docs/editor/portable) documentation for details.

​​	Visual Studio Code 支持便携模式安装。此模式使 VS Code 创建和维护的所有数据都位于其附近，因此可以在环境之间移动，例如，在 USB 驱动器上。有关详细信息，请参阅 VS Code 便携模式文档。

## [Additional components 其他组件]({{< ref "/Setup/Overview#_additional-components" >}})

VS Code is an editor, first and foremost, and prides itself on a small footprint. Unlike traditional IDEs that tend to include everything but the kitchen sink, you can tune your installation to the development technologies you care about. Be sure to read the [Additional Components]({{< ref "/Setup/AdditionalComponents" >}}) topic after reading the platform guides to learn about customizing your VS Code installation.

​​	VS Code 首先是一款编辑器，并且以占用空间小而自豪。与倾向于包含除厨房水槽以外所有内容的传统 IDE 不同，您可以将安装调整为您关心的开发技术。务必在阅读平台指南后阅读其他组件主题，以了解如何自定义 VS Code 安装。

## [Extensions 扩展]({{< ref "/Setup/Overview#_extensions" >}})

VS Code [extensions]({{< ref "/UserGuide/ExtensionMarketplace" >}}) let third parties add support for additional:

​​	VS Code 扩展允许第三方添加对以下内容的支持：

- Languages - [C++]({{< ref "/Languages/C" >}}), [C#]({{< ref "/Languages/C#" >}}), [Go]({{< ref "/Languages/Go" >}}), [Java]({{< ref "/Languages/Java" >}}), [Python]({{< ref "/Languages/Python" >}})
  语言 - C++、C#、Go、Java、Python
- Tools - [ESLint](https://marketplace.visualstudio.com/items/dbaeumer.vscode-eslint), [JSHint](https://marketplace.visualstudio.com/items/dbaeumer.jshint) , [PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)
  工具 - ESLint、JSHint、PowerShell
- Debuggers - [PHP XDebug](https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug).
  调试器 - PHP XDebug。
- Keymaps - [Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim), [Sublime Text](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings), [IntelliJ](https://marketplace.visualstudio.com/items?itemName=k--kato.intellij-idea-keybindings), [Emacs](https://marketplace.visualstudio.com/items?itemName=hiro-sun.vscode-emacs), [Atom](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings), [Brackets](https://marketplace.visualstudio.com/items?itemName=ms-vscode.brackets-keybindings), [Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vs-keybindings), [Eclipse](https://marketplace.visualstudio.com/items?itemName=alphabotsec.vscode-eclipse-keybindings)
  按键映射 - Vim、Sublime Text、IntelliJ、Emacs、Atom、Brackets、Visual Studio、Eclipse

Extensions integrate into VS Code's UI, commands, and task running systems so you'll find it easy to work with different technologies through VS Code's shared interface. Check out the VS Code extension [Marketplace](https://marketplace.visualstudio.com/vscode) to see what's available.

​​	扩展集成到 VS Code 的 UI、命令和任务运行系统中，因此您会发现通过 VS Code 的共享界面使用不同的技术非常容易。查看 VS Code 扩展市场以了解可用内容。

## [Next steps 后续步骤]({{< ref "/Setup/Overview#_next-steps" >}})

Once you have installed and set up VS Code, these topics will help you learn more about VS Code:

​​	安装并设置 VS Code 后，以下主题将帮助您详细了解 VS Code：

- [Additional Components]({{< ref "/Setup/AdditionalComponents" >}}) - Learn how to install Git, Node.js, TypeScript, and tools like Yeoman.
  其他组件 - 了解如何安装 Git、Node.js、TypeScript 和 Yeoman 等工具。
- [User Interface]({{< ref "/GetStarted/UserInterface" >}}) - A quick orientation to VS Code.
  用户界面 - 快速了解 VS Code。
- [Basic Editing]({{< ref "/UserGuide/BasicEditing" >}}) - Learn about the powerful VS Code editor.
  基本编辑 - 了解功能强大的 VS Code 编辑器。
- [Code Navigation]({{< ref "/UserGuide/CodeNavigation" >}}) - Move quickly through your source code.
  代码导航 - 快速浏览源代码。
- [Debugging]({{< ref "/UserGuide/Debugging" >}}) - Debug your source code directly in the VS Code editor.
  调试 - 直接在 VS Code 编辑器中调试源代码。
- [Proxy Server Support]({{< ref "/Setup/Network" >}}) - Configure your proxy settings.
  代理服务器支持 - 配置代理设置。

If you'd like to get something running quickly, try the [Node.js tutorial]({{< ref "/Node_jsJavaScript/Node_jsTutorial" >}}) walkthrough that will have you debugging a Node.js web application with VS Code in minutes.

​​	如果您想快速运行某些内容，请尝试 Node.js 教程演练，几分钟内即可使用 VS Code 调试 Node.js Web 应用程序。

## [Common questions 常见问题]({{< ref "/Setup/Overview#_common-questions" >}})

### [What are the system requirements for VS Code? VS Code 的系统要求是什么？]({{< ref "/Setup/Overview#_what-are-the-system-requirements-for-vs-code" >}})

We have a list of [System Requirements](https://code.visualstudio.com/docs/supporting/requirements).

​​	我们提供了系统要求列表。

### [How big is VS Code? VS Code 有多大？]({{< ref "/Setup/Overview#_how-big-is-vs-code" >}})

VS Code is a small download (< 100 MB) and has a disk footprint of less than 200 MB, so you can quickly install VS Code and try it out.

​​	VS Code 下载量小（< 100 MB），磁盘占用空间小于 200 MB，因此您可以快速安装 VS Code 并试用。

### [How do I create and run a new project? 如何创建并运行新项目？]({{< ref "/Setup/Overview#_how-do-i-create-and-run-a-new-project" >}})

VS Code doesn't include a traditional **File** > **New Project** dialog or pre-installed project templates. You'll need to add [additional components]({{< ref "/Setup/AdditionalComponents" >}}) and scaffolders depending on your development interests. With scaffolding tools like [Yeoman](https://yeoman.io/) and the multitude of modules available through the [npm](https://www.npmjs.com/) package manager, you're sure to find appropriate templates and tools to create your projects.

​​	VS Code 不包含传统的“文件”>“新建项目”对话框或预安装的项目模板。您需要根据您的开发兴趣添加其他组件和脚手架。借助 Yeoman 等脚手架工具和通过 npm 包管理器提供的众多模块，您一定能找到合适的模板和工具来创建项目。

### [How do I know which version I'm running? 如何知道我正在运行哪个版本？]({{< ref "/Setup/Overview#_how-do-i-know-which-version-im-running" >}})

On Linux and Windows, choose **Help** > **About**. On macOS, use **Code** > **About Visual Studio Code**.

​​	在 Linux 和 Windows 上，选择“帮助”>“关于”。在 macOS 上，使用“代码”>“关于 Visual Studio Code”。

### [Why is VS Code saying my installation is Unsupported? 为什么 VS Code 说我的安装“不受支持”？]({{< ref "/Setup/Overview#_why-is-vs-code-saying-my-installation-is-unsupported" >}})

VS Code has detected that some installation files have been modified, perhaps by an extension. Reinstalling VS Code will replace the affected files. See our [FAQ topic](https://code.visualstudio.com/docs/supporting/faq#_installation-appears-to-be-corrupt-unsupported) for more details.

​​	VS Code 检测到某些安装文件已被修改，可能是由扩展程序修改的。重新安装 VS Code 将替换受影响的文件。有关更多详细信息，请参阅我们的常见问题解答主题。

### [How can I do a 'clean' uninstall of VS Code? 如何“干净地”卸载 VS Code？]({{< ref "/Setup/Overview#_how-can-i-do-a-clean-uninstall-of-vs-code" >}})

If you want to remove all user data after [uninstalling]({{< ref "/Setup/Uninstall" >}}) VS Code, you can delete the user data folders `Code` and `.vscode`. This will return you to the state before you installed VS Code. This can also be used to reset all settings if you don't want to uninstall VS Code.

​​	如果您想在卸载 VS Code 后删除所有用户数据，可以删除用户数据文件夹 `Code` 和 `.vscode` 。这会让您回到安装 VS Code 之前状态。如果您不想卸载 VS Code，也可以使用此方法重置所有设置。

The folder locations will vary depending on your platform:

​​	文件夹位置会根据您的平台而有所不同：

- **Windows** - Delete `%APPDATA%\Code` and `%USERPROFILE%\.vscode`.
  Windows - 删除 `%APPDATA%\Code` 和 `%USERPROFILE%\.vscode` 。
- **macOS** - Delete `$HOME/Library/Application Support/Code` and `~/.vscode`.
  macOS - 删除 `$HOME/Library/Application Support/Code` 和 `~/.vscode` 。
- **Linux** - Delete `$HOME/.config/Code` and `~/.vscode`.
  Linux - 删除 `$HOME/.config/Code` 和 `~/.vscode` 。
