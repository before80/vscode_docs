+++
title = "Uninstall"
date = 2024-01-12T22:36:24+08:00
weight = 80
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/uninstall](https://code.visualstudio.com/docs/setup/uninstall)

# Uninstall Visual Studio Code 卸载 Visual Studio Code



The steps for uninstalling Visual Studio Code will depend on your platform (Windows, macOS, or Linux) and the install option that you used. For example on Windows, you can use the System or User Windows Installers or download a `.zip` file and extract the contents anywhere on your machine.

​​​	卸载 Visual Studio Code 的步骤取决于你的平台（Windows、macOS 或 Linux）以及你使用的安装选项。例如，在 Windows 上，你可以使用系统或用户 Windows 安装程序，或下载一个 `.zip` 文件并将内容解压到你的计算机上的任意位置。

In general, you would uninstall VS Code as you would any other desktop application and follow your platform's recommended flow for uninstalling software. Specific platform guidance is provided below as well as how to [completely clean up](https://code.visualstudio.com/docs/setup/uninstall#_clean-uninstall) any remaining VS Code configuration files.

​​​	通常，你可以像卸载任何其他桌面应用程序一样卸载 VS Code，并按照你的平台推荐的软件卸载流程进行操作。下面提供了特定平台的指导，以及如何彻底清理任何剩余的 VS Code 配置文件。

## [Windows](https://code.visualstudio.com/docs/setup/uninstall#_windows)

### [Windows Installer Windows 安装程序](https://code.visualstudio.com/docs/setup/uninstall#_windows-installer)

If you installed VS Code via the Windows Installer, either the User or System version, use the installer to remove VS Code.

​​​	如果你通过 Windows 安装程序（用户版或系统版）安装了 VS Code，请使用该安装程序来移除 VS Code。

- Start menu

  
  开始菜单

  - Search for **Add or Remove Programs** and find Visual Studio Code in the **Apps** > **Apps & features** list.
    搜索“添加或删除程序”，并在“应用”>“应用和功能”列表中找到 Visual Studio Code。
  - Select **Uninstall** from the actions dropdown on the right side (three vertical dots).
    从右侧的操作下拉菜单（三个垂直点）中选择“卸载”。
  - Follow the prompts to uninstall VS Code.
    按照提示卸载 VS Code。

- Control Panel

  
  控制面板

  - Under **Programs**, select the **Uninstall a program** link.
    在“程序”下，选择“卸载程序”链接。
  - Find the Visual Studio Code entry, right-click, and select the **Uninstall** command.
    找到 Visual Studio Code 条目，右键单击，然后选择“卸载”命令。
  - Follow the prompts to uninstall VS Code.
    按照提示卸载 VS Code。

### [.zip file installation .zip 文件安装](https://code.visualstudio.com/docs/setup/uninstall#_zip-file-installation)

If you installed VS Code on Windows by downloading and extracting one of the `.zip` files found on the [Visual Studio Code website](https://code.visualstudio.com/#alt-downloads), you can uninstall by deleting the folder where you extracted the `.zip` contents.

​​​	如果您通过下载并解压 Visual Studio Code 网站上找到的 `.zip` 文件之一在 Windows 上安装了 VS Code，则可以通过删除解压 `.zip` 内容的文件夹来卸载。

## [macOS](https://code.visualstudio.com/docs/setup/uninstall#_macos)

To uninstall VS Code on macOS, open **Finder** and go to **Applications**. Right-click on the Visual Studio Code application and select **Move to Trash**.

​​​	要在 macOS 上卸载 VS Code，请打开 Finder 并转到应用程序。右键单击 Visual Studio Code 应用程序，然后选择“移至废纸篓”。

## [Linux](https://code.visualstudio.com/docs/setup/uninstall#_linux)

To uninstall VS Code on Linux, you should use your package manager's uninstall or remove option. The exact command line will differ depending on which package manager you used (for example, `apt-get`, `rpn`, `dnf`, `yum`, etc.).

​​​	要在 Linux 上卸载 VS Code，您应该使用包管理器的卸载或删除选项。确切的命令行会根据您使用的包管理器而有所不同（例如， `apt-get` 、 `rpn` 、 `dnf` 、 `yum` 等）。

The names for the VS Code packages are:

​​​	VS Code 包的名称为：

- `code` - VS Code Stable release
  `code` - VS Code 稳定版
- `code-insiders` - VS Code [Insiders](https://code.visualstudio.com/insiders) release
  `code-insiders` - VS Code 预览版

For example, if you installed VS Code via the Debian package (`.deb`) and `apt-get` package manager, you would run:

​​​	例如，如果您通过 Debian 包 ( `.deb` ) 和 `apt-get` 包管理器安装了 VS Code，则您将运行：

```
sudo apt-get remove code
```

where `code` is the name of the VS Code Debian package.

​​​	其中 `code` 是 VS Code Debian 包的名称。

## [Clean uninstall 彻底卸载](https://code.visualstudio.com/docs/setup/uninstall#_clean-uninstall)

If you want to remove all user data after uninstalling VS Code, you can delete the user data folders `Code` and `.vscode`. This will return you to the state before you installed VS Code. This can also be used to reset all settings if you don't want to uninstall VS Code.

​​​	如果您想在卸载 VS Code 后删除所有用户数据，则可以删除用户数据文件夹 `Code` 和 `.vscode` 。这会让您回到安装 VS Code 之前状态。如果您不想卸载 VS Code，也可以使用此方法重置所有设置。

The folder locations will vary depending on your platform:

​​​	文件夹位置会根据您的平台而有所不同：

- **Windows** - Delete `%APPDATA%\Code` and `%USERPROFILE%\.vscode`.
  Windows - 删除 `%APPDATA%\Code` 和 `%USERPROFILE%\.vscode` 。
- **macOS** - Delete `$HOME/Library/Application Support/Code` and `~/.vscode`.
  macOS - 删除 `$HOME/Library/Application Support/Code` 和 `~/.vscode` 。
- **Linux** - Delete `$HOME/.config/Code` and `~/.vscode`.
  Linux - 删除 `$HOME/.config/Code` 和 `~/.vscode` 。

## [Next steps 后续步骤](https://code.visualstudio.com/docs/setup/uninstall#_next-steps)

- [Setup overview](https://code.visualstudio.com/docs/setup/setup-overview) - General information about VS Code setup and updates.
  设置概述 - 有关 VS Code 设置和更新的常规信息。
- [Windows setup](https://code.visualstudio.com/docs/setup/windows) - Details and common questions about installing VS Code on Windows.
  Windows 设置 - 有关在 Windows 上安装 VS Code 的详细信息和常见问题。
- [macOS setup](https://code.visualstudio.com/docs/setup/mac) - VS Code is available for both Intel and Apple silicon macOS machines.
  macOS 设置 - VS Code 适用于 Intel 和 Apple 芯片 macOS 电脑。
- [Linux setup](https://code.visualstudio.com/docs/setup/linux) - Learn about the different VS Code packages available for Linux.
  Linux 设置 - 了解适用于 Linux 的不同 VS Code 软件包。
