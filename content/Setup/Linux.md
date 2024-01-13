+++
title = "Linux"
date = 2024-01-12T22:36:24+08:00
weight = 10
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/linux](https://code.visualstudio.com/docs/setup/linux)

# Visual Studio Code on Linux Visual Studio Code 在 Linux 上



## [Installation 安装](https://code.visualstudio.com/docs/setup/linux#_installation)

See the [Download Visual Studio Code](https://code.visualstudio.com/download) page for a complete list of available installation options.

&zeroWidthSpace;有关可用安装选项的完整列表，请参阅下载 Visual Studio Code 页面。

By downloading and using Visual Studio Code, you agree to the [license terms](https://code.visualstudio.com/license) and [privacy statement](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

&zeroWidthSpace;通过下载和使用 Visual Studio Code，您同意许可条款和隐私声明。

### [Debian and Ubuntu based distributions 基于 Debian 和 Ubuntu 的发行版](https://code.visualstudio.com/docs/setup/linux#_debian-and-ubuntu-based-distributions)

The easiest way to install Visual Studio Code for Debian/Ubuntu based distributions is to download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868), either through the graphical software center if it's available, or through the command line with:

&zeroWidthSpace;在基于 Debian/Ubuntu 的发行版上安装 Visual Studio Code 的最简单方法是下载并安装 .deb 软件包（64 位），可以通过图形软件中心（如果可用）或通过命令行下载并安装，如下所示：

```
sudo apt install ./<file>.deb

# If you're on an older Linux distribution, you will need to run this instead:
# sudo dpkg -i <file>.deb
# sudo apt-get install -f # Install dependencies
```

Note that other binaries are also available on the [VS Code download page](https://code.visualstudio.com/Download).

&zeroWidthSpace;请注意，VS Code 下载页面上还提供了其他二进制文件。

Installing the .deb package will automatically install the apt repository and signing key to enable auto-updating using the system's package manager. Alternatively, the repository and key can also be installed manually with the following script:

&zeroWidthSpace;安装 .deb 软件包将自动安装 apt 存储库和签名密钥，以使用系统的软件包管理器启用自动更新。或者，还可以使用以下脚本手动安装存储库和密钥：

```
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
```

Then update the package cache and install the package using:

&zeroWidthSpace;然后更新软件包缓存并使用以下命令安装软件包：

```
sudo apt install apt-transport-https
sudo apt update
sudo apt install code # or code-insiders
```

### [RHEL, Fedora, and CentOS based distributions 基于 RHEL、Fedora 和 CentOS 的发行版](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)

We currently ship the stable 64-bit VS Code in a yum repository, the following script will install the key and repository:

&zeroWidthSpace;我们目前在 yum 存储库中提供稳定的 64 位 VS Code，以下脚本将安装密钥和存储库：

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

Then update the package cache and install the package using `dnf` (Fedora 22 and above):

&zeroWidthSpace;然后更新软件包缓存并使用 `dnf` （Fedora 22 及更高版本）安装软件包：

```
dnf check-update
sudo dnf install code # or code-insiders
```

Or on older versions using `yum`:

&zeroWidthSpace;或在使用 `yum` 的旧版本上：

```
yum check-update
sudo yum install code # or code-insiders
```

Due to the manual signing process and the system we use to publish, the yum repo may lag behind and not get the latest version of VS Code immediately.

&zeroWidthSpace;由于手动签名过程和我们用于发布的系统，yum 存储库可能会滞后，无法立即获取最新版本的 VS Code。

### [Snap](https://code.visualstudio.com/docs/setup/linux#_snap)

Visual Studio Code is officially distributed as a Snap package in the [Snap Store](https://snapcraft.io/store):

&zeroWidthSpace;Visual Studio Code 在 Snap 商店中正式分发为 Snap 软件包：

[![Get it from the Snap Store](https://code.visualstudio.com/assets/docs/setup/linux/snap-store.png)](https://snapcraft.io/code)

You can install it by running:

&zeroWidthSpace;您可以通过运行以下命令进行安装：

```
sudo snap install --classic code # or code-insiders
```

Once installed, the Snap daemon will take care of automatically updating VS Code in the background. You will get an in-product update notification whenever a new update is available.

&zeroWidthSpace;安装后，Snap 后台程序将负责在后台自动更新 VS Code。每当有新更新可用时，您都将收到产品内更新通知。

**Note:** If `snap` isn't available in your Linux distribution, please check the following [Installing snapd guide](https://docs.snapcraft.io/installing-snapd), which can help you get that set up.

&zeroWidthSpace;注意：如果 `snap` 在您的 Linux 发行版中不可用，请查看以下安装 snapd 指南，它可以帮助您进行设置。

Learn more about snaps from the [official Snap Documentation](https://docs.snapcraft.io/).

&zeroWidthSpace;从官方 Snap 文档中了解有关 snap 的更多信息。

### [openSUSE and SLE-based distributions 基于 openSUSE 和 SLE 的发行版](https://code.visualstudio.com/docs/setup/linux#_opensuse-and-slebased-distributions)

The yum repository above also works for openSUSE and SLE-based systems, the following script will install the key and repository:

&zeroWidthSpace;上述 yum 存储库也适用于基于 openSUSE 和 SLE 的系统，以下脚本将安装密钥和存储库：

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
```

Then update the package cache and install the package using:

&zeroWidthSpace;然后更新软件包缓存并使用以下命令安装软件包：

```
sudo zypper refresh
sudo zypper install code
```

### [AUR package for Arch Linux 适用于 Arch Linux 的 AUR 软件包](https://code.visualstudio.com/docs/setup/linux#_aur-package-for-arch-linux)

There is a community-maintained [Arch User Repository package for VS Code](https://aur.archlinux.org/packages/visual-studio-code-bin).

&zeroWidthSpace;有一个由社区维护的适用于 VS Code 的 Arch 用户存储库软件包。

To get more information about the installation from the AUR, please consult the following wiki entry: [Install AUR Packages](https://wiki.archlinux.org/index.php/Arch_User_Repository#Build_and_install_the_package).

&zeroWidthSpace;要获取有关从 AUR 安装的更多信息，请参阅以下 wiki 条目：安装 AUR 软件包。

### [Nix package for NixOS (or any Linux distribution using Nix package manager) 适用于 NixOS（或任何使用 Nix 软件包管理器的 Linux 发行版）的 Nix 软件包](https://code.visualstudio.com/docs/setup/linux#_nix-package-for-nixos-or-any-linux-distribution-using-nix-package-manager)

There is a community maintained [VS Code Nix package](https://github.com/NixOS/nixpkgs/blob/master/pkgs/applications/editors/vscode/vscode.nix) in the nixpkgs repository. In order to install it using Nix, set `allowUnfree` option to true in your `config.nix` and execute:

&zeroWidthSpace;在 nixpkgs 存储库中有一个由社区维护的 VS Code Nix 软件包。要使用 Nix 安装它，请将 `allowUnfree` 选项设置为 true，并在 `config.nix` 中执行：

```
nix-env -i vscode
```

### [Installing .rpm package manually 手动安装 .rpm 软件包](https://code.visualstudio.com/docs/setup/linux#_installing-rpm-package-manually)

The [VS Code .rpm package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760867) can also be manually downloaded and installed, however, auto-updating won't work unless the repository above is installed. Once downloaded it can be installed using your package manager, for example with `dnf`:

&zeroWidthSpace;VS Code .rpm 软件包（64 位）也可以手动下载和安装，但是，除非安装了上述存储库，否则自动更新将不起作用。下载后，可以使用软件包管理器安装它，例如使用 `dnf` ：

```
sudo dnf install <file>.rpm
```

Note that other binaries are also available on the [VS Code download page](https://code.visualstudio.com/Download).

&zeroWidthSpace;请注意，VS Code 下载页面上还提供了其他二进制文件。

## [Updates 更新](https://code.visualstudio.com/docs/setup/linux#_updates)

VS Code ships monthly and you can see when a new release is available by checking the [release notes](https://code.visualstudio.com/updates). If the VS Code repository was installed correctly, then your system package manager should handle auto-updating in the same way as other packages on the system.

&zeroWidthSpace;VS Code 每月发布，您可以通过查看发行说明来了解何时有新版本可用。如果 VS Code 存储库已正确安装，那么您的系统包管理器应以与系统上其他包相同的方式处理自动更新。

**Note:** Updates are automatic and run in the background for the [Snap package](https://code.visualstudio.com/docs/setup/linux#_snap).

&zeroWidthSpace;注意：对于 Snap 包，更新是自动的，并在后台运行。

## [Node.js](https://code.visualstudio.com/docs/setup/linux#_nodejs)

Node.js is a popular platform and runtime for easily building and running JavaScript applications. It also includes [npm](https://www.npmjs.com/), a Package Manager for Node.js modules. You'll see Node.js and npm mentioned frequently in our documentation and some optional VS Code tooling requires Node.js (for example, the VS Code [extension generator](https://code.visualstudio.com/api/get-started/your-first-extension)).

&zeroWidthSpace;Node.js 是一个流行的平台和运行时，可轻松构建和运行 JavaScript 应用程序。它还包括 npm，一个 Node.js 模块的包管理器。您将在我们的文档中经常看到提及 Node.js 和 npm，并且一些可选的 VS Code 工具需要 Node.js（例如，VS Code 扩展生成器）。

If you'd like to install Node.js on Linux, see [Installing Node.js via package manager](https://nodejs.org/en/download/package-manager) to find the Node.js package and installation instructions tailored to your Linux distribution. You can also install and support multiple versions of Node.js by using the [Node Version Manager](https://github.com/creationix/nvm).

&zeroWidthSpace;如果您想在 Linux 上安装 Node.js，请参阅通过包管理器安装 Node.js 以查找适用于您的 Linux 发行版的 Node.js 包和安装说明。您还可以使用 Node 版本管理器来安装和支持多个版本的 Node.js。

To learn more about JavaScript and Node.js, see our [Node.js tutorial](https://code.visualstudio.com/docs/nodejs/nodejs-tutorial), where you'll learn about running and debugging Node.js applications with VS Code.

&zeroWidthSpace;要详细了解 JavaScript 和 Node.js，请参阅我们的 Node.js 教程，您将在其中学习如何使用 VS Code 运行和调试 Node.js 应用程序。

## [Setting VS Code as the default text editor 将 VS Code 设置为默认文本编辑器](https://code.visualstudio.com/docs/setup/linux#_setting-vs-code-as-the-default-text-editor)

### [xdg-open](https://code.visualstudio.com/docs/setup/linux#_xdgopen)

You can set the default text editor for text files (`text/plain`) that is used by `xdg-open` with the following command:

&zeroWidthSpace;您可以使用以下命令为 `xdg-open` 使用的文本文件 ( `text/plain` ) 设置默认文本编辑器：

```
xdg-mime default code.desktop text/plain
```

### [Debian alternatives system Debian 备选系统](https://code.visualstudio.com/docs/setup/linux#_debian-alternatives-system)

Debian-based distributions allow setting a default **editor** using the [Debian alternatives system](https://wiki.debian.org/DebianAlternatives), without concern for the MIME type. You can set this by running the following and selecting code:

&zeroWidthSpace;基于 Debian 的发行版允许使用 Debian 备选系统设置默认编辑器，而无需考虑 MIME 类型。您可以通过运行以下命令并选择代码来设置此项：

```
sudo update-alternatives --set editor /usr/bin/code
```

If Visual Studio Code doesn't show up as an alternative to `editor`, you need to register it:

&zeroWidthSpace;如果 Visual Studio Code 未显示为 `editor` 的备选方案，您需要注册它：

```
sudo update-alternatives --install /usr/bin/editor editor $(which code) 10
```

## [Windows as a Linux developer machine Windows 作为 Linux 开发人员计算机](https://code.visualstudio.com/docs/setup/linux#_windows-as-a-linux-developer-machine)

Another option for Linux development with VS Code is to use a Windows machine with the [Windows Subsystem for Linux](https://learn.microsoft.com/windows/wsl/install) (WSL).

&zeroWidthSpace;使用 VS Code 进行 Linux 开发的另一个选择是使用装有适用于 Linux 的 Windows 子系统 (WSL) 的 Windows 计算机。

### [Windows Subsystem for Linux 适用于 Linux 的 Windows 子系统](https://code.visualstudio.com/docs/setup/linux#_windows-subsystem-for-linux)

With WSL, you can install and run Linux distributions on Windows. This enables you to develop and test your source code on Linux while still working locally on a Windows machine. WSL supports Linux distributions such as Ubuntu, Debian, SUSE, and Alpine available from the Microsoft Store.

&zeroWidthSpace;使用 WSL，您可以在 Windows 上安装并运行 Linux 发行版。这使您能够在 Linux 上开发和测试源代码，同时仍在 Windows 计算机上本地工作。WSL 支持从 Microsoft Store 获取的 Linux 发行版，例如 Ubuntu、Debian、SUSE 和 Alpine。

When coupled with the [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) extension, you get full VS Code editing and debugging support while running in the context of a Linux distro on WSL.

&zeroWidthSpace;与 WSL 扩展结合使用时，您可以在 WSL 上的 Linux 发行版环境中运行时获得完整的 VS Code 编辑和调试支持。

See the [Developing in WSL](https://code.visualstudio.com/docs/remote/wsl) documentation to learn more or try the [Working in WSL](https://code.visualstudio.com/docs/remote/wsl-tutorial) introductory tutorial.

&zeroWidthSpace;请参阅在 WSL 中进行开发文档以了解更多信息或尝试在 WSL 中工作入门教程。

## [Next steps 后续步骤](https://code.visualstudio.com/docs/setup/linux#_next-steps)

Once you have installed VS Code, these topics will help you learn more about it:

&zeroWidthSpace;安装 VS Code 后，以下主题将帮助您详细了解它：

- [Additional Components](https://code.visualstudio.com/docs/setup/additional-components) - Learn how to install Git, Node.js, TypeScript, and tools like Yeoman.
  其他组件 - 了解如何安装 Git、Node.js、TypeScript 和 Yeoman 等工具。
- [User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) - A quick orientation to VS Code.
  用户界面 - VS Code 的快速入门。
- [User/Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings) - Learn how to configure VS Code to your preferences through settings.
  用户/工作区设置 - 了解如何通过设置将 VS Code 配置为您的首选项。

## [Common questions 常见问题](https://code.visualstudio.com/docs/setup/linux#_common-questions)

### [Azure VM Issues Azure VM 问题](https://code.visualstudio.com/docs/setup/linux#_azure-vm-issues)

I'm getting a "Running without the SUID sandbox" error?

&zeroWidthSpace;我收到“在没有 SUID 沙盒的情况下运行”错误？

You can safely ignore this error.

&zeroWidthSpace;您可以安全地忽略此错误。

### [Debian and moving files to trash Debian 和将文件移动到回收站](https://code.visualstudio.com/docs/setup/linux#_debian-and-moving-files-to-trash)

If you see an error when deleting files from the VS Code Explorer on the Debian operating system, it might be because the trash implementation that VS Code is using is not there.

&zeroWidthSpace;如果您在 Debian 操作系统上的 VS Code 资源管理器中删除文件时看到错误，则可能是因为 VS Code 使用的回收站实现不存在。

Run these commands to solve this issue:

&zeroWidthSpace;运行以下命令来解决此问题：

```
sudo apt-get install gvfs libglib2.0-bin
```

### [Conflicts with VS Code packages from other repositories 与其他存储库中的 VS Code 软件包发生冲突](https://code.visualstudio.com/docs/setup/linux#_conflicts-with-vs-code-packages-from-other-repositories)

Some distributions, for example [Pop!_OS](https://pop.system76.com/) provide their own `code` package. To ensure the official VS Code repository is used, create a file named `/etc/apt/preferences.d/code` with the following content:

&zeroWidthSpace;某些发行版（例如 Pop!_OS）提供自己的 `code` 软件包。为确保使用官方 VS Code 存储库，请创建一个名为 `/etc/apt/preferences.d/code` 的文件，其中包含以下内容：

```
Package: code
Pin: origin "packages.microsoft.com"
Pin-Priority: 9999
```

### ["Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC) “Visual Studio Code 无法监视此大型工作区中的文件更改”（错误 ENOSPC）](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)

When you see this notification, it indicates that the VS Code file watcher is running out of handles because the workspace is large and contains many files. Before adjusting platform limits, make sure that potentially large folders, such as Python `.venv`, are added to the `files.watcherExclude` setting (more details below). The current limit can be viewed by running:

&zeroWidthSpace;当您看到此通知时，表示 VS Code 文件监视器正在耗尽句柄，因为工作区很大且包含许多文件。在调整平台限制之前，请确保将可能较大的文件夹（例如 Python `.venv` ）添加到 `files.watcherExclude` 设置中（更多详细信息如下）。可以通过运行以下命令查看当前限制：

```
cat /proc/sys/fs/inotify/max_user_watches
```

The limit can be increased to its maximum by editing `/etc/sysctl.conf` (except on Arch Linux, read below) and adding this line to the end of the file:

&zeroWidthSpace;可以通过编辑 `/etc/sysctl.conf` 将限制增加到最大值（在 Arch Linux 上除外，请参阅下文），并在文件末尾添加此行：

```
fs.inotify.max_user_watches=524288
```

The new value can then be loaded in by running `sudo sysctl -p`.

&zeroWidthSpace;然后可以通过运行 `sudo sysctl -p` 加载新值。

While 524,288 is the maximum number of files that can be watched, if you're in an environment that is particularly memory constrained, you may want to lower the number. Each file watch [takes up 1080 bytes](https://stackoverflow.com/a/7091897/1156119), so assuming that all 524,288 watches are consumed, that results in an upper bound of around 540 MiB.

&zeroWidthSpace;虽然 524,288 是可以监视的文件的最大数量，但如果您身处内存特别受限的环境中，您可能希望降低此数量。每个文件监视占用 1080 字节，因此假设消耗了所有 524,288 个监视，则上限约为 540 MiB。

[Arch](https://www.archlinux.org/)-based distros (including Manjaro) require you to change a different file; follow [these steps](https://gist.github.com/tbjgolden/c53ca37f3bc2fab8c930183310918c8c) instead.

&zeroWidthSpace;基于 Arch 的发行版（包括 Manjaro）要求您更改不同的文件；请改而执行以下步骤。

Another option is to exclude specific workspace directories from the VS Code file watcher with the `files.watcherExclude` [setting](https://code.visualstudio.com/docs/getstarted/settings). The default for `files.watcherExclude` excludes `node_modules` and some folders under `.git`, but you can add other directories that you don't want VS Code to track.

&zeroWidthSpace;另一个选项是使用 `files.watcherExclude` 设置从 VS Code 文件监视器中排除特定的工作区目录。 `files.watcherExclude` 的默认值排除 `node_modules` 和 `.git` 下的某些文件夹，但您可以添加您不希望 VS Code 跟踪的其他目录。

```
"files.watcherExclude": {
    "**/.git/objects/**": true,
    "**/.git/subtree-cache/**": true,
    "**/node_modules/*/**": true
  }
```

### [I can't see Chinese characters in Ubuntu 我在 Ubuntu 中看不到中文字符](https://code.visualstudio.com/docs/setup/linux#_i-cant-see-chinese-characters-in-ubuntu)

We're working on a fix. In the meantime, open the application menu, then choose **File** > **Preferences** > **Settings**. In the **Text Editor** > **Font** section, set "Font Family" to `Droid Sans Mono, Droid Sans Fallback`. If you'd rather edit the `settings.json` file directly, set `editor.fontFamily` as shown:

&zeroWidthSpace;我们正在努力修复。在此期间，打开应用程序菜单，然后选择文件 > 首选项 > 设置。在文本编辑器 > 字体部分，将“字体系列”设置为 `Droid Sans Mono, Droid Sans Fallback` 。如果您更愿意直接编辑 `settings.json` 文件，请按所示设置 `editor.fontFamily` ：

```
    "editor.fontFamily": "Droid Sans Mono, Droid Sans Fallback"
```

### [Package git is not installed 未安装软件包 git](https://code.visualstudio.com/docs/setup/linux#_package-git-is-not-installed)

This error can appear during installation and is typically caused by the package manager's lists being out of date. Try updating them and installing again:

&zeroWidthSpace;此错误可能在安装期间出现，通常是由软件包管理器的列表过时导致。尝试更新它们并重新安装：

```
# For .deb
sudo apt-get update

# For .rpm (Fedora 21 and below)
sudo yum check-update

# For .rpm (Fedora 22 and above)
sudo dnf check-update
```

### [The code bin command does not bring the window to the foreground on Ubuntu Ubuntu 上的 code bin 命令不会将窗口置于前台](https://code.visualstudio.com/docs/setup/linux#_the-code-bin-command-does-not-bring-the-window-to-the-foreground-on-ubuntu)

Running `code .` on Ubuntu when VS Code is already open in the current directory will not bring VS Code into the foreground. This is a feature of the OS which can be disabled using `ccsm`.

&zeroWidthSpace;在当前目录中已打开 VS Code 时在 Ubuntu 上运行 `code .` 不会将 VS Code 置于前台。这是操作系统的一项功能，可以使用 `ccsm` 禁用。在“常规”>“常规选项”>“焦点和提升行为”下，将“焦点预防级别”设置为“关闭”。请记住，这是一个操作系统级别的设置，将适用于所有应用程序，而不仅仅是 VS Code。

```
# Install
sudo apt-get update
sudo apt-get install compizconfig-settings-manager

# Run
ccsm
```

Under **General** > **General Options** > **Focus & Raise Behaviour**, set "Focus Prevention Level" to "Off". Remember this is an OS-level setting that will apply to all applications, not just VS Code.

&zeroWidthSpace;无法安装 .deb 软件包，因为“/etc/apt/sources.list.d/vscode.list：没有这样的文件或目录”

### [Cannot install .deb package due to "/etc/apt/sources.list.d/vscode.list: No such file or directory" 当 不存在或您无权创建该文件时，可能会发生这种情况。要解决此问题，请尝试手动创建文件夹和一个空的 文件：](https://code.visualstudio.com/docs/setup/linux#_cannot-install-deb-package-due-to-etcaptsourceslistdvscodelist-no-such-file-or-directory)

This can happen when `sources.list.d` doesn't exist or you don't have access to create the file. To fix this, try manually creating the folder and an empty `vscode.list` file:

&zeroWidthSpace;在远程转发远程窗口时无法移动或调整窗口大小

```
sudo mkdir /etc/apt/sources.list.d
sudo touch /etc/apt/sources.list.d/vscode.list
```

### [Cannot move or resize the window while X forwarding a remote window 如果您使用 X 转发远程使用 VS Code，则需要使用本机标题栏以确保您可以正确操作窗口。您可以通过将 设置为 来切换到使用它。使用自定义标题栏](https://code.visualstudio.com/docs/setup/linux#_cannot-move-or-resize-the-window-while-x-forwarding-a-remote-window)

If you are using X forwarding to use VS Code remotely, you will need to use the native title bar to ensure you can properly manipulate the window. You can switch to using it by setting `window.titleBarStyle` to `native`.

### [Using the custom title bar](https://code.visualstudio.com/docs/setup/linux#_using-the-custom-title-bar)

The custom title bar and menus were enabled by default on Linux for several months. The custom title bar has been a success on Windows, but the customer response on Linux suggests otherwise. Based on feedback, we have decided to make this setting opt-in on Linux and leave the native title bar as the default.

&zeroWidthSpace;在 Linux 上，自定义标题栏和菜单默认启用了好几个月。自定义标题栏在 Windows 上取得了成功，但 Linux 上的客户反馈却并非如此。根据反馈，我们决定在 Linux 上将此设置设为选择加入，并将原生标题栏保留为默认设置。

The custom title bar provides many benefits including great theming support and better accessibility through keyboard navigation and screen readers. Unfortunately, these benefits do not translate as well to the Linux platform. Linux has a variety of desktop environments and window managers that can make the VS Code theming look foreign to users. For users needing the accessibility improvements, we recommend enabling the custom title bar when running in accessibility mode using a screen reader. You can still manually set the title bar with the **Window: Title Bar Style** (`window.titleBarStyle`) setting.

&zeroWidthSpace;自定义标题栏提供了许多好处，包括出色的主题支持以及通过键盘导航和屏幕阅读器实现更好的可访问性。遗憾的是，这些好处无法很好地移植到 Linux 平台。Linux 具有各种桌面环境和窗口管理器，这些环境和管理器可能会让 VS Code 主题对用户来说显得陌生。对于需要可访问性改进的用户，我们建议在使用屏幕阅读器以可访问性模式运行时启用自定义标题栏。您仍可以使用“窗口：标题栏样式 ( `window.titleBarStyle` )”设置手动设置标题栏。

### [Broken cursor in editor with display scaling enabled 启用显示缩放时编辑器中的光标损坏](https://code.visualstudio.com/docs/setup/linux#_broken-cursor-in-editor-with-display-scaling-enabled)

Due to an upstream [issue #14787](https://github.com/electron/electron/issues/14787) with Electron, the mouse cursor may render incorrectly with scaling enabled. If you notice that the usual text cursor is not being rendered inside the editor as you would expect, try falling back to the native menu bar by configuring the setting `window.titleBarStyle` to `native`.

&zeroWidthSpace;由于 Electron 中的上游问题 #14787，启用缩放时鼠标光标可能呈现不正确。如果您注意到通常的文本光标未按预期在编辑器内呈现，请尝试通过将设置 `window.titleBarStyle` 配置为 `native` 来回退到原生菜单栏。

### [Repository changed its origin value 存储库更改了其 origin 值](https://code.visualstudio.com/docs/setup/linux#_repository-changed-its-origin-value)

If you receive an error similar to the following:

&zeroWidthSpace;如果您收到类似于以下内容的错误：

```
E: Repository '...' changed its 'Origin' value from '...' to '...'
N: This must be accepted explicitly before updates for this repository can be applied. See apt-secure(8) manpage for details.
```

Use `apt` instead of `apt-get` and you will be prompted to accept the origin change:

&zeroWidthSpace;使用 `apt` 而不是 `apt-get` ，系统将提示您接受 origin 更改：

```
sudo apt update
```
