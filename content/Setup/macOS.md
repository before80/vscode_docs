+++
title = "macOS"
date = 2024-01-12T22:36:24+08:00
weight = 20
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/mac](https://code.visualstudio.com/docs/setup/mac)

# Visual Studio Code on macOS macOS 上的 Visual Studio Code



## [Installation 安装]({{< ref "/Setup/macOS#_installation" >}})

1. [Download Visual Studio Code](https://go.microsoft.com/fwlink/?LinkID=534106) for macOS.
   下载适用于 macOS 的 Visual Studio Code。
2. Open the browser's download list and locate the downloaded app or archive.
   打开浏览器的下载列表并找到下载的应用程序或存档。
3. If archive, extract the archive contents. Use double-click for some browsers or select the 'magnifying glass' icon with Safari.
   如果是存档，则提取存档内容。对于某些浏览器，请双击或使用 Safari 选择“放大镜”图标。
4. Drag `Visual Studio Code.app` to the **Applications** folder, making it available in the macOS Launchpad.
   将 `Visual Studio Code.app` 拖到应用程序文件夹，使其在 macOS 启动台中可用。
5. Open VS Code from the **Applications** folder, by double clicking the icon.
   通过双击图标，从应用程序文件夹中打开 VS Code。
6. Add VS Code to your Dock by right-clicking on the icon, located in the Dock, to bring up the context menu and choosing **Options**, **Keep in Dock**.
   右键单击 Dock 中的图标，调出上下文菜单并选择“选项”和“保留在 Dock 中”，将 VS Code 添加到 Dock 中。

## [Launching from the command line 从命令行启动]({{< ref "/Setup/macOS#_launching-from-the-command-line" >}})

You can also run VS Code from the terminal by typing 'code' after adding it to the path:

​​​	您还可以在将 VS Code 添加到路径后，通过在终端中键入“code”来运行 VS Code：

- Launch VS Code.
  启动 VS Code。
- Open the **Command Palette** (Cmd+Shift+P) and type 'shell command' to find the **Shell Command: Install 'code' command in PATH** command.
  打开命令面板 (Cmd+Shift+P) 并键入“shell 命令”以查找 Shell 命令：在 PATH 命令中安装“code”命令。

![macOS shell commands](./macOS_img/shell-command.png)

- Restart the terminal for the new `$PATH` value to take effect. You'll be able to type 'code .' in any folder to start editing files in that folder.
  重新启动终端以使新的 `$PATH` 值生效。您将能够在任何文件夹中键入“code .”以开始编辑该文件夹中的文件。

> **Note:** If you still have the old `code` alias in your `.bash_profile` (or equivalent) from an early VS Code version, remove it and replace it by executing the **Shell Command: Install 'code' command in PATH** command.
>
> ​​​	注意：如果您在早期版本的 VS Code 中的 `.bash_profile` （或等效版本）中仍然有旧的 `code` 别名，请将其删除并通过执行 Shell 命令：在 PATH 命令中安装“code”命令来替换它。

### [Alternative manual instructions 备选的手动说明]({{< ref "/Setup/macOS#_alternative-manual-instructions" >}})

Instead of running the command above, you can manually add VS Code to your path, to do so run the following commands:

​​​	您可以手动将 VS Code 添加到您的路径中，而不是运行上述命令，为此，请运行以下命令：

```
cat << EOF >> ~/.bash_profile
# Add Visual Studio Code (code)
export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
EOF
```

Start a new terminal to pick up your `.bash_profile` changes.

​​​	启动一个新的终端来获取您的 `.bash_profile` 更改。

**Note**: The leading slash `\` is required to prevent `$PATH` from expanding during the concatenation. Remove the leading slash if you want to run the export command directly in a terminal.

​​​	注意：需要前导斜杠 `\` 以防止 `$PATH` 在连接期间展开。如果您想直接在终端中运行 export 命令，请删除前导斜杠。

**Note**: Since `zsh` became the default shell in macOS Catalina, run the following commands to add VS Code to your path:

​​​	注意：由于 `zsh` 已成为 macOS Catalina 中的默认 shell，因此请运行以下命令将 VS Code 添加到您的路径中：

```
cat << EOF >> ~/.zprofile
# Add Visual Studio Code (code)
export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
EOF
```

## [Touch Bar support 触控栏支持]({{< ref "/Setup/macOS#_touch-bar-support" >}})

Out of the box VS Code adds actions to navigate in editor history as well as the full Debug tool bar to control the debugger on your Touch Bar:

​​​	开箱即用的 VS Code 会添加操作以在编辑器历史记录中导航，以及完整的调试工具栏以控制触控栏上的调试器：

![macOS Touch Bar](./macOS_img/touchbar.gif)

## [Mojave privacy protections Mojave 隐私保护]({{< ref "/Setup/macOS#_mojave-privacy-protections" >}})

After upgrading to macOS Mojave version, you may see dialogs saying "Visual Studio Code would like to access your {calendar/contacts/photos}." This is due to the new privacy protections in Mojave and is not specific to VS Code. The same dialogs may be displayed when running other applications as well. The dialog is shown once for each type of personal data and it is fine to choose **Don't Allow** since VS Code does not need access to those folders.

​​​	升级到 macOS Mojave 版本后，您可能会看到提示“Visual Studio Code 想要访问您的 {日历/联系人/照片}”的对话框。这是由于 Mojave 中的新隐私保护措施所致，并非 VS Code 特有。运行其他应用程序时也可能会显示相同的对话框。此对话框针对每种类型的个人数据显示一次，选择“不允许”是可以的，因为 VS Code 无需访问这些文件夹。

## [Updates 更新]({{< ref "/Setup/macOS#_updates" >}})

VS Code ships monthly [releases](https://code.visualstudio.com/updates) and supports auto-update when a new release is available. If you're prompted by VS Code, accept the newest update and it will get installed (you won't need to do anything else to get the latest bits).

​​​	VS Code 每月发布版本，并在有新版本可用时支持自动更新。如果 VS Code 提示您，请接受最新的更新，它将得到安装（您无需执行任何其他操作即可获取最新版本）。

> Note: You can [disable auto-update](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates) if you prefer to update VS Code on your own schedule.
>
> ​​​	注意：如果您希望按照自己的计划更新 VS Code，则可以禁用自动更新。

## [Preferences menu 首选项菜单]({{< ref "/Setup/macOS#_preferences-menu" >}})

You can configure VS Code through [settings]({{< ref "/GetStarted/Settings" >}}), [color themes]({{< ref "/GetStarted/Themes" >}}), and [custom keybindings]({{< ref "/GetStarted/KeyBindings" >}}) available through the **File** > **Preferences** menu group.

​​​	您可以通过“文件”>“首选项”菜单组中提供的设置、颜色主题和自定义键绑定来配置 VS Code。

## [Next steps 后续步骤]({{< ref "/Setup/macOS#_next-steps" >}})

Once you have installed VS Code, these topics will help you learn more about VS Code:

​​​	安装 VS Code 后，这些主题将帮助您详细了解 VS Code：

- [Additional Components]({{< ref "/Setup/AdditionalComponents" >}}) - Learn how to install Git, Node.js, TypeScript, and tools like Yeoman.
  其他组件 - 了解如何安装 Git、Node.js、TypeScript 和 Yeoman 等工具。
- [User Interface]({{< ref "/GetStarted/UserInterface" >}}) - A quick orientation around VS Code.
  用户界面 - VS Code 的快速入门。
- [User/Workspace Settings]({{< ref "/GetStarted/Settings" >}}) - Learn how to configure VS Code to your preferences settings.
  用户/工作区设置 - 了解如何将 VS Code 配置为您的首选项设置。

## [Common questions 常见问题]({{< ref "/Setup/macOS#_common-questions" >}})

### [Why do I see "Visual Studio Code would like access to your calendar." 为什么我看到“Visual Studio Code 想要访问您的日历”。]({{< ref "/Setup/macOS#_why-do-i-see-visual-studio-code-would-like-access-to-your-calendar" >}})

If you are running macOS Mojave version, you may see dialogs saying "Visual Studio Code would like to access your {calendar/contacts/photos}." This is due to the new privacy protections in Mojave [discussed above]({{< ref "/Setup/macOS#_mojave-privacy-protections" >}}). It is fine to choose **Don't Allow** since VS Code does not need access to those folders.

​​​	如果您运行的是 macOS Mojave 版本，您可能会看到对话框，提示“Visual Studio Code 想要访问您的 {日历/联系人/照片}”。这是由于 Mojave 中讨论的新隐私保护。选择“不允许”是可以的，因为 VS Code 不需要访问这些文件夹。

### [VS Code fails to update VS Code 无法更新]({{< ref "/Setup/macOS#_vs-code-fails-to-update" >}})

If VS Code doesn't update once it restarts, it might be set under quarantine by macOS. Follow the steps in this [issue](https://github.com/microsoft/vscode/issues/7426#issuecomment-425093469) for resolution.

​​​	如果 VS Code 在重新启动后无法更新，它可能被 macOS 隔离了。按照此问题中的步骤进行解决。

### [Does VS Code run on Apple silicon machines? VS Code 是否可以在 Apple 芯片电脑上运行？]({{< ref "/Setup/macOS#_does-vs-code-run-on-apple-silicon-machines" >}})

Yes, VS Code supports macOS Arm64 builds that can run on Macs with the Apple silicon chipsets. You can install the Universal build, which includes both Intel and Apple silicon builds, or one of the platform specific builds.

​​​	是的，VS Code 支持可以在搭载 Apple 芯片的 Mac 上运行的 macOS Arm64 版本。您可以安装通用版本（包括 Intel 和 Apple 芯片版本）或其中一个特定于平台的版本。
