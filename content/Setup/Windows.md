+++
title = "Windows"
date = 2024-01-12T22:36:24+08:00
weight = 30
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/windows](https://code.visualstudio.com/docs/setup/windows)

# Visual Studio Code on Windows Windows 上的 Visual Studio Code



## [Installation 安装](https://code.visualstudio.com/docs/setup/windows#_installation)

1. Download the [Visual Studio Code installer](https://go.microsoft.com/fwlink/?LinkID=534107) for Windows.
   下载适用于 Windows 的 Visual Studio Code 安装程序。
2. Once it is downloaded, run the installer (VSCodeUserSetup-{version}.exe). This will only take a minute.
   下载后，运行安装程序 (VSCodeUserSetup-{version}.exe)。这只需要一分钟。
3. By default, VS Code is installed under `C:\Users\{Username}\AppData\Local\Programs\Microsoft VS Code`.
   默认情况下，VS Code 安装在 `C:\Users\{Username}\AppData\Local\Programs\Microsoft VS Code` 下。

Alternatively, you can also download a [Zip archive](https://code.visualstudio.com/docs/?dv=winzip), extract it and run Code from there.

​	或者，您还可以下载一个 Zip 存档，解压缩并从那里运行 Code。

> **Tip:** Setup will add Visual Studio Code to your `%PATH%`, so from the console you can type 'code .' to open VS Code on that folder. You will need to restart your console after the installation for the change to the `%PATH%` environmental variable to take effect.
>
> ​	提示：安装程序会将 Visual Studio Code 添加到您的 `%PATH%` 中，因此您可以从控制台键入“code .” 以在该文件夹中打开 VS Code。您需要在安装后重新启动控制台，才能使对 `%PATH%` 环境变量的更改生效。

## [User setup versus system setup 用户安装与系统安装](https://code.visualstudio.com/docs/setup/windows#_user-setup-versus-system-setup)

VS Code provides both Windows **user** and **system** level setups.

​	VS Code 提供 Windows 用户和系统级别的安装程序。

The [user setup](https://go.microsoft.com/fwlink/?LinkID=534107) does not require Administrator privileges to run as the location will be under your user Local AppData (`LOCALAPPDATA`) folder. Since it requires no elevation, the user setup is able to provide a smoother background update experience. This is the preferred way to install VS Code on Windows.

​	用户安装程序不需要管理员权限即可运行，因为位置将在您的用户本地 AppData ( `LOCALAPPDATA` ) 文件夹下。由于不需要提升权限，因此用户安装程序能够提供更流畅的后台更新体验。这是在 Windows 上安装 VS Code 的首选方式。

> **Note:** When running VS Code as Administrator in a user setup installation, updates will be disabled.
>
> ​	注意：在用户安装程序中以管理员身份运行 VS Code 时，更新将被禁用。

The [system setup](https://go.microsoft.com/fwlink/?linkid=852157) requires elevation to Administrator privileges to run and will place the installation under the system's Program Files. The in-product update flow will also require elevation, making it less streamlined than the user setup. On the other hand, installing VS Code using the system setup means that it will be available to all users in the system.

​	系统设置需要提升到管理员权限才能运行，并将安装程序放在系统的 Program Files 中。产品内更新流程也需要提升权限，这使得它不如用户设置那么精简。另一方面，使用系统设置安装 VS Code 意味着它将对系统中的所有用户可用。

See the [Download Visual Studio Code](https://code.visualstudio.com/download) page for a complete list of available installation options.

​	请参阅下载 Visual Studio Code 页面以获取可用安装选项的完整列表。

## [Updates 更新](https://code.visualstudio.com/docs/setup/windows#_updates)

VS Code ships monthly [releases](https://code.visualstudio.com/updates) and supports auto-update when a new release is available. If you're prompted by VS Code, accept the newest update and it will be installed (you won't need to do anything else to get the latest bits).

​	VS Code 每月发布版本，并在有新版本可用时支持自动更新。如果您收到 VS Code 的提示，请接受最新的更新，它将被安装（您无需执行任何其他操作即可获取最新位）。

> **Note:** You can [disable auto-update](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates) if you prefer to update VS Code on your own schedule.
>
> ​	注意：如果您希望按照自己的时间表更新 VS Code，则可以禁用自动更新。

## [Windows Subsystem for Linux 适用于 Linux 的 Windows 子系统](https://code.visualstudio.com/docs/setup/windows#_windows-subsystem-for-linux)

Windows is a popular operating system and it can be a great cross-platform development environment. This section describes cross-platform features such as the [Windows Subsystem for Linux](https://learn.microsoft.com/windows/wsl/install) (WSL) and the new Windows Terminal.

​	Windows 是一个流行的操作系统，它可以成为一个出色的跨平台开发环境。本部分介绍跨平台功能，例如适用于 Linux 的 Windows 子系统 (WSL) 和新的 Windows 终端。

### [Recent Windows build 最新的 Windows 版本](https://code.visualstudio.com/docs/setup/windows#_recent-windows-build)

Make sure you are on a recent Windows 10 build. Check **Settings** > **Windows Update** to see if you are up-to-date.

​	确保您使用的是最新的 Windows 10 版本。检查“设置”>“Windows 更新”以查看您是否为最新版本。

### [Windows as a developer machine Windows 作为开发计算机](https://code.visualstudio.com/docs/setup/windows#_windows-as-a-developer-machine)

With WSL, you can install and run Linux distributions on Windows. This enables you to develop and test your source code on Linux while still working locally on your Windows machine.

​	借助 WSL，您可以在 Windows 上安装并运行 Linux 发行版。这使您能够在 Linux 上开发和测试源代码，同时仍在 Windows 机器上本地工作。

When coupled with the [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) extension, you get full VS Code editing and debugging support while running in the context of WSL.

​	与 WSL 扩展结合使用时，您可以在 WSL 上下文中运行时获得完整的 VS Code 编辑和调试支持。

See the [Developing in WSL](https://code.visualstudio.com/docs/remote/wsl) documentation to learn more or try the [Working in WSL](https://code.visualstudio.com/docs/remote/wsl-tutorial) introductory tutorial.

​	请参阅在 WSL 中开发文档以了解更多信息或尝试在 WSL 中工作入门教程。

### [New Windows Terminal 新的 Windows 终端](https://code.visualstudio.com/docs/setup/windows#_new-windows-terminal)

Available from the Microsoft Store, the [Windows Terminal (Preview)](https://www.microsoft.com/p/windows-terminal-preview/9n0dx20hk701?SilentAuth=1&wa=wsignin1.0&activetab=pivot%3Aoverviewtab) lets you easily open PowerShell, Command Prompt, and WSL terminals in a multiple tab shell.

​	可从 Microsoft Store 获得的 Windows 终端（预览版）使您能够轻松地在多标签 shell 中打开命令提示符和 WSL 终端。

## [Next steps 后续步骤](https://code.visualstudio.com/docs/setup/windows#_next-steps)

Once you have installed VS Code, these topics will help you learn more about VS Code:

​	安装 VS Code 后，这些主题将帮助您详细了解 VS Code：

- [Additional Components](https://code.visualstudio.com/docs/setup/additional-components) - Learn how to install Git, Node.js, TypeScript, and tools like Yeoman.
  其他组件 - 了解如何安装 Git、Node.js、TypeScript 和 Yeoman 等工具。
- [User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) - A quick orientation to VS Code.
  用户界面 - 快速了解 VS Code。
- [User/Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings) - Learn how to configure VS Code to your preferences through settings.
  用户/工作区设置 - 了解如何通过设置将 VS Code 配置为您的首选项。
- [Tips and Tricks](https://code.visualstudio.com/docs/getstarted/tips-and-tricks) - Lets you jump right in and learn how to be productive with VS Code.
  提示和技巧 - 让您直接上手并了解如何高效使用 VS Code。

## [Common questions 常见问题](https://code.visualstudio.com/docs/setup/windows#_common-questions)

### [What command-line arguments are supported by the Windows Setup? Windows 安装程序支持哪些命令行参数？](https://code.visualstudio.com/docs/setup/windows#_what-commandline-arguments-are-supported-by-the-windows-setup)

VS Code uses [Inno Setup](https://www.jrsoftware.org/isinfo.php) to create its setup package for Windows. Thus, all the [Inno Setup command-line switches](https://www.jrsoftware.org/ishelp/index.php?topic=setupcmdline) are available for use.

​	VS Code 使用 Setup 为 Windows 创建其安装程序包。因此，所有 Setup 命令行开关均可供使用。

Additionally, you can prevent the Setup from launching VS Code after completion with `/mergetasks=!runcode`.

​	此外，您可以使用 `/mergetasks=!runcode` 来防止安装程序在完成之后启动 VS Code。

### [Scrolling is laggy and not smooth 滚动滞后且不流畅](https://code.visualstudio.com/docs/setup/windows#_scrolling-is-laggy-and-not-smooth)

On certain devices, editor scrolling is not smooth but laggy for an unpleasant experience. If you notice this issue, make sure you install the Windows 10 October 2018 update where this issue is fixed.

​	在某些设备上，编辑器滚动不流畅，而是滞后，体验不佳。如果您注意到此问题，请确保安装 Windows 10 2018 年 10 月更新，其中已修复此问题。

### [I'm having trouble with the installer 安装程序出现问题](https://code.visualstudio.com/docs/setup/windows#_im-having-trouble-with-the-installer)

Try using the [zip file](https://code.visualstudio.com/docs/?dv=winzip) instead of the installer. To use this, unzip VS Code in your `AppData\Local\Programs` folder.

​	尝试使用 zip 文件，而不是安装程序。要使用此文件，请在 `AppData\Local\Programs` 文件夹中解压缩 VS Code。

> **Note:** When VS Code is installed via a Zip file, you will need to manually update it for each [release](https://code.visualstudio.com/updates).
>
> ​	注意：通过 Zip 文件安装 VS Code 时，您需要为每个版本手动更新它。

### [Icons are missing 缺少图标](https://code.visualstudio.com/docs/setup/windows#_icons-are-missing)

I installed Visual Studio Code on my Windows 8 machine. Why are some icons not appearing in the workbench and editor?

​	我在 Windows 8 计算机上安装了 Visual Studio Code。为什么工作台和编辑器中不显示某些图标？

VS Code uses [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) icons and we have found instances where the .SVG file extension is associated with something other than `image/svg+xml`. We're considering options to fix it, but for now here's a workaround:

​	VS Code 使用 SVG 图标，我们发现某些情况下 .SVG 文件扩展名与 `image/svg+xml` 以外的其他内容相关联。我们正在考虑修复它的选项，但目前提供以下解决方法：

Using the Command Prompt:

​	使用命令提示符：

1. Open an Administrator Command Prompt.
   打开管理员命令提示符。
2. Type `REG ADD HKCR\.svg /f /v "Content Type" /t REG_SZ /d image/svg+xml`.
   键入 `REG ADD HKCR\.svg /f /v "Content Type" /t REG_SZ /d image/svg+xml` 。

Using the Registry Editor (regedit):

​	使用注册表编辑器 (regedit)：

1. Start `regedit`.
   启动 `regedit` 。
2. Open the `HKEY_CLASSES_ROOT` key.
   打开 `HKEY_CLASSES_ROOT` 项。
3. Find the `.svg` key.
   查找 `.svg` 项。
4. Set its `Content Type` Data value to `image/svg+xml`.
   将其 `Content Type` 数据值设置为 `image/svg+xml` 。
5. Exit `regedit`.
   退出 `regedit` 。

### [Unable to run as admin when AppLocker is enabled 在启用 AppLocker 时无法以管理员身份运行](https://code.visualstudio.com/docs/setup/windows#_unable-to-run-as-admin-when-applocker-is-enabled)

With the introduction of process sandboxing (discussed in this [blog post](https://code.visualstudio.com/blogs/2022/11/28/vscode-sandbox)) running as administrator is currently unsupported when AppLocker is configured due to a limitation of the runtime sandbox. If your work requires that you run VS Code from an elevated terminal, you can launch `code` with `--no-sandbox --disable-gpu-sandbox` as a workaround.

​	由于运行时沙盒的限制，在配置了 AppLocker 时，目前不支持以管理员身份运行（在此博客文章中进行了讨论）。如果您的工作要求您从提升的终端运行 VS Code，您可以将 `code` 与 `--no-sandbox --disable-gpu-sandbox` 作为解决方法一起启动。

Subscribe to [issue #122951](https://github.com/microsoft/vscode/issues/122951) to receive updates.

​	订阅问题 #122951 以接收更新。

### [Working with UNC paths 使用 UNC 路径](https://code.visualstudio.com/docs/setup/windows#_working-with-unc-paths)

Beginning with version `1.78.1`, VS Code on Windows will only allow to access UNC paths (these begin with a leading `\\`) that were either approved by the user on startup or where the host name is configured to be allowed via the new `security.allowedUNCHosts` setting.

​	从版本 `1.78.1` 开始，Windows 上的 VS Code 将只允许访问 UNC 路径（以 `\\` 开头），这些路径要么在启动时得到用户批准，要么将主机名配置为允许通过新的 `security.allowedUNCHosts` 设置进行访问。

If you rely on using UNC paths in VS Code, you can either

​	如果您依赖于在 VS Code 中使用 UNC 路径，您可以

- configure the host to be allowed via the `security.allowedUNCHosts` setting (for example add `server-a` when you open a path such as `\\server-a\path`)
  通过 `security.allowedUNCHosts` 设置将主机配置为允许（例如，当您打开诸如 `\\server-a\path` 之类的路径时添加 `server-a` ）
- map the UNC path as netwo[vscode_docs_240113.html](..%2F..%2F..%2F..%2Ffort%2Fpublic%2Fvscode_docs_240113.html)rk drive and use the drive letter instead of the UNC path ([documentation](https://support.microsoft.com/en-us/windows/map-a-network-drive-in-windows-29ce55d1-34e3-a7e2-4801-131475f9557d))
  将 UNC 路径映射为网络驱动器，并使用驱动器号代替 UNC 路径（文档）
- define a global environment variable `NODE_UNC_HOST_ALLOWLIST` with the backslash-separated list of hostnames to allow, for example: `server-a\server-b` to allow the hosts `server-a` and `server-b`.
  定义一个全局环境变量 `NODE_UNC_HOST_ALLOWLIST` ，其中包含允许的主机名的以反斜杠分隔的列表，例如： `server-a\server-b` 以允许主机 `server-a` 和 `server-b` 。

*Note:* if you are using any of the remote extensions to connect to a workspace remotely (such as SSH), the `security.allowedUNCHosts` has to be configured on the remote machine and not the local machine.

​	注意：如果您使用任何远程扩展名来远程连接到工作区（例如 SSH），则必须在远程计算机上配置 `security.allowedUNCHosts` ，而不是在本地计算机上配置。

This change was done to improve the security when using VS Code with UNC paths. Please refer to the associated [security advisory](https://github.com/microsoft/vscode/security/advisories/GHSA-mmfh-4pv3-39hr) for more information.

​	此更改是为了提高使用 VS Code 和 UNC 路径时的安全性。有关更多信息，请参阅关联的安全公告。
