+++
title = "Sharing git credentials"
date = 2024-01-13T13:53:43+08:00
weight = 150
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials)

# Sharing Git credentials with your container 与容器共享 Git 凭据



The Dev Containers extension provides out of the box support for using local Git credentials from inside a container. In this section, we'll walk through the two supported options.

​​	Dev Containers 扩展提供了开箱即用的支持，可用于从容器内部使用本地 Git 凭据。在本节中，我们将逐步介绍两种受支持的选项。

If you do not have your user name or email address set up locally, you may be prompted to do so. You can do this on your **local** machine by running the following commands:

​​	如果您尚未在本地设置用户名或电子邮件地址，系统可能会提示您进行设置。您可以在本地计算机上运行以下命令来执行此操作：

```
git config --global user.name "Your Name"
git config --global user.email "your.email@address"
```

The extension will automatically copy your local `.gitconfig` file into the container on startup so you should not need to do this in the container itself.

​​	扩展将在启动时自动将您的本地 `.gitconfig` 文件复制到容器中，因此您无需在容器本身中执行此操作。

## [Using a credential helper 使用凭据帮助器](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials#_using-a-credential-helper)

If you use HTTPS to clone your repositories and **have a [credential helper configured](https://docs.github.com/get-started/getting-started-with-git/caching-your-github-credentials-in-git) in your local OS, no further setup is required.** Credentials you've entered locally will be reused in the container and vice versa.

​​	如果您使用 HTTPS 克隆存储库并在本地操作系统中配置了凭据帮助器，则无需进一步设置。您在本地输入的凭据将在容器中重复使用，反之亦然。

## [Using SSH keys 使用 SSH 密钥](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials#_using-ssh-keys)

There are some cases when you may be cloning your repository using SSH keys instead of a credential helper. To enable this scenario, the extension will automatically forward your **local [SSH agent](https://www.ssh.com/ssh/agent) if one is running**.

​​	在某些情况下，您可能使用 SSH 密钥而不是凭据帮助器来克隆存储库。为了启用此方案，如果本地 SSH 代理正在运行，扩展将自动转发该代理。

You can add your local SSH keys to the agent if it is running by using the `ssh-add` command. For example, run this from a terminal or PowerShell:

​​	如果代理正在运行，您可以使用 `ssh-add` 命令将本地 SSH 密钥添加到代理。例如，从终端或 PowerShell 运行此命令：

```
ssh-add $HOME/.ssh/github_rsa
```

On Windows and Linux, you may get an error because the agent is not running (macOS typically has it running by default). Follow these steps to resolve the problem:

​​	在 Windows 和 Linux 上，您可能会收到错误，因为代理未运行（macOS 通常默认运行它）。请按照以下步骤解决问题：

**Windows**:

​​	Windows：

Start a **local Administrator PowerShell** and run the following commands:

​​	启动本地管理员 PowerShell 并运行以下命令：

```
# Make sure you're running as an Administrator
Set-Service ssh-agent -StartupType Automatic
Start-Service ssh-agent
Get-Service ssh-agent
```

**Linux:
Linux：**

First, start the SSH Agent in the background by running the following in a terminal:

​​	首先，通过在终端中运行以下命令在后台启动 SSH 代理：

```
eval "$(ssh-agent -s)"
```

Then add these lines to your `~/.bash_profile` or `~/.zprofile` (for Zsh) so it starts on login:

​​	然后将这些行添加到您的 `~/.bash_profile` 或 `~/.zprofile` （适用于 Zsh）中，以便它在登录时启动：

```
if [ -z "$SSH_AUTH_SOCK" ]; then
   # Check for a currently running instance of the agent
   RUNNING_AGENT="`ps -ax | grep 'ssh-agent -s' | grep -v grep | wc -l | tr -d '[:space:]'`"
   if [ "$RUNNING_AGENT" = "0" ]; then
        # Launch a new instance of the agent
        ssh-agent -s &> $HOME/.ssh/ssh-agent
   fi
   eval `cat $HOME/.ssh/ssh-agent`
fi
```

## [Sharing GPG Keys 共享 GPG 密钥](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials#_sharing-gpg-keys)

If you want to [GPG](https://www.gnupg.org/) sign your commits, you can share your local keys with your container as well. You can find out about signing using a GPG key in [GitHub's documentation](https://docs.github.com/authentication/managing-commit-signature-verification).

​​	如果您想对提交进行 GPG 签名，也可以将本地密钥与容器共享。您可以在 GitHub 文档中了解有关使用 GPG 密钥进行签名的信息。

If you do not have GPG set up, you can configure it for your platform:

​​	如果您尚未设置 GPG，可以为您的平台配置它：

- On **Windows**, you can install [Gpg4win](https://www.gpg4win.org/).
  在 Windows 上，您可以安装 Gpg4win。

- On **macOS**, you can install [GPG Tools](https://gpgtools.org/).
  在 macOS 上，您可以安装 GPG Tools。

- On **Linux**, **locally** install the `gnupg2` package using your system's package manager.
  在 Linux 上，使用系统的包管理器在本地安装 `gnupg2` 包。

- On

   

  WSL

  :

  
  在 WSL 上：

  - Install [Gpg4win](https://www.gpg4win.org/) on the Windows side.
    在 Windows 端安装 Gpg4win。
  - Install `gpg` in your WSL distro. `sudo apt install gpg`
    在 WSL 发行版中安装 `gpg` 。 `sudo apt install gpg`
  - Register a `pinentry` GUI in your WSL distro. `echo pinentry-program /mnt/c/Program\ Files\ \(x86\)/Gpg4win/bin/pinentry.exe > ~/.gnupg/gpg-agent.conf`
    在 WSL 发行版中注册 `pinentry` GUI。 `echo pinentry-program /mnt/c/Program\ Files\ \(x86\)/Gpg4win/bin/pinentry.exe > ~/.gnupg/gpg-agent.conf`
  - Reload the `gpg` agent in WSL. `gpg-connect-agent reloadagent /bye`
    在 WSL 中重新加载 `gpg` 代理。 `gpg-connect-agent reloadagent /bye`

> **Note**: For Windows user, the gpg signing key must be configured using the Windows GUI or CLI (powershell/cmd) and not in Git Bash. A Dev Container can't access the gpg keys set in Git Bash even though it is in your `~/.gnupg/` folder, accessible in the Windows Explorer.
>
> ​​	注意：对于 Windows 用户，必须使用 Windows GUI 或 CLI（powershell/cmd）配置 gpg 签名密钥，而不能在 Git Bash 中配置。Dev Container 无法访问 Git Bash 中设置的 gpg 密钥，即使它位于 Windows 资源管理器中可访问的 `~/.gnupg/` 文件夹中。

Next, install `gnupg2` in your container by updating your Dockerfile.

​​	接下来，通过更新 Dockerfile 在容器中安装 `gnupg2` 。

For example:

​​	例如：

```
RUN apt-get update && apt-get install gnupg2 -y
```

Or if running as a [non-root user](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user):

​​	或者，如果以非 root 用户身份运行：

```
RUN sudo apt-get update && sudo apt-get install gnupg2 -y
```

To apply your configuration changes, you need to rebuild the container. You can do this by running **Dev Containers: Rebuild Container** from the Command Palette (`F1`). The next time the container starts, your GPG keys should be accessible inside the container as well.

​​	要应用配置更改，您需要重新构建容器。您可以通过从命令面板运行 Dev Containers: Rebuild Container（ `F1` ）来执行此操作。容器下次启动时，您的 GPG 密钥也应该可以在容器内访问。

> **Note**: If you used `gpg` previously in the container, you may need to run **Dev Containers: Rebuild Container** for the update to take effect.
>
> ​​	注意：如果您之前在容器中使用过 `gpg` ，您可能需要运行 Dev Containers: Rebuild Container 才能使更新生效。
