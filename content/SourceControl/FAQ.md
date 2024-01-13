+++
title = "FAQ"
date = 2024-01-12T22:36:24+08:00
weight = 30
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/sourcecontrol/faq](https://code.visualstudio.com/docs/sourcecontrol/faq)

### [ 如何编辑最近的提交消息？](https://code.visualstudio.com/docs/sourcecontrol/faq#_how-to-i-edit-the-most-recent-commit-message)

To update the commit message for the last local commit use the **Git: Commit Staged (Amend)** command. It will open an editor to edit and save the last message. Make sure that no other changes are staged, as they would be included with the commit.

​​	若要更新最近本地提交的提交消息，请使用 Git：提交暂存（修改）命令。它将打开一个编辑器以编辑并保存最后一条消息。确保未暂存其他更改，因为它们将包含在提交中。

### [I initialized my repo but the actions in the ... menu are all grayed out 我初始化了我的存储库，但 ... 菜单中的操作全部灰显](https://code.visualstudio.com/docs/sourcecontrol/faq#_i-initialized-my-repo-but-the-actions-in-the-menu-are-all-grayed-out)

To **push, pull, and sync** you need to have a Git origin set up. You can get the required URL from the repository host. Once you have that URL, you need to add it to the Git settings by running a couple of command-line actions. For example:

​​	要推送、拉取和同步，您需要设置 Git 源。您可以从存储库主机获取所需的 URL。获取该 URL 后，您需要通过运行几个命令行操作将其添加到 Git 设置中。例如：

```
> git remote add origin https://github.com/<repo owner>/<repo name>.git
> git push -u origin main
```

### [My team is using Team Foundation Version Control (TFVC) instead of Git. What should I do? 我的团队使用 Team Foundation 版本控制 (TFVC) 而不是 Git。我该怎么办？](https://code.visualstudio.com/docs/sourcecontrol/faq#_my-team-is-using-team-foundation-version-control-tfvc-instead-of-git-what-should-i-do)

Use the [Azure Repos](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team) extension and this will light up TFVC support.

​​	使用 Azure Repos 扩展，这将点亮 TFVC 支持。

### [Why do the Pull, Push and Sync actions never finish? 为什么拉取、推送和同步操作永远不会完成？](https://code.visualstudio.com/docs/sourcecontrol/faq#_why-do-the-pull-push-and-sync-actions-never-finish)

This usually means there is no credential management configured in Git and you're not getting credential prompts for some reason.

​​	这通常意味着 Git 中未配置凭据管理，并且由于某种原因您没有收到凭据提示。

You can always set up a [credential helper](https://docs.github.com/get-started/getting-started-with-git/caching-your-github-credentials-in-git) in order to pull and push from a remote server without having VS Code prompt for your credentials each time.

​​	您始终可以设置凭据帮助程序，以便从远程服务器拉取和推送，而无需 VS Code 每次都提示您输入凭据。

### [How can I sign in to Git with my Azure DevOps organization that requires multi-factor authentication? 如何使用需要多重身份验证的 Azure DevOps 组织登录 Git？](https://code.visualstudio.com/docs/sourcecontrol/faq#_how-can-i-sign-in-to-git-with-my-azure-devops-organization-that-requires-multifactor-authentication)

[Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager) (GCM) is the recommended Git credential helper for Windows, macOS, and Linux. If you're running Git for Windows, GCM has already been installed and configured for you. If you're running on macOS or Linux, the GCM [README](https://github.com/GitCredentialManager/git-credential-manager#download-and-install) has setup instructions.

​​	Git Credential Manager (GCM) 是适用于 Windows、macOS 和 Linux 的推荐 Git 凭据帮助程序。如果您正在运行 Git for Windows，则 GCM 已为您安装并配置。如果您在 macOS 或 Linux 上运行，则 GCM 自述文件具有设置说明。

### [I have GitHub Desktop installed on my computer but VS Code ignores it 我的计算机上安装了 GitHub Desktop，但 VS Code 忽略了它](https://code.visualstudio.com/docs/sourcecontrol/faq#_i-have-github-desktop-installed-on-my-computer-but-vs-code-ignores-it)

VS Code only supports the [official Git distribution](https://git-scm.com/) for its Git integration.

​​	VS Code 仅支持官方 Git 发行版进行 Git 集成。

### [I keep getting Git authentication dialogs whenever VS Code is running 每当 VS Code 运行时，我都会收到 Git 身份验证对话框](https://code.visualstudio.com/docs/sourcecontrol/faq#_i-keep-getting-git-authentication-dialogs-whenever-vs-code-is-running)

VS Code automatically fetches changes from the server in order to present you with a summary of incoming changes. The Git authentication dialog is independent from VS Code itself and is a part of your current Git credential helper.

​​	VS Code 会自动从服务器获取更改，以便向您显示传入更改的摘要。Git 身份验证对话框独立于 VS Code 本身，并且是您当前的 Git 凭据帮助程序的一部分。

One way to avoid these prompts is to set up a [credential helper](https://docs.github.com/get-started/getting-started-with-git/caching-your-github-credentials-in-git) that remembers your credentials.

​​	避免这些提示的一种方法是设置一个记住您凭据的凭据帮助程序。

Another option is to disable the auto fetch feature by changing the following setting: `"git.autofetch": false`.

​​	另一种选择是通过更改以下设置来禁用自动获取功能： `"git.autofetch": false` 。

### [Why is VS Code warning me that the git repository is potentially unsafe? 为什么 VS Code 警告我 Git 存储库可能不安全？](https://code.visualstudio.com/docs/sourcecontrol/faq#_why-is-vs-code-warning-me-that-the-git-repository-is-potentially-unsafe)

VS Code uses `git.exe` for executing all Git operations. Starting with Git [2.35.2](https://github.blog/2022-04-18-highlights-from-git-2-36/#stricter-repository-ownership-checks), users are prevented from running Git operations in a repository that is in a folder that owned by a user other than the current user as the repository is deemed to be potentially unsafe.

​​	VS Code 使用 `git.exe` 执行所有 Git 操作。从 Git 2.35.2 开始，用户无法在属于当前用户以外的其他用户拥有的文件夹中的存储库中运行 Git 操作，因为该存储库被视为可能不安全。

If you try to open such a repository, VS Code will show a welcome view in the Source Control view or an error notification. Both the welcome view and the notification contain the **Manage Unsafe Repositories** command that lets you review the list of potentially unsafe repositories, mark them as safe, and open them. The **Manage Unsafe Repositories** command is also available in the Command Palette (Ctrl+Shift+P). Marking a repository as safe will add the repository location to the `safe.directory` [git configuration](https://git-scm.com/docs/git-config#Documentation/git-config.txt-safedirectory).

​​	如果您尝试打开这样的存储库，VS Code 将在源代码管理视图中显示欢迎视图或错误通知。欢迎视图和通知都包含“管理不安全存储库”命令，该命令允许您查看可能不安全的存储库列表，将它们标记为安全并将其打开。“管理不安全存储库”命令还可在命令面板（Ctrl+Shift+P）中使用。将存储库标记为安全会将存储库位置添加到 `safe.directory` git 配置中。

On Windows, a common scenario where this can occur is when a repository is cloned using an application (for example, Windows Terminal or VS Code) that runs "as administrator", but the repository is opened using another application or instance (for example, VS Code) that does not run "as administrator".

​​	在 Windows 上，可能会出现这种情况的常见场景是，当使用“以管理员身份”运行的应用程序（例如 Windows 终端或 VS Code）克隆存储库时，但使用不“以管理员身份”运行的另一个应用程序或实例（例如 VS Code）打开存储库时。

### [Why isn't VS Code discovering Git repositories in parent folders of workspaces or open files? 为什么 VS Code 未在工作区或打开文件的父文件夹中发现 Git 存储库？](https://code.visualstudio.com/docs/sourcecontrol/faq#_why-isnt-vs-code-discovering-git-repositories-in-parent-folders-of-workspaces-or-open-files)

VS Code uses `git rev-parse --show-toplevel` to determine the root of a Git repository. In most cases, the root of the Git repository is inside the workspace, but there are scenarios where the root of the Git repository is in the parent folders of the workspace or the open file(s). While opening Git repositories in parent folders of workspaces or open files is a great feature for advanced users, it can be confusing for new users. We have seen cases where this confusion resulted in discarding changes from these Git repositories causing data loss.

​​	VS Code 使用 `git rev-parse --show-toplevel` 来确定 Git 存储库的根目录。在大多数情况下，Git 存储库的根目录位于工作区内，但有时 Git 存储库的根目录位于工作区或打开文件的父文件夹中。虽然在工作区或打开文件的父文件夹中打开 Git 存储库对于高级用户来说是一项很棒的功能，但对于新用户来说可能会造成混淆。我们已经看到一些案例，这种混淆导致丢弃了这些 Git 存储库中的更改，从而造成数据丢失。

To avoid confusion, and to reduce the risk of data loss, VS Code will display a notification and a new welcome view in the Source Control view, and will not automatically open Git repositories from the parent folders of workspaces and open files.

​​	为了避免混淆并降低数据丢失的风险，VS Code 将在源代码管理视图中显示一条通知和一个新的欢迎视图，并且不会自动打开来自工作区和打开文件的父文件夹的 Git 存储库。

You can control how Git repositories from parent folders are handled using the `git.openRepositoryInParentFolders` setting. If you would like to restore the old behavior, set the `git.openRepositoryInParentFolders` setting to `always`.

​​	您可以使用 `git.openRepositoryInParentFolders` 设置控制如何处理来自父文件夹的 Git 存储库。如果您想恢复旧行为，请将 `git.openRepositoryInParentFolders` 设置设置为 `always` 。

### [Can I use SSH Git authentication with VS Code? 我可以使用 SSH Git 身份验证与 VS Code 配合使用吗？](https://code.visualstudio.com/docs/sourcecontrol/faq#_can-i-use-ssh-git-authentication-with-vs-code)

Yes, though VS Code works most easily with SSH keys without a passphrase. If you have an SSH key with a passphrase, you'll need to launch VS Code from a Git Bash prompt to inherit its SSH environment.

​​	是的，尽管 VS Code 最容易与没有密码的 SSH 密钥配合使用。如果您有带密码的 SSH 密钥，则需要从 Git Bash 提示符启动 VS Code 以继承其 SSH 环境。

## [GitHub](https://code.visualstudio.com/docs/sourcecontrol/faq#_github)

### [Is GitHub Enterprise supported? 是否支持 GitHub Enterprise？](https://code.visualstudio.com/docs/sourcecontrol/faq#_is-github-enterprise-supported)

VS Code has official support for authentication with GitHub Enterprise Servers. Open a local checkout of a GHES repository and you will be prompted to sign in with your GitHub Enterprise Server account.

​​	VS Code 正式支持使用 GitHub Enterprise 服务器进行身份验证。打开 GHES 存储库的本地检出，系统将提示您使用 GitHub Enterprise Server 帐户登录。
