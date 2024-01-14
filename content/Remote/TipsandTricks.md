+++
title = "Tips and Tricks"
date = 2024-01-12T22:36:24+08:00
weight = 90
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/remote/troubleshooting](https://code.visualstudio.com/docs/remote/troubleshooting)

# Remote Development Tips and Tricks 远程开发技巧和窍门



This article covers troubleshooting tips and tricks for each of the Visual Studio Code [Remote Development](https://aka.ms/vscode-remote/download/extension) extensions. See the [SSH]({{< ref "/Remote/SSH" >}}), [Containers]({{< ref "/DevContainers/Overview" >}}), and [WSL]({{< ref "/Remote/WindowsSubsystemforLinux" >}}) articles for details on setting up and working with each specific extension. Or try the introductory [Tutorials]({{< ref "/Remote/SSHTutorial" >}}) to help get you running quickly in a remote environment.

​​	本文介绍了适用于每个 Visual Studio Code 远程开发扩展的故障排除提示和技巧。有关设置和使用每个特定扩展的详细信息，请参阅 SSH、容器和 WSL 文章。或者尝试使用入门教程，帮助您快速在远程环境中运行。

For tips and questions about [GitHub Codespaces](https://github.com/features/codespaces), see the [GitHub Codespaces documentation](https://docs.github.com/github/developing-online-with-codespaces).

​​	有关 GitHub Codespaces 的提示和问题，请参阅 GitHub Codespaces 文档。

## [SSH tips SSH 提示]({{< ref "/Remote/TipsandTricks#_ssh-tips" >}})

SSH is powerful and flexible, but this also adds some setup complexity. This section includes some tips and tricks for getting the Remote - SSH extension up and running in different environments.

​​	SSH 功能强大且灵活，但也增加了一些设置复杂性。本部分包括一些提示和技巧，用于在不同环境中启动并运行 Remote - SSH 扩展。

### [Configuring key based authentication 配置基于密钥的身份验证]({{< ref "/Remote/TipsandTricks#_configuring-key-based-authentication" >}})

[SSH public key authentication](https://www.ssh.com/ssh/public-key-authentication) is a convenient, high security authentication method that combines a local "private" key with a "public" key that you associate with your user account on an SSH host. This section will walk you through how to generate these keys and add them to a host.

​​	SSH 公钥身份验证是一种方便、高安全性的身份验证方法，它将本地“私钥”与您在 SSH 主机上与您的用户帐户关联的“公钥”结合起来。本部分将指导您如何生成这些密钥并将它们添加到主机。

> **Tip:** PuTTY for Windows is not a [supported client]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-client" >}}), but you can [convert your PuTTYGen keys]({{< ref "/Remote/TipsandTricks#_reusing-a-key-generated-in-puttygen" >}}).
>
> ​​	提示：Windows 版 PuTTY 不是受支持的客户端，但您可以转换您的 PuTTYGen 密钥。

### [Quick start: Using SSH keys 快速入门：使用 SSH 密钥]({{< ref "/Remote/TipsandTricks#_quick-start-using-ssh-keys" >}})

To set up SSH key based authentication for your remote host. First we'll create a key pair and then copy the public key to the host.

​​	为您的远程主机设置基于 SSH 密钥的身份验证。首先，我们将创建一个密钥对，然后将公钥复制到主机。

**Create your local SSH key pair
创建本地 SSH 密钥对**

Check to see if you already have an SSH key on your **local** machine. This is typically located at `~/.ssh/id_ed25519.pub` on macOS / Linux, and the `.ssh` directory in your user profile folder on Windows (for example `C:\Users\your-user\.ssh\id_ed25519.pub`).

​​	检查本地计算机上是否已有 SSH 密钥。这通常位于 macOS/Linux 上的 `~/.ssh/id_ed25519.pub` ，以及 Windows 上用户配置文件文件夹中的 `.ssh` 目录（例如 `C:\Users\your-user\.ssh\id_ed25519.pub` ）。

If you do not have a key, run the following command in a **local** terminal / PowerShell to generate an SSH key pair:

​​	如果没有密钥，请在本地终端/PowerShell 中运行以下命令以生成 SSH 密钥对：

```
ssh-keygen -t ed25519 -b 4096
```

> **Tip:** Don't have `ssh-keygen`? Install [a supported SSH client]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-client" >}}).
>
> ​​	提示：没有 `ssh-keygen` ？安装受支持的 SSH 客户端。

**Restrict the permissions on the private key file
限制私钥文件的权限**

- For macOS / Linux, run the following shell command, replacing the path to your private key if necessary:

  ​​	对于 macOS/Linux，运行以下 shell 命令，如有必要，替换私钥的路径：

  ```
  chmod 400 ~/.ssh/id_ed25519
  ```

- For Windows, run the following command in PowerShell to grant explicit read access to your username:

  ​​	对于 Windows，在 PowerShell 中运行以下命令以授予用户名显式读取访问权限：

  ```
  icacls "privateKeyPath" /grant :R
  ```

  Then navigate to the private key file in Windows Explorer, right-click and select **Properties**. Select the **Security** tab > **Advanced** > **Disable inheritance** > **Remove all inherited permissions from this object**.

  ​​	然后在 Windows 资源管理器中导航到私钥文件，右键单击并选择“属性”。选择“安全”选项卡>“高级”>“禁用继承”>“从此对象中删除所有继承的权限”。

**Authorize your macOS or Linux machine to connect
授权 macOS 或 Linux 计算机进行连接**

Run one of the following commands, in a **local terminal window** replacing user and host name as appropriate to copy your local public key to the SSH host.

​​	在本地终端窗口中运行以下命令之一，替换用户和主机名以将本地公钥复制到 SSH 主机。

- Connecting to a **macOS or Linux** SSH host:

  ​​	连接到 macOS 或 Linux SSH 主机：

  ```
  export USER_AT_HOST="your-user-name-on-host@hostname"
  export PUBKEYPATH="$HOME/.ssh/id_ed25519.pub"
  
  ssh-copy-id -i "$PUBKEYPATH" "$USER_AT_HOST"
  ```

- Connecting to a **Windows** SSH host:

  ​​	连接到 Windows SSH 主机：

  ```
  export USER_AT_HOST="your-user-name-on-host@hostname"
  export PUBKEYPATH="$HOME/.ssh/id_ed25519.pub"
  
  ssh $USER_AT_HOST "powershell New-Item -Force -ItemType Directory -Path \"\$HOME\\.ssh\"; Add-Content -Force -Path \"\$HOME\\.ssh\\authorized_keys\" -Value '$(tr -d '\n\r' < "$PUBKEYPATH")'"
  ```

  You may want to validate that the `authorized_keys` file in the `.ssh` folder for your **remote user on the SSH host** is owned by you and no other user has permission to access it. See the [OpenSSH wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-Win32-OpenSSH#authorized_keys) for details.

  ​​	您可能需要验证 SSH 主机上远程用户的 `authorized_keys` 文件夹中的 `.ssh` 文件归您所有，并且没有其他用户有权访问它。有关详细信息，请参阅 OpenSSH Wiki。

**Authorize your Windows machine to connect
授权您的 Windows 机器进行连接**

Run one of the following commands, in a **local PowerShell** window replacing user and host name as appropriate to copy your local public key to the SSH host.

​​	在本地 PowerShell 窗口中运行以下命令之一，替换用户和主机名以将您的本地公钥复制到 SSH 主机。

- Connecting to a **macOS or Linux** SSH host:

  ​​	连接到 macOS 或 Linux SSH 主机：

  ```
  $USER_AT_HOST="your-user-name-on-host@hostname"
  $PUBKEYPATH="$HOME\.ssh\id_ed25519.pub"
  
  $pubKey=(Get-Content "$PUBKEYPATH" | Out-String); ssh "$USER_AT_HOST" "mkdir -p ~/.ssh && chmod 700 ~/.ssh && echo '${pubKey}' >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
  ```

- Connecting to a **Windows** SSH host:

  ​​	连接到 Windows SSH 主机：

  ```
  $USER_AT_HOST="your-user-name-on-host@hostname"
  $PUBKEYPATH="$HOME\.ssh\id_ed25519.pub"
  
  Get-Content "$PUBKEYPATH" | Out-String | ssh $USER_AT_HOST "powershell `"New-Item -Force -ItemType Directory -Path `"`$HOME\.ssh`"; Add-Content -Force -Path `"`$HOME\.ssh\authorized_keys`" `""
  ```

  Validate that the `authorized_keys` file in the `.ssh` folder for your **remote user on the SSH host** is owned by you and no other user has permission to access it. See the [OpenSSH wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-Win32-OpenSSH#authorized_keys) for details.

  ​​	验证 SSH 主机上远程用户的 `authorized_keys` 文件夹中的 `.ssh` 文件归您所有，并且没有其他用户有权访问它。有关详细信息，请参阅 OpenSSH Wiki。

### [Improving your security with a dedicated key 使用专用密钥提高安全性]({{< ref "/Remote/TipsandTricks#_improving-your-security-with-a-dedicated-key" >}})

While using a single SSH key across all your SSH hosts can be convenient, if anyone gains access to your private key, they will have access to all of your hosts as well. You can prevent this by creating a separate SSH key for your development hosts. Just follow these steps:

​​	虽然在所有 SSH 主机上使用单个 SSH 密钥很方便，但如果有人获得了您的私钥，他们也将能够访问您的所有主机。您可以通过为您的开发主机创建单独的 SSH 密钥来防止这种情况。只需按照以下步骤操作：

1. Generate a separate SSH key in a different file.

   ​​	在不同的文件中生成单独的 SSH 密钥。

   **macOS / Linux**: Run the following command in a **local terminal**:

   ​​	macOS/Linux：在本地终端中运行以下命令：

   ```
   ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519-remote-ssh
   ```

   **Windows**: Run the following command in a **local PowerShell**:

   ​​	Windows：在本地 PowerShell 中运行以下命令：

   ```
   ssh-keygen -t ed25519 -f "$HOME\.ssh\id_ed25519-remote-ssh"
   ```

2. Follow the same steps in the [quick start]({{< ref "/Remote/TipsandTricks#_quick-start-using-ssh-keys" >}}) to authorize the key on the SSH host, but set the `PUBKEYPATH` to the `id_ed25519-remote-ssh.pub` file instead.

   ​​	按照快速入门中的相同步骤在 SSH 主机上授权密钥，但将 `PUBKEYPATH` 设置为 `id_ed25519-remote-ssh.pub` 文件。

3. In VS Code, run **Remote-SSH: Open Configuration File...** in the Command Palette (F1), select an SSH config file, and add (or modify) a host entry as follows:

   ​​	在 VS Code 中，运行远程 SSH：在命令面板 (F1) 中打开配置文件...，选择一个 SSH 配置文件，并按如下方式添加（或修改）主机条目：

   ```
   Host name-of-ssh-host-here
       User your-user-name-on-host
       HostName host-fqdn-or-ip-goes-here
       IdentityFile ~/.ssh/id_ed25519-remote-ssh
   ```

   > **Tip:** You can use `/` for Windows paths as well. If you use `\` you will need to use two slashes. For example, `C:\\path\\to\\my\\id_ed25519`.
   >
   > ​​	提示：您也可以将 `/` 用于 Windows 路径。如果您使用 `\` ，则需要使用两个斜杠。例如， `C:\\path\\to\\my\\id_ed25519` 。

### [Reusing a key generated in PuTTYGen 重新使用在 PuTTYGen 中生成的密钥]({{< ref "/Remote/TipsandTricks#_reusing-a-key-generated-in-puttygen" >}})

If you used PuTTYGen to set up SSH public key authentication for the host you are connecting to, you need to convert your private key so that other SSH clients can use it. To do this:

​​	如果您使用 PuTTYGen 为要连接的主机设置 SSH 公钥身份验证，则需要转换您的私钥，以便其他 SSH 客户端可以使用它。为此，请执行以下操作：

1. Open PuTTYGen **locally** and load the private key you want to convert.

   ​​	在本地打开 PuTTYGen 并加载要转换的私钥。

2. Select **Conversions > Export OpenSSH key** from the application menu. Save the converted key to a **local** location under the`.ssh` directory in your user profile folder (for example `C:\Users\youruser\.ssh`).

   ​​	从应用程序菜单中选择转换 > 导出 OpenSSH 密钥。将转换后的密钥保存在用户配置文件文件夹中的 `.ssh` 目录下的本地位置（例如 `C:\Users\youruser\.ssh` ）。

3. Validate that this new **local** file is owned by you and no other user has permissions to access it.

   ​​	验证此新本地文件归您所有，并且没有其他用户有权访问它。

4. In VS Code, run **Remote-SSH: Open Configuration File...** in the Command Palette (F1), select the SSH config file you want to change, and add (or modify) a host entry in the config file as follows to point to the file:

   ​​	在 VS Code 中，在命令面板 (F1) 中运行 Remote-SSH：打开配置文件...，选择要更改的 SSH 配置文件，然后在配置文件中添加（或修改）主机条目，如下所示以指向该文件：

   ```
   Host name-of-ssh-host-here
       User your-user-name-on-host
       HostName host-fqdn-or-ip-goes-here
       IdentityFile ~/.ssh/exported-keyfile-from-putty
   ```

### [Improving security on multi-user servers 提高多用户服务器上的安全性]({{< ref "/Remote/TipsandTricks#_improving-security-on-multiuser-servers" >}})

The Remote - SSH extension installs and maintains the "VS Code Server". The server is started with a randomly generated key, and any new connection to the server needs to provide the key. The key is stored on the remote's disk, readable only by the current user. There is one HTTP path that is available without authentication at `/version`.

​​	Remote - SSH 扩展安装并维护“VS Code Server”。服务器使用随机生成的密钥启动，并且与服务器的任何新连接都需要提供该密钥。该密钥存储在远程磁盘上，只有当前用户可读。有一个 HTTP 路径可以在 `/version` 处不经身份验证而使用。

By default, the server listens to `localhost` on a random TCP port that is then forwarded to your local machine. If you are connecting to a **Linux or macOS** host, you can switch to using Unix sockets that are locked down to a particular user. This socket is then forwarded instead of the port.

​​	默认情况下，服务器在随机 TCP 端口上侦听 `localhost` ，然后将其转发到您的本地计算机。如果您正在连接到 Linux 或 macOS 主机，则可以切换为使用锁定到特定用户的 Unix 套接字。然后转发此套接字，而不是端口。

> **Note:** This setting **disables connection multiplexing** so configuring [public key authentication]({{< ref "/Remote/TipsandTricks#_configuring-key-based-authentication" >}}) is recommended.
>
> ​​	注意：此设置禁用连接多路复用，因此建议配置公钥身份验证。

To configure it:

​​	要配置它：

1. Ensure you have a **local OpenSSH 6.7+ SSH client** on Windows, macOS, or Linux and an **OpenSSH 6.7+ Linux or macOS Host** (Windows does not support this mode).

   ​​	确保您在 Windows、macOS 或 Linux 上拥有本地 OpenSSH 6.7+ SSH 客户端，以及 OpenSSH 6.7+ Linux 或 macOS 主机（Windows 不支持此模式）。

2. Switch Remote - SSH into socket mode by enabling **Remote.SSH: Remote Server Listen On Socket** in your **local** VS Code [User settings]({{< ref "/GetStarted/Settings" >}}).

   ​​	切换远程 - 通过在本地 VS Code 用户设置中启用 Remote.SSH: Remote Server Listen On Socket，将 SSH 切换到套接字模式。

   ![Listen on socket VS Code setting](./TipsandTricks_img/ssh-listen-on-socket.png)

3. If you've already connected to the SSH Host, select **Remote-SSH: Kill VS Code Server on Host...** from the Command Palette (F1) so the setting takes effect.

   ​​	如果您已连接到 SSH 主机，请从命令面板 (F1) 中选择 Remote-SSH: Kill VS Code Server on Host...，以便该设置生效。

If you encounter an error when connecting, you may need to enable socket forwarding on your SSH Host's [sshd config](https://www.ssh.com/ssh/sshd_config/). To do so:

​​	如果您在连接时遇到错误，可能需要在 SSH 主机的 sshd 配置中启用套接字转发。为此，请执行以下操作：

1. Open `/etc/ssh/sshd_config` in a text editor (like vi, nano, or pico) on the **SSH host** (not locally).
   在 SSH 主机上（而非本地）使用文本编辑器（如 vi、nano 或 pico）打开 `/etc/ssh/sshd_config` 。
2. Add the setting `AllowStreamLocalForwarding yes`.
   添加设置 `AllowStreamLocalForwarding yes` 。
3. Restart the SSH server. (On Ubuntu, run `sudo systemctl restart sshd`.).
   重新启动 SSH 服务器。（在 Ubuntu 上，运行 `sudo systemctl restart sshd` .）。
4. Retry.
   重试。

### [Troubleshooting hanging or failing connections 故障排除挂起或连接失败]({{< ref "/Remote/TipsandTricks#_troubleshooting-hanging-or-failing-connections" >}})

If you are running into problems with VS Code hanging while trying to connect (and potentially timing out), there are a few things you can do to try to resolve the issue.

​​	如果您在尝试连接时遇到 VS Code 挂起（并可能超时）的问题，您可以执行一些操作来尝试解决此问题。

**General troubleshooting: Remove the server
常规故障排除：删除服务器**

One command helpful to troubleshoot a variety of Remote-SSH issues is **Remote-SSH: Kill VS Code Server on Host**. This will remove the server, which can fix a wide range of issues and error messages you may see, such as "Could not establish connection to `server_name`: The VS Code Server failed to start."

​​	一个有助于解决各种远程 SSH 问题的命令是远程 SSH：在主机上终止 VS Code 服务器。这将删除服务器，这可以修复您可能看到的各种问题和错误消息，例如“无法建立与 `server_name` 的连接：VS Code 服务器启动失败”。

**See if VS Code is waiting on a prompt
查看 VS Code 是否正在等待提示**

Enable the `remote.SSH.showLoginTerminal` [setting]({{< ref "/GetStarted/Settings" >}}) in VS Code and retry. If you are prompted to input a password or token, see [Enabling alternate SSH authentication methods]({{< ref "/Remote/TipsandTricks#_enabling-alternate-ssh-authentication-methods" >}}) for details on reducing the frequency of prompts.

​​	在 VS Code 中启用 `remote.SSH.showLoginTerminal` 设置并重试。如果您收到输入密码或令牌的提示，请参阅启用备用 SSH 身份验证方法，了解有关减少提示频率的详细信息。

If you are still having trouble, set the following properties in `settings.json` and retry:

​​	如果您仍然遇到问题，请在 `settings.json` 中设置以下属性并重试：

```
"remote.SSH.showLoginTerminal": true,
"remote.SSH.useLocalServer": false
```

**Work around a bug with some versions of Windows OpenSSH server
解决某些版本的 Windows OpenSSH 服务器的错误**

Due to a bug in certain versions of OpenSSH server for Windows, the default check to determine if the host is running Windows may not work properly. This does not occur with OpenSSH server that ships with Windows 1909 and below.

​​	由于 Windows 的某些版本的 OpenSSH 服务器中存在错误，因此用于确定主机是否正在运行 Windows 的默认检查可能无法正常工作。使用 Windows 1909 及更低版本附带的 OpenSSH 服务器不会出现这种情况。

Fortunately, you can work around this problem by specifically telling VS Code if your SSH host is running Windows by adding the following to `settings.json`:

​​	幸运的是，您可以通过明确告知 VS Code 您的 SSH 主机是否运行 Windows 来解决此问题，方法是将以下内容添加到 `settings.json` 中：

```
"remote.SSH.useLocalServer": false
```

You can also force VS Code to identify a particular host as Windows using the following property:

​​	您还可以使用以下属性强制 VS Code 将特定主机识别为 Windows：

```
"remote.SSH.remotePlatform": {
    "host-in-ssh-config-or-fqdn": "windows"
}
```

A fix has been merged so this problem should be resolved in a version of the server greater than 8.1.0.0.

​​	已合并修复程序，因此此问题应在高于 8.1.0.0 的服务器版本中得到解决。

**Enable TCP Forwarding on the remote host
在远程主机上启用 TCP 转发**

Remote - SSH extension makes use of an SSH tunnel to facilitate communication with the host. In some cases, this may be disabled on your SSH server. To see if this is the problem, open the **Remote - SSH** category in the output window and check for the following message:

​​	Remote - SSH 扩展利用 SSH 隧道来促进与主机的通信。在某些情况下，这可能会在您的 SSH 服务器上禁用。要查看是否出现此问题，请在输出窗口中打开 Remote - SSH 类别，然后检查是否有以下消息：

```
open failed: administratively prohibited: open failed
```

If you do see that message, follow these steps to update your SSH server's [sshd config](https://www.ssh.com/ssh/sshd_config/):

​​	如果您确实看到该消息，请按照以下步骤更新 SSH 服务器的 sshd 配置：

1. Open `/etc/ssh/sshd_config` or `C:\ProgramData\ssh\sshd_config` in a text editor (like Vim, nano, Pico, or Notepad) on the **SSH host** (not locally).
   在 SSH 主机上（而非本地）的文本编辑器（如 Vim、nano、Pico 或记事本）中打开 `/etc/ssh/sshd_config` 或 `C:\ProgramData\ssh\sshd_config` 。
2. Add the setting `AllowTcpForwarding yes`.
   添加设置 `AllowTcpForwarding yes` 。
3. Restart the SSH server. (On Ubuntu, run `sudo systemctl restart sshd`. On Windows, in an admin PowerShell run, `Restart-Service sshd`).
   重新启动 SSH 服务器。（在 Ubuntu 上，运行 `sudo systemctl restart sshd` 。在 Windows 上，在管理员 PowerShell 中运行 `Restart-Service sshd` ）。
4. Retry.
   重试。

**Set the ProxyCommand parameter in your SSH config file
在 SSH 配置文件中设置 ProxyCommand 参数**

If you are behind a proxy and are unable to connect to your SSH host, you may need to use the `ProxyCommand` parameter for your host in a **local** [SSH config file](https://linux.die.net/man/5/ssh_config). You can read this [SSH ProxyCommand article](https://www.cyberciti.biz/faq/linux-unix-ssh-proxycommand-passing-through-one-host-gateway-server/) for an example of its use.

​​	如果您位于代理后面并且无法连接到 SSH 主机，您可能需要在本地 SSH 配置文件中为您的主机使用 `ProxyCommand` 参数。您可以阅读此 SSH ProxyCommand 文章以了解其使用示例。

**Ensure the remote machine has internet access
确保远程计算机具有 Internet 访问权限**

The remote machine must have internet access to be able to download the VS Code Server and extensions from the Marketplace. See the [FAQ for details]({{< ref "/Remote/FAQ#_what-are-the-connectivity-requirements-for-vs-code-server" >}}) on connectivity requirements.

​​	远程计算机必须具有 Internet 访问权限，才能从 Marketplace 下载 VS Code Server 和扩展。有关连接要求的详细信息，请参阅常见问题解答。

**Set HTTP_PROXY / HTTPS_PROXY on the remote host
在远程主机上设置 HTTP_PROXY / HTTPS_PROXY**

If your remote host is behind a proxy, you may need to set the HTTP_PROXY or HTTPS_PROXY environment variable on the **SSH host**. Open your `~/.bashrc` file add the following (replacing `proxy.fqdn.or.ip:3128` with the appropriate hostname / IP and port):

​​	如果您的远程主机位于代理后面，您可能需要在 SSH 主机上设置 HTTP_PROXY 或 HTTPS_PROXY 环境变量。打开您的 `~/.bashrc` 文件，添加以下内容（将 `proxy.fqdn.or.ip:3128` 替换为相应的主机名/IP 和端口）：

```
export HTTP_PROXY=http://proxy.fqdn.or.ip:3128
export HTTPS_PROXY=$HTTP_PROXY

# Or if an authenticated proxy
export HTTP_PROXY=http://username:password@proxy.fqdn.or.ip:3128
export HTTPS_PROXY=$HTTP_PROXY
```

**Work around `/tmp` mounted with `noexec`
解决使用 `noexec` 挂载的 `/tmp`**

Some remote servers are set up to disallow executing scripts from `/tmp`. VS Code writes its install script to the system temp directory and tries to execute it from there. You can work with your system administrator to determine whether this can be worked around.

​​	某些远程服务器被设置为不允许从 `/tmp` 执行脚本。VS Code 将其安装脚本写入系统临时目录并尝试从中执行它。您可以与系统管理员合作以确定是否可以解决此问题。

**Check whether a different shell is launched during install
检查在安装期间是否启动了不同的 shell**

Some users launch a different shell from their `.bash_profile` or other startup script on their **SSH host** because they want to use a different shell than the default. This can break VS Code's remote server install script and isn't recommended. Instead, use `chsh` to change your default shell on the remote machine.

​​	一些用户从其 SSH 主机上的 `.bash_profile` 或其他启动脚本启动不同的 shell，因为他们想使用不同于默认 shell 的 shell。这可能会破坏 VS Code 的远程服务器安装脚本，不建议这样做。相反，使用 `chsh` 更改远程计算机上的默认 shell。

**Connecting to systems that dynamically assign machines per connection
连接到按连接动态分配计算机的系统**

Some systems will dynamically route an SSH connection to one node from a cluster each time an SSH connection is made. This is an issue for VS Code because it makes two connections to open a remote window: the first to install or start the VS Code Server (or find an already running instance) and the second to create the SSH port tunnel that VS Code uses to talk to the server. If VS Code is routed to a different machine when it creates the second connection, it won't be able to talk to the VS Code server.

​​	每次建立 SSH 连接时，某些系统会将 SSH 连接动态路由到群集中的一个节点。这对 VS Code 来说是一个问题，因为它会创建两个连接以打开一个远程窗口：第一个连接用于安装或启动 VS Code Server（或查找已运行的实例），第二个连接用于创建 VS Code 用于与服务器通信的 SSH 端口隧道。如果在创建第二个连接时将 VS Code 路由到不同的计算机，它将无法与 VS Code 服务器通信。

One workaround for this is to use the `ControlMaster` option in OpenSSH (macOS/Linux clients only), described in [Enabling alternate SSH authentication methods]({{< ref "/Remote/TipsandTricks#_enabling-alternate-ssh-authentication-methods" >}}), so that VS Code's two connections will be multiplexed through a single SSH connection to the same node.

​​	一种解决方法是在 OpenSSH（仅限 macOS/Linux 客户端）中使用 `ControlMaster` 选项，如启用备用 SSH 身份验证方法中所述，以便 VS Code 的两个连接将通过到同一节点的单个 SSH 连接进行多路复用。

**Contact your system administrator for configuration help
有关配置帮助，请联系系统管理员**

SSH is a very flexible protocol and supports many configurations. If you see other errors, in either the login terminal or the **Remote-SSH** output window, they could be due to a missing setting.

​​	SSH 是一种非常灵活的协议，支持多种配置。如果您在登录终端或远程 SSH 输出窗口中看到其他错误，则可能是由于缺少设置。

Contact your system administrator for information about the required settings for your SSH host and client. Specific command-line arguments for connecting to your SSH host can be added to an [SSH config file](https://linux.die.net/man/5/ssh_config).

​​	请联系系统管理员，以了解 SSH 主机和客户端所需设置的信息。可以将用于连接到 SSH 主机的特定命令行参数添加到 SSH 配置文件中。

To access your config file, run **Remote-SSH: Open Configuration File...** in the Command Palette (F1). You can then work with your admin to add the necessary settings.

​​	若要访问配置文件，请在命令面板 (F1) 中运行远程 SSH：打开配置文件...。然后，您可以与管理员合作添加必要的设置。

### [Enabling alternate SSH authentication methods 启用备用 SSH 身份验证方法]({{< ref "/Remote/TipsandTricks#_enabling-alternate-ssh-authentication-methods" >}})

If you are connecting to an SSH remote host and are either:

​​	如果您正在连接到 SSH 远程主机，并且：

- Connecting with two-factor authentication
  使用双重身份验证进行连接
- Using password authentication
  使用密码身份验证
- Using an SSH key with a passphrase when the [SSH Agent]({{< ref "/Remote/TipsandTricks#_setting-up-the-ssh-agent" >}}) is not running or accessible
  在 SSH 代理程序未运行或无法访问时使用带有密码的 SSH 密钥

then VS Code should automatically prompt you to enter needed information. If you do not see the prompt, enable the `remote.SSH.showLoginTerminal` [setting]({{< ref "/GetStarted/Settings" >}}) in VS Code. This setting displays the terminal whenever VS Code runs an SSH command. You can then enter your authentication code, password, or passphrase when the terminal appears.

​​	那么 VS Code 应自动提示您输入所需信息。如果您没有看到提示，请在 VS Code 中启用 `remote.SSH.showLoginTerminal` 设置。此设置会在 VS Code 运行 SSH 命令时显示终端。然后，您可以在终端出现时输入身份验证代码、密码或密码短语。

If you are still having trouble, you may need to add the following properties in `settings.json` and retry:

​​	如果您仍然遇到问题，您可能需要在 `settings.json` 中添加以下属性并重试：

```
"remote.SSH.showLoginTerminal": true,
"remote.SSH.useLocalServer": false
```

If you are on macOS and Linux and want to reduce how often you have to enter a password or token, you can enable the `ControlMaster` feature on your **local machine** so that OpenSSH runs multiple SSH sessions over a single connection.

​​	如果您使用的是 macOS 和 Linux 并希望减少输入密码或令牌的频率，您可以在本地计算机上启用 `ControlMaster` 功能，以便 OpenSSH 通过单个连接运行多个 SSH 会话。

To enable `ControlMaster`:

​​	要启用 `ControlMaster` ：

1. Add an entry like this to your SSH config file:

   ​​	将类似这样的条目添加到您的 SSH 配置文件：

   ```
   Host *
       ControlMaster auto
       ControlPath  ~/.ssh/sockets/%r@%h-%p
       ControlPersist  600
   ```

2. Then run `mkdir -p ~/.ssh/sockets` to create the sockets folder.

   ​​	然后运行 `mkdir -p ~/.ssh/sockets` 以创建套接字文件夹。

### [Setting up the SSH Agent 设置 SSH 代理]({{< ref "/Remote/TipsandTricks#_setting-up-the-ssh-agent" >}})

If you are connecting to an SSH host using a key with a passphrase, you should ensure that the [SSH Agent](https://www.ssh.com/ssh/agent) is running **locally**. VS Code will automatically add your key to the agent so you don't have to enter your passphrase every time you open a remote VS Code window.

​​	如果您使用带有密码的密钥连接到 SSH 主机，您应确保 SSH 代理在本地运行。VS Code 会自动将您的密钥添加到代理，因此您不必在每次打开远程 VS Code 窗口时输入密码。

To verify that the agent is running and is reachable from VS Code's environment, run `ssh-add -l` in the terminal of a local VS Code window. You should see a listing of the keys in the agent (or a message that it has no keys). If the agent is not running, follow these instructions to start it. After starting the agent, be sure to restart VS Code.

​​	要验证代理正在运行并且 VS Code 的环境可以访问它，请在本地 VS Code 窗口的终端中运行 `ssh-add -l` 。您应该会看到代理中的密钥列表（或一条消息，指出它没有密钥）。如果代理未运行，请按照以下说明启动它。启动代理后，务必重新启动 VS Code。

**Windows:
Windows：**

To enable SSH Agent automatically on Windows, start a **local Administrator PowerShell** and run the following commands:

​​	要在 Windows 上自动启用 SSH 代理，请启动本地管理员 PowerShell 并运行以下命令：

```
# Make sure you're running as an Administrator
Set-Service ssh-agent -StartupType Automatic
Start-Service ssh-agent
Get-Service ssh-agent
```

Now the agent will be started automatically on login.

​​	现在，代理将在登录时自动启动。

**Linux:
Linux：**

To start the SSH Agent in the background, run:

​​	要在后台启动 SSH 代理，请运行：

```
eval "$(ssh-agent -s)"
```

To start the SSH Agent automatically on login, add these lines to your `~/.bash_profile`:

​​	要在登录时自动启动 SSH 代理，请将这些行添加到您的 `~/.bash_profile` 中：

```
if [ -z "$SSH_AUTH_SOCK" ]; then
   # Check for a currently running instance of the agent
   RUNNING_AGENT="`ps -ax | grep 'ssh-agent -s' | grep -v grep | wc -l | tr -d '[:space:]'`"
   if [ "$RUNNING_AGENT" = "0" ]; then
        # Launch a new instance of the agent
        ssh-agent -s &> .ssh/ssh-agent
   fi
   eval `cat .ssh/ssh-agent`
fi
```

**macOS:
macOS：**

The agent should be running by default on macOS.

​​	代理应在 macOS 上默认运行。

### [Making local SSH Agent available on the remote 使本地 SSH 代理在远程可用]({{< ref "/Remote/TipsandTricks#_making-local-ssh-agent-available-on-the-remote" >}})

An SSH Agent on your local machine allows the Remote - SSH extension to connect to your chosen remote system without repeatedly prompting for a passphrase, but tools like Git that run on the remote, don't have access to your locally-unlocked private keys.

​​	本地计算机上的 SSH 代理允许“远程 - SSH”扩展连接到您选择的远程系统，而无需反复提示输入密码，但像 Git 这样的在远程运行的工具无法访问您本地解锁的私钥。

You can see this by opening the integrated terminal on the remote and running `ssh-add -l`. The command should list the unlocked keys, but instead reports an error about not being able to connect to the authentication agent. Setting `ForwardAgent yes` makes the local SSH Agent available in the remote environment, solving this problem.

​​	您可以通过在远程打开集成终端并运行 `ssh-add -l` 来查看这一点。该命令应列出解锁的密钥，但会报告一条错误，指出无法连接到身份验证代理。设置 `ForwardAgent yes` 使本地 SSH 代理在远程环境中可用，从而解决此问题。

You can do this by editing your `.ssh/config` file (or whatever `Remote.SSH.configFile` is set to - use the **Remote-SSH: Open SSH Configuration File...** command to be sure) and adding:

​​	您可以通过编辑 `.ssh/config` 文件（或 `Remote.SSH.configFile` 设置为任何内容 - 使用“远程 SSH：打开 SSH 配置文件...”命令以确保）并添加以下内容来执行此操作：

```
Host *
    ForwardAgent yes
```

Note that you might want to be more restrictive and only set the option for particular named hosts.

​​	请注意，您可能希望更加严格，并且仅为特定命名主机设置选项。

### [Fixing SSH file permission errors 修复 SSH 文件权限错误]({{< ref "/Remote/TipsandTricks#_fixing-ssh-file-permission-errors" >}})

SSH can be strict about file permissions and if they are set incorrectly, you may see errors such as "WARNING: UNPROTECTED PRIVATE KEY FILE!". There are several ways to update file permissions in order to fix this, which are described in the sections below.

​​	SSH 对文件权限非常严格，如果设置不正确，您可能会看到“警告：未受保护的私钥文件！”等错误。有几种方法可以更新文件权限以修复此问题，这些方法在以下部分中进行了描述。

### [Local SSH file and folder permissions 本地 SSH 文件和文件夹权限]({{< ref "/Remote/TipsandTricks#_local-ssh-file-and-folder-permissions" >}})

**macOS / Linux:
macOS/Linux：**

On your local machine, make sure the following permissions are set:

​​	在您的本地计算机上，确保设置了以下权限：

| Folder / File 文件夹/文件                                    | Permissions 权限                  |
| :----------------------------------------------------------- | :-------------------------------- |
| `.ssh` in your user folder `.ssh` 在您的用户文件夹中         | `chmod 700 ~/.ssh`                |
| `.ssh/config` in your user folder `.ssh/config` 在您的用户文件夹中 | `chmod 600 ~/.ssh/config`         |
| `.ssh/id_ed25519.pub` in your user folder `.ssh/id_ed25519.pub` 在您的用户文件夹中 | `chmod 600 ~/.ssh/id_ed25519.pub` |
| Any other key file 任何其他密钥文件                          | `chmod 600 /path/to/key/file`     |

**Windows:
Windows：**

The specific expected permissions can vary depending on the exact SSH implementation you are using. We recommend using the out of box [Windows 10 OpenSSH Client](https://learn.microsoft.com/windows-server/administration/openssh/openssh_overview).

​​	具体预期的权限可能因您正在使用的确切 SSH 实现而异。我们建议使用开箱即用的 Windows 10 OpenSSH 客户端。

In this case, make sure that all of the files in the `.ssh` folder for your remote user on the SSH host is owned by you and no other user has permissions to access it. See the [Windows OpenSSH wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-Win32-OpenSSH) for details.

​​	在这种情况下，请确保 SSH 主机上远程用户的 `.ssh` 文件夹中的所有文件都归您所有，并且没有其他用户有权访问它。有关详细信息，请参阅 Windows OpenSSH Wiki。

For all other clients, consult your client's documentation for what the implementation expects.

​​	对于所有其他客户端，请查阅客户端文档以了解实现预期。

### [Server SSH file and folder permissions 服务器 SSH 文件和文件夹权限]({{< ref "/Remote/TipsandTricks#_server-ssh-file-and-folder-permissions" >}})

**macOS / Linux:
macOS / Linux：**

On the remote machine you are connecting to, make sure the following permissions are set:

​​	在您连接到的远程计算机上，确保设置了以下权限：

| Folder / File 文件夹 / 文件                                  | Linux / macOS Permissions Linux / macOS 权限 |
| :----------------------------------------------------------- | :------------------------------------------- |
| `.ssh` in your user folder on the server `.ssh` 在服务器上的用户文件夹中 | `chmod 700 ~/.ssh`                           |
| `.ssh/authorized_keys` in your user folder on the server `.ssh/authorized_keys` 在服务器上的用户文件夹中 | `chmod 600 ~/.ssh/authorized_keys`           |

Note that only Linux hosts are currently supported, which is why permissions for macOS and Windows 10 have been omitted.

​​	请注意，目前仅支持 Linux 主机，这就是为什么省略了 macOS 和 Windows 10 的权限。

**Windows:
Windows：**

See the [Windows OpenSSH wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-Win32-OpenSSH) for details on setting the appropriate file permissions for the Windows OpenSSH server.

​​	有关为 Windows OpenSSH 服务器设置适当文件权限的详细信息，请参阅 Windows OpenSSH wiki。

### [Installing a supported SSH client 安装受支持的 SSH 客户端]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-client" >}})

| OS                                        | Instructions 说明                                            |
| :---------------------------------------- | :----------------------------------------------------------- |
| Windows 10 1803+ / Server 2016/2019 1803+ | Install the [Windows OpenSSH Client](https://learn.microsoft.com/windows-server/administration/openssh/openssh_install_firstuse). 安装 Windows OpenSSH 客户端。 |
| Earlier Windows 早期 Windows              | Install [Git for Windows](https://git-scm.com/download/win). 安装适用于 Windows 的 Git。 |
| macOS                                     | Comes pre-installed. 预先安装。                              |
| Debian/Ubuntu                             | Run `sudo apt-get install openssh-client` 运行 `sudo apt-get install openssh-client` |
| RHEL / Fedora / CentOS                    | Run `sudo yum install openssh-clients` 运行 `sudo yum install openssh-clients` |

VS Code will look for the `ssh` command in the PATH. Failing that, on Windows it will attempt to find `ssh.exe` in the default Git for Windows install path. You can also specifically tell VS Code where to find the SSH client by adding the `remote.SSH.path` property to `settings.json`.

​​	VS Code 将在 PATH 中查找 `ssh` 命令。如果失败，它将在 Windows 上尝试在默认的适用于 Windows 的 Git 安装路径中查找 `ssh.exe` 。您还可以通过将 `remote.SSH.path` 属性添加到 `settings.json` 中来明确告诉 VS Code 在哪里查找 SSH 客户端。

### [Installing a supported SSH server 安装受支持的 SSH 服务器]({{< ref "/Remote/TipsandTricks#_installing-a-supported-ssh-server" >}})

| OS                                        | Instructions 说明                                            | Details 详细信息                                             |
| :---------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Debian 8+ / Ubuntu 16.04+                 | Run `sudo apt-get install openssh-server` 运行 `sudo apt-get install openssh-server` | See the [Ubuntu SSH](https://help.ubuntu.com/community/SSH?action=show) documentation for details. 有关详细信息，请参阅 Ubuntu SSH 文档。 |
| RHEL / CentOS 7+                          | Run `sudo yum install openssh-server && sudo systemctl start sshd.service && sudo systemctl enable sshd.service` 运行 `sudo yum install openssh-server && sudo systemctl start sshd.service && sudo systemctl enable sshd.service` | See the [RedHat SSH](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh) documentation for details. 有关详细信息，请参阅 RedHat SSH 文档。 |
| SuSE 12+ / openSUSE 42.3+                 | In Yast, go to Services Manager, select "sshd" in the list, and click **Enable**. Next go to Firewall, select the **Permanent** configuration, and under services check **sshd**. 在 Yast 中，转到服务管理器，在列表中选择“sshd”，然后单击启用。接下来转到防火墙，选择永久配置，然后在服务下检查 sshd。 | See the [SuSE SSH](https://en.opensuse.org/OpenSSH) documentation for details. 有关详细信息，请参阅 SuSE SSH 文档。 |
| Windows 10 1803+ / Server 2016/2019 1803+ | Install the [Windows OpenSSH Server](https://learn.microsoft.com/windows-server/administration/openssh/openssh_install_firstuse). 安装 Windows OpenSSH 服务器。 |                                                              |
| macOS 10.14+ (Mojave)                     | Enable [Remote Login](https://support.apple.com/guide/mac-help/allow-a-remote-computer-to-access-your-mac-mchlp1066/mac). 启用远程登录。 |                                                              |

### [Resolving hangs when doing a Git push or sync on an SSH host 在 SSH 主机上执行 Git 推送或同步时解决挂起问题]({{< ref "/Remote/TipsandTricks#_resolving-hangs-when-doing-a-git-push-or-sync-on-an-ssh-host" >}})

If you clone a Git repository using SSH and your SSH key has a passphrase, VS Code's pull and sync features may hang when running remotely.

​​	如果您使用 SSH 克隆 Git 存储库，并且您的 SSH 密钥有密码，则在远程运行时，VS Code 的拉取和同步功能可能会挂起。

Either use an SSH key without a passphrase, clone using HTTPS, or run `git push` from the command line to work around the issue.

​​	可以使用没有密码的 SSH 密钥，使用 HTTPS 克隆，或从命令行运行 `git push` 来解决此问题。

### [Using SSHFS to access files on your remote host 使用 SSHFS 访问远程主机上的文件]({{< ref "/Remote/TipsandTricks#_using-sshfs-to-access-files-on-your-remote-host" >}})

[SSHFS](https://en.wikipedia.org/wiki/SSHFS) is a secure remote filesystem access protocol that builds up from SFTP. It provides advantages over something like a CIFS / Samba share in that all that is required is SSH access to the machine.

​​	SSHFS 是一个安全的远程文件系统访问协议，由 SFTP 构建而成。与 CIFS / Samba 共享相比，它的优势在于只需要对计算机进行 SSH 访问。

> **Note:** For performance reasons, SSHFS is best used for single file edits and uploading/downloading content. If you need to use an application that bulk reads/write to many files at once (like a local source control tool), [rsync]({{< ref "/Remote/TipsandTricks#_using-rsync-to-maintain-a-local-copy-of-your-source-code" >}}) is a better choice.
>
> ​​	注意：出于性能原因，SSHFS 最适合用于编辑单个文件和上传/下载内容。如果您需要使用一次性批量读/写多个文件的应用程序（如本地源代码管理工具），rsync 是更好的选择。

**macOS / Linux**:

​​	macOS/Linux：

On Linux, you can use your distribution's package manager to install SSHFS. For Debian/Ubuntu: `sudo apt-get install sshfs`

​​	在 Linux 上，您可以使用发行版的软件包管理器来安装 SSHFS。对于 Debian/Ubuntu： `sudo apt-get install sshfs`

> **Note:** WSL 1 does not support FUSE or SSHFS, so the instructions differ for Windows currently. **WSL 2 does include FUSE and SSHFS support**, so this will change soon.
>
> ​​	注意：WSL 1 不支持 FUSE 或 SSHFS，因此 Windows 目前使用的说明有所不同。WSL 2 包括 FUSE 和 SSHFS 支持，因此这种情况很快就会改变。

On macOS, you can install SSHFS using [Homebrew](https://brew.sh/):

​​	在 macOS 上，您可以使用 Homebrew 安装 SSHFS：

```
brew install --cask macfuse
brew install gromgit/fuse/sshfs-mac
brew link --overwrite sshfs-mac
```

In addition, if you would prefer not to use the command line to mount the remote filesystem, you can also install [SSHFS GUI](https://github.com/dstuecken/sshfs-gui).

​​	此外，如果您不想使用命令行来挂载远程文件系统，还可以安装 SSHFS GUI。

To use the command line, run the following commands from a local terminal (replacing `user@hostname` with the remote user and hostname / IP):

​​	要使用命令行，请从本地终端运行以下命令（用远程用户和主机名/IP 替换 `user@hostname` ）：

```
export USER_AT_HOST=user@hostname
# Make the directory where the remote filesystem will be mounted
mkdir -p "$HOME/sshfs/$USER_AT_HOST"
# Mount the remote filesystem
sshfs "$USER_AT_HOST:" "$HOME/sshfs/$USER_AT_HOST" -ovolname="$USER_AT_HOST" -p 22  \
    -o workaround=nonodelay -o transform_symlinks -o idmap=user  -C
```

This will make your home folder on the remote machine available under the `~/sshfs`. When you are done, you can unmount it using your OS's Finder / file explorer or by using the command line:

​​	这会使远程计算机上的您的主文件夹在 `~/sshfs` 下可用。完成后，您可以使用操作系统的 Finder/文件资源管理器或使用命令行将其卸载：

```
umount "$HOME/sshfs/$USER_AT_HOST"
```

**Windows:
Windows：**

Follow these steps:

​​	请按照以下步骤操作：

1. On Linux, add `.gitattributes` file to your project to **force consistent line endings** between Linux and Windows to avoid unexpected issues due to CRLF/LF differences between the two operating systems. See [Resolving Git line ending issues]({{< ref "/Remote/TipsandTricks#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files" >}}) for details.

   ​​	在 Linux 上，将 `.gitattributes` 文件添加到您的项目中，以强制在 Linux 和 Windows 之间使用一致的行尾，以避免由于这两个操作系统之间的 CRLF/LF 差异而导致意外问题。有关详细信息，请参阅解决 Git 换行符问题。

2. Next, install [SSHFS-Win](https://github.com/billziss-gh/sshfs-win) using [Chocolatey](https://chocolatey.org/): `choco install sshfs`

   ​​	接下来，使用 Chocolatey 安装 SSHFS-Win： `choco install sshfs`

3. Once you've installed SSHFS for Windows, you can use the File Explorer's **Map Network Drive...** option with the path `\\sshfs\user@hostname`, where `user@hostname` is your remote user and hostname / IP. You can script this using the command prompt as follows: `net use /PERSISTENT:NO X: \\sshfs\user@hostname`

   ​​	安装了适用于 Windows 的 SSHFS 后，您可以使用文件资源管理器的“映射网络驱动器...”选项，其中路径为 `\\sshfs\user@hostname` ，其中 `user@hostname` 是您的远程用户和主机名/IP。您可以使用命令提示符按如下方式编写脚本： `net use /PERSISTENT:NO X: \\sshfs\user@hostname`

4. Once done, disconnect by right-clicking on the drive in the File Explorer and selecting **Disconnect**.

   ​​	完成后，右键单击文件资源管理器中的驱动器并选择“断开连接”以断开连接。

### [Connect to a remote host from the terminal 从终端连接到远程主机]({{< ref "/Remote/TipsandTricks#_connect-to-a-remote-host-from-the-terminal" >}})

Once a host has been configured, you can connect to it directly from the terminal by passing a remote URI.

​​	配置好主机后，您可以通过传递远程 URI 直接从终端连接到该主机。

For example, to connect to `remote_server` and open the `/code/my_project` folder, run:

​​	例如，要连接到 `remote_server` 并打开 `/code/my_project` 文件夹，请运行：

```
code --remote ssh-remote+remote_server /code/my_project
```

We need to do some guessing on whether the input path is a file or a folder. If it has a file extension, it is considered a file.

​​	我们需要猜测输入路径是文件还是文件夹。如果它具有文件扩展名，则认为它是一个文件。

To force that a folder is opened, add slash to the path or use:

​​	要强制打开文件夹，请在路径中添加斜杠或使用：

```
code --folder-uri vscode-remote://ssh-remote+remote_server/code/folder.with.dot
```

To force that a file is opened, add `--goto` or use:

​​	要强制打开文件，请添加 `--goto` 或使用：

```
code --file-uri vscode-remote://ssh-remote+remote_server/code/fileWithoutExtension
```

### [Using rsync to maintain a local copy of your source code 使用 rsync 维护源代码的本地副本]({{< ref "/Remote/TipsandTricks#_using-rsync-to-maintain-a-local-copy-of-your-source-code" >}})

An alternative to [using SSHFS to access remote files]({{< ref "/Remote/TipsandTricks#_using-sshfs-to-access-files-on-your-remote-host" >}}) is to [use `rsync`](https://rsync.samba.org/) to copy the entire contents of a folder on remote host to your local machine. The `rsync` command will determine which files need to be updated each time it is run, which is far more efficient and convenient than using something like `scp` or `sftp`. This is primarily something to consider if you really need to use multi-file or performance intensive local tools.

​​	除了使用 SSHFS 访问远程文件外，还可以使用 `rsync` 将远程主机上文件夹的全部内容复制到本地计算机。每次运行 `rsync` 命令时，它都会确定哪些文件需要更新，这比使用 `scp` 或 `sftp` 之类的东西要高效和方便得多。如果您确实需要使用多文件或性能密集型本地工具，则主要需要考虑这一点。

The `rsync` command is available out of box on macOS and can be installed using Linux package managers (for example `sudo apt-get install rsync` on Debian/Ubuntu). For Windows, you'll need to either use [WSL](https://learn.microsoft.com/windows/wsl/install) or [Cygwin](https://www.cygwin.com/) to access the command.

​​	在 macOS 上， `rsync` 命令开箱即用，并且可以使用 Linux 包管理器（例如 Debian/Ubuntu 上的 `sudo apt-get install rsync` ）进行安装。对于 Windows，您需要使用 WSL 或 Cygwin 来访问该命令。

To use the command, navigate to the folder you want to store the synched contents and run the following replacing `user@hostname` with the remote user and hostname / IP and `/remote/source/code/path` with the remote source code location.

​​	要使用该命令，请导航到要存储同步内容的文件夹，并运行以下命令，将 `user@hostname` 替换为远程用户和主机名/IP，将 `/remote/source/code/path` 替换为远程源代码位置。

On **macOS, Linux, or inside WSL**:

​​	在 macOS、Linux 或 WSL 内部：

```
rsync -rlptzv --progress --delete --exclude=.git "user@hostname:/remote/source/code/path" .
```

Or using **WSL from PowerShell on Windows**:

​​	或在 Windows 上使用 PowerShell 从 WSL 中使用：

```
wsl rsync -rlptzv --progress --delete --exclude=.git "user@hostname:/remote/source/code/path" "`$(wslpath -a '$PWD')"
```

You can rerun this command each time you want to get the latest copy of your files and only updates will be transferred. The `.git` folder is intentionally excluded both for performance reasons and so you can use local Git tools without worrying about the state on the remote host.

​​	每次想要获取文件的最新副本时，都可以重新运行此命令，并且只会传输更新。出于性能原因，有意排除了 `.git` 文件夹，这样您就可以使用本地 Git 工具，而不用担心远程主机上的状态。

To push content, reverse the source and target parameters in the command. However, **on Windows** you should add a `.gitattributes` file to your project to **force consistent line endings** before doing so. See [Resolving Git line ending issues]({{< ref "/Remote/TipsandTricks#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files" >}}) for details.

​​	要推送内容，请在命令中反转源和目标参数。但是，在 Windows 上，您应该在执行此操作之前向项目添加 `.gitattributes` 文件，以强制使用一致的行尾。有关详细信息，请参阅解决 Git 行尾问题。

```
rsync -rlptzv --progress --delete --exclude=.git . "user@hostname:/remote/source/code/path"
```

### [Cleaning up the VS Code Server on the remote 清理远程上的 VS Code Server]({{< ref "/Remote/TipsandTricks#_cleaning-up-the-vs-code-server-on-the-remote" >}})

The SSH extension provides a command for cleaning up the VS Code Server from the remote machine, **Remote-SSH: Uninstall VS Code Server from Host...**. The command does two things: it kills any running VS Code Server processes and it deletes the folder where the server was installed.

​​	SSH 扩展提供了一个用于从远程计算机清理 VS Code Server 的命令，Remote-SSH：从主机卸载 VS Code Server.... 该命令执行两项操作：它会终止所有正在运行的 VS Code Server 进程，并删除安装服务器的文件夹。

If you want to run these steps manually, or if the command isn't working for you, you can run a script like this:

​​	如果您想手动运行这些步骤，或者命令对您不起作用，您可以运行类似这样的脚本：

```
# Kill server processes
kill -9 $(ps aux | grep vscode-server | grep $USER | grep -v grep | awk '{print $2}')
# Delete related files and folder
rm -rf $HOME/.vscode-server # Or ~/.vscode-server-insiders
```

The VS Code Server was previously installed under `~/.vscode-remote` so you can check that location too.

​​	VS Code Server 之前安装在 `~/.vscode-remote` 下，因此您也可以检查该位置。

### [SSH into a remote WSL 2 host SSH 登录到远程 WSL 2 主机]({{< ref "/Remote/TipsandTricks#_ssh-into-a-remote-wsl-2-host" >}})

You may want to use SSH to connect to a WSL distro running on your remote machine. Check out [this guide](https://www.hanselman.com/blog/the-easy-way-how-to-ssh-into-bash-and-wsl2-on-windows-10-from-an-external-machine) to learn how to SSH into Bash and WSL 2 on Windows 10 from an external machine.

​​	您可能希望使用 SSH 连接到远程计算机上运行的 WSL 发行版。查看本指南，了解如何在外部计算机上通过 SSH 登录到 Windows 10 上的 Bash 和 WSL 2。

## [Dev Containers tips Dev Containers 提示]({{< ref "/Remote/TipsandTricks#_dev-containers-tips" >}})

If you'd like to read about tips for using Dev Containers, you can go to Dev Containers [Tips and Tricks]({{< ref "/DevContainers/TipsandTricks" >}}).

​​	如果您想阅读有关使用 Dev Containers 的提示，可以转到 Dev Containers 提示和技巧。

## [WSL tips WSL 提示]({{< ref "/Remote/TipsandTricks#_wsl-tips" >}})

### [First time start: VS Code Server prerequisites 首次启动：VS Code Server 先决条件]({{< ref "/Remote/TipsandTricks#_first-time-start-vs-code-server-prerequisites" >}})

Some WSL Linux distributions are lacking libraries that are required by the VS Code server to start up. You can add additional libraries into your Linux distribution by using its package manager.

​​	某些 WSL Linux 发行版缺少 VS Code 服务器启动所需的库。您可以使用其软件包管理器向 Linux 发行版中添加其他库。

#### [Debian and Ubuntu Debian 和 Ubuntu]({{< ref "/Remote/TipsandTricks#_debian-and-ubuntu" >}})

Open the Debian or Ubuntu WSL shell to add `wget` and `ca-certificates`:

​​	打开 Debian 或 Ubuntu WSL shell 以添加 `wget` 和 `ca-certificates` ：

```
sudo apt-get update && sudo apt-get install wget ca-certificates
```

#### [Alpine]({{< ref "/Remote/TipsandTricks#_alpine" >}})

Open the Alpine WSL shell as root (`wsl -d Alpine -u root`) to add `libstdc++`:

​​	以 root 身份打开 Alpine WSL shell ( `wsl -d Alpine -u root` ) 以添加 `libstdc++` ：

```
apk update && apk add libstdc++
```

On Windows 10 April 2018 Update (build 1803) and older, `/bin/bash` is required:

​​	在 Windows 10 April 2018 更新 (内部版本 1803) 及更早版本中，需要 `/bin/bash` ：

```
apk update && apk add bash
```

### [Selecting the distribution used by the WSL extension 选择 WSL 扩展程序使用的发行版]({{< ref "/Remote/TipsandTricks#_selecting-the-distribution-used-by-the-wsl-extension" >}})

**WSL: New Window** will open the WSL distro registered as default.

​​	WSL：新窗口将打开注册为默认值 WSL 发行版。

To open a non-default distro, run `code .` from the WSL shell of the distro to use or use **WSL: New Window using Distro**.

​​	要打开非默认发行版，请从要使用的发行版的 WSL shell 运行 `code .` 或使用 WSL：使用发行版的新窗口。

With WSL versions older than Windows 10, May 2019 Update (version 1903), the WSL command can only use the **default distro**. For this reason, the WSL extension might prompt you if you agree to change the default distro.

​​	对于早于 Windows 10，2019 年 5 月更新 (版本 1903) 的 WSL 版本，WSL 命令只能使用默认发行版。因此，WSL 扩展程序可能会提示您是否同意更改默认发行版。

You can always use [wslconfig.exe](https://learn.microsoft.com/windows/wsl/wsl-config) to change your default.

​​	您始终可以使用 wslconfig.exe 更改默认值。

For example:

​​	例如：

```
wslconfig /setdefault Ubuntu
```

You can see which distributions you have installed by running:

​​	您可以通过运行以下命令查看已安装的发行版：

```
wslconfig /l
```

### [Configure the environment for the server startup 为服务器启动配置环境]({{< ref "/Remote/TipsandTricks#_configure-the-environment-for-the-server-startup" >}})

When the WSL extension starts the VS Code server in WSL, it does not run any shell configuration scripts. This was done to avoid that custom configuration scripts can prevent the startup.

​​	当 WSL 扩展在 WSL 中启动 VS Code 服务器时，它不会运行任何 shell 配置脚本。这样做是为了避免自定义配置脚本阻止启动。

If you need to configure the startup environment, you can use the environment setup script as described [here]({{< ref "/Remote/WindowsSubsystemforLinux#_advanced-environment-setup-script" >}}).

​​	如果您需要配置启动环境，可以使用此处描述的环境设置脚本。

### [Configure the environment for the remote extension host 为远程扩展主机配置环境]({{< ref "/Remote/TipsandTricks#_configure-the-environment-for-the-remote-extension-host" >}})

The environment for the remote extension host and terminal are based on the default shell's configuration scripts. To evaluate the environment variables for the remote extension host process, the server creates an instance of the default shell as an **interactive login shell**. It probes the environment variables from it and uses them as the initial environment for the remote extension host process. The values of environment variables therefore depend on what shell is configured as the default and the content of the configuration scripts for that shell.

​​	远程扩展主机和终端的环境基于默认 shell 的配置脚本。为了评估远程扩展主机进程的环境变量，服务器将默认 shell 的一个实例创建为交互式登录 shell。它从中探测环境变量，并将它们用作远程扩展主机进程的初始环境。因此，环境变量的值取决于将哪个 shell 配置为默认 shell，以及该 shell 的配置脚本的内容。

See [Unix shell initialization](https://github.com/rbenv/rbenv/wiki/unix-shell-initialization) for an overview of each shell's configuration scripts. Most WSL distributions have `/bin/bash` configured as the default shell. `/bin/bash` will look for startup files under `/etc/profile` first and for any startup files under `~/.bash_profile`, `~/.bash_login`, `~/.profile`.

​​	有关每个 shell 的配置文件脚本的概述，请参阅 Unix shell 初始化。大多数 WSL 发行版已将 `/bin/bash` 配置为默认 shell。 `/bin/bash` 将首先查找 `/etc/profile` 下的启动文件，然后查找 `~/.bash_profile` 、 `~/.bash_login` 、 `~/.profile` 下的任何启动文件。

To change the default shell of a WSL distro, follow the instructions of [this blog post](https://medium.com/@vinhp/set-and-use-zsh-as-default-shell-in-wsl-on-windows-10-the-right-way-4f30ed9592dc).

​​	要更改 WSL 发行版的默认 shell，请按照此博客文章中的说明进行操作。

### [Fixing problems with the code command not working 修复 code 命令无法正常工作的相关问题]({{< ref "/Remote/TipsandTricks#_fixing-problems-with-the-code-command-not-working" >}})

If typing `code` from a WSL terminal on Window does not work because `code` cannot be found, you may be missing some key locations from your PATH in WSL.

​​	如果在 Windows 上的 WSL 终端中键入 `code` 不起作用，因为找不到 `code` ，则 WSL 中的 PATH 中可能缺少一些关键位置。

Check by opening a WSL terminal and typing `echo $PATH`. You should see VS Code install path listed. By default, this would be:

​​	通过打开 WSL 终端并键入 `echo $PATH` 进行检查。您应该会看到列出的 VS Code 安装路径。默认情况下，这将是：

```
/mnt/c/Users/Your Username/AppData/Local/Programs/Microsoft VS Code/bin
```

But, if you used the **System Installer**, the install path is:

​​	但是，如果您使用的是系统安装程序，则安装路径为：

```
/mnt/c/Program Files/Microsoft VS Code/bin
```

...or...

​​	...或...

```
/mnt/c/Program Files (x86)/Microsoft VS Code/bin
```

It's a feature of WSL that paths are inherited from the PATH variable in Windows. To change the Windows PATH variable, use the **Edit environment variables for your account** command from the start menu in Windows.

​​	WSL 的一个特点是路径是从 Windows 中的 PATH 变量继承的。要更改 Windows PATH 变量，请在 Windows 的开始菜单中使用“为您的帐户编辑环境变量”命令。

If you have disabled the path sharing feature, edit your `.bashrc`, add the following, and start a new terminal:

​​	如果您已禁用路径共享功能，请编辑您的 `.bashrc` ，添加以下内容，然后启动一个新终端：

```
WINDOWS_USERNAME="Your Windows Alias"

export PATH="$PATH:/mnt/c/Windows/System32:/mnt/c/Users/${WINDOWS_USERNAME}/AppData/Local/Programs/Microsoft VS Code/bin"
# or...
# export PATH="$PATH:/mnt/c/Program Files/Microsoft VS Code/bin"
# or...
# export PATH="$PATH:/mnt/c/Program Files (x86)/Microsoft VS Code/bin"
```

> **Note:** Be sure to quote or escape space characters in the directory names.
>
> ​​	注意：务必对目录名称中的空格字符加上引号或转义符。

### [Finding problems with the 'code' command 查找“代码”命令的问题]({{< ref "/Remote/TipsandTricks#_finding-problems-with-the-code-command" >}})

If typing `code` from a Windows command prompt does not launch VS Code, you can help us diagnose the problem by running `VSCODE_WSL_DEBUG_INFO=true code .`.

​​	如果从 Windows 命令提示符键入 `code` 不会启动 VS Code，你可以通过运行 `VSCODE_WSL_DEBUG_INFO=true code .` 来帮助我们诊断问题。

Please file an issue and attach the full output.

​​	请提交一个问题并附上完整输出。

### [Finding problems starting or connected to the server 查找启动或连接到服务器时的问题]({{< ref "/Remote/TipsandTricks#_finding-problems-starting-or-connected-to-the-server" >}})

When the WSL window fails to connect to the remote server, you can get more information in the WSL log. When filing an issue, it is important to always send the full content of the WSL log.

​​	当 WSL 窗口无法连接到远程服务器时，你可以在 WSL 日志中获取更多信息。提交问题时，务必始终发送 WSL 日志的完整内容。

Open the WSL log by running the command **WSL: Open Log**. The log will show in the terminal view under the WSL tab.

​​	通过运行命令 WSL: 打开日志来打开 WSL 日志。日志将显示在 WSL 选项卡下的终端视图中。

![WSL Log](./TipsandTricks_img/wsl-log.png)

To get even more verbose logging, enable the setting `remote.WSL.debug` in the user settings.

​​	要获取更详细的日志记录，请在用户设置中启用设置 `remote.WSL.debug` 。

### [The server fails to start with a segmentation fault 服务器因段错误而无法启动]({{< ref "/Remote/TipsandTricks#_the-server-fails-to-start-with-a-segmentation-fault" >}})

You can help us investigate this problem by sending us the core dump file. To get the core dump file, follow these steps:

​​	你可以通过向我们发送核心转储文件来帮助我们调查此问题。要获取核心转储文件，请按照以下步骤操作：

In a Windows command prompt:

​​	在 Windows 命令提示符中：

- Run `code --locate-extension ms-vscode-remote.remote-wsl` to determine the WSL extension folder.
  运行 `code --locate-extension ms-vscode-remote.remote-wsl` 以确定 WSL 扩展文件夹。
- `cd` to the path that is returned.
  到返回的路径。
- Open the `wslServer.sh` script with VS Code, `code .\scripts\wslServer.sh`.
  使用 VS Code 打开 `wslServer.sh` 脚本， `code .\scripts\wslServer.sh` 。
- Before the last line (before `"$VSCODE_REMOTE_BIN/$COMMIT/bin/$SERVER_APPNAME" "$@"`), add `ulimit -C unlimited`.
  在最后一行之前（在 `"$VSCODE_REMOTE_BIN/$COMMIT/bin/$SERVER_APPNAME" "$@"` 之前），添加 `ulimit -C unlimited` 。
- Start the WSL window running the remote server and wait for the segmentation fault.
  启动运行远程服务器的 WSL 窗口，并等待段错误。

The core file will be in the WSL extension folder from above.

​​	核心文件将位于上述 WSL 扩展文件夹中。

### [I see EACCES: permission denied error trying to rename a folder in the open workspace 我看到 EACCES：尝试重命名打开工作区中的文件夹时出现权限被拒绝错误]({{< ref "/Remote/TipsandTricks#_i-see-eacces-permission-denied-error-trying-to-rename-a-folder-in-the-open-workspace" >}})

This is a known problem with the WSL file system implementation ([Microsoft/WSL#3395](https://github.com/microsoft/WSL/issues/3395), [Microsoft/WSL#1956](https://github.com/microsoft/WSL/issues/1956)) caused by the file watcher active by VS Code. The issue will only be fixed in WSL 2.

​​	这是 WSL 文件系统实现（Microsoft/WSL#3395、Microsoft/WSL#1956）的一个已知问题，由 VS Code 激活的文件观察程序导致。此问题仅在 WSL 2 中修复。

To avoid the issue, set `remote.WSL.fileWatcher.polling` to true. However, polling based has a performance impact for large workspaces.

​​	若要避免此问题，请将 `remote.WSL.fileWatcher.polling` 设置为 true。但是，基于轮询的方式对大型工作区有性能影响。

For large workspace you may want to increase the polling interval, `remote.WSL.fileWatcher.pollingInterval`, and control the folders that are watched with `files.watcherExclude`.

​​	对于大型工作区，您可能需要增加轮询间隔， `remote.WSL.fileWatcher.pollingInterval` ，并使用 `files.watcherExclude` 控制受监视的文件夹。

[WSL 2](https://learn.microsoft.com/windows/wsl/compare-versions#whats-new-in-wsl-2) does not have that file watcher problem and is not affected by the new setting.

​​	WSL 2 没有该文件观察程序问题，不受新设置的影响。

### [Resolving Git line ending issues in WSL (resulting in many modified files) 解决 WSL 中的 Git 换行符问题（导致许多文件被修改）]({{< ref "/Remote/TipsandTricks#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files" >}})

Since Windows and Linux use different default line endings, Git may report a large number of modified files that have no differences aside from their line endings. To prevent this from happening, you can disable line-ending conversion using a `.gitattributes` file or globally on the Windows side.

​​	由于 Windows 和 Linux 使用不同的默认换行符，Git 可能会报告大量修改过的文件，除了换行符之外没有任何差异。若要防止这种情况发生，可以使用 `.gitattributes` 文件或在 Windows 端全局禁用换行符转换。

Typically adding or modifying a `.gitattributes` file in your repository is the most reliable way to solve this problem. Committing this file to source control will help others and allows you to vary behaviors by repository as appropriate. For example, adding the following to `.gitattributes` file to the root of your repository will force everything to be LF, except for Windows batch files that require CRLF:

​​	通常，在存储库中添加或修改 `.gitattributes` 文件是解决此问题的最可靠方法。将此文件提交到源代码管理将对其他人有所帮助，并允许您根据需要按存储库更改行为。例如，将以下内容添加到存储库根目录的 `.gitattributes` 文件中，将强制所有内容为 LF，但需要 CRLF 的 Windows 批处理文件除外：

```
* text=auto eol=lf
*.{cmd,[cC][mM][dD]} text eol=crlf
*.{bat,[bB][aA][tT]} text eol=crlf
```

Note that this works in **Git v2.10+**, so if you are running into problems, be sure you've got a recent Git client installed. You can add other file types in your repository that require CRLF to this same file.

​​	请注意，此方法适用于 Git v2.10+，因此如果您遇到问题，请确保已安装最新的 Git 客户端。您可以在存储库中添加其他需要 CRLF 的文件类型到此相同的文件。

If you would prefer to still always upload Unix-style line endings (LF), you can use the `input` option.

​​	如果您仍希望始终上传 Unix 风格的换行符 (LF)，可以使用 `input` 选项。

```
git config --global core.autocrlf input
```

If you'd prefer to disable line-ending conversion entirely, run the following instead:

​​	如果您更愿意完全禁用行尾转换，请改而运行以下命令：

```
git config --global core.autocrlf false
```

Finally, you may need to clone the repository again for these settings to take effect.

​​	最后，您可能需要再次克隆存储库，才能使这些设置生效。

### [Sharing Git credentials between Windows and WSL 在 Windows 和 WSL 之间共享 Git 凭据]({{< ref "/Remote/TipsandTricks#_sharing-git-credentials-between-windows-and-wsl" >}})

If you use HTTPS to clone your repositories and **have a [credential helper configured](https://docs.github.com/get-started/getting-started-with-git/caching-your-github-credentials-in-git) in Windows**, you can share this with WSL so that passwords you enter are persisted on both sides. (Note that this does not apply to using SSH keys.)

​​	如果您使用 HTTPS 克隆存储库，并在 Windows 中配置了凭据帮助程序，则可以与 WSL 共享此凭据，以便您输入的密码在双方都保持不变。（请注意，这不适用于使用 SSH 密钥。）

Just follow these steps:

​​	只需按照以下步骤操作：

1. Configure the credential manager on Windows by running the following in a **Windows command prompt** or **PowerShell**:

   ​​	通过在 Windows 命令提示符或 PowerShell 中运行以下命令，在 Windows 上配置凭据管理器：

   ```
    git config --global credential.helper wincred
   ```

2. Configure WSL to use the same credential helper, but running the following in a **WSL terminal**:

   ​​	通过在 WSL 终端中运行以下命令，将 WSL 配置为使用相同的凭据帮助程序：

   ```
    git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager-core.exe"
   ```

Any password you enter when working with Git on the Windows side will now be available to WSL and vice versa.

​​	现在，您在 Windows 端使用 Git 时输入的任何密码都可供 WSL 使用，反之亦然。

### [Resolving hangs when doing a Git push or sync from WSL 在从 WSL 执行 Git 推送或同步时解决挂起问题]({{< ref "/Remote/TipsandTricks#_resolving-hangs-when-doing-a-git-push-or-sync-from-wsl" >}})

If you clone a Git repository using SSH and your SSH key has a passphrase, VS Code's pull and sync features may hang when running remotely.

​​	如果您使用 SSH 克隆 Git 存储库，并且您的 SSH 密钥具有密码，则在远程运行时，VS Code 的拉取和同步功能可能会挂起。

Either use an SSH key without a passphrase, clone using HTTPS, or run `git push` from the command line to work around the issue.

​​	要解决此问题，可以使用没有密码的 SSH 密钥、使用 HTTPS 克隆或从命令行运行 `git push` 。

## [GitHub Codespaces tips GitHub Codespaces 提示]({{< ref "/Remote/TipsandTricks#_github-codespaces-tips" >}})

For tips and questions about [GitHub Codespaces](https://github.com/features/codespaces), see the [GitHub Codespaces documentation](https://docs.github.com/github/developing-online-with-codespaces). You can also check out the [known web limitations and adaptations]({{< ref "/Remote/GitHubCodespaces#_known-limitations-and-adaptations" >}}) that may impact your Codespaces.

​​	有关 GitHub Codespaces 的提示和问题，请参阅 GitHub Codespaces 文档。您还可以查看可能影响您的 Codespaces 的已知 Web 限制和改编。

## [Extension tips 扩展提示]({{< ref "/Remote/TipsandTricks#_extension-tips" >}})

While many extensions will work unmodified, there are a few issues that can prevent certain features from working as expected. In some cases, you can use another command to work around the issue, while in others, the extension may need to be modified. This section provides a quick reference for common issues and tips on resolving them. You can also refer to the main extension article on [Supporting Remote Development](https://code.visualstudio.com/api/advanced-topics/remote-extensions) for an in-depth guide on modifying extensions to support remote extension hosts.

​​	虽然许多扩展将按原样工作，但有一些问题可能会阻止某些功能按预期工作。在某些情况下，您可以使用另一个命令来解决此问题，而在其他情况下，可能需要修改扩展。本部分提供了常见问题和解决问题的提示的快速参考。您还可以参考关于支持远程开发的主要扩展文章，以获取有关修改扩展以支持远程扩展主机的深入指南。

### [Resolving errors about missing dependencies 解决有关缺少依赖项的错误]({{< ref "/Remote/TipsandTricks#_resolving-errors-about-missing-dependencies" >}})

Some extensions rely on libraries not found in the basic install of certain WSL Linux distributions. You can add additional libraries into your Linux distribution by using its package manager. For Ubuntu and Debian based distributions, run `sudo apt-get install <package>` to install the needed libraries. Check the documentation for your extension or the runtime that is mentioned in the error message for additional installation details.

​​	某些扩展依赖于某些 WSL Linux 发行版的基本安装中找不到的库。您可以使用其软件包管理器向 Linux 发行版中添加其他库。对于基于 Ubuntu 和 Debian 的发行版，运行 `sudo apt-get install <package>` 以安装所需的库。查看扩展的文档或错误消息中提到的运行时以获取其他安装详细信息。

### [Local absolute path settings fail when applied remotely 应用时本地绝对路径设置失败]({{< ref "/Remote/TipsandTricks#_local-absolute-path-settings-fail-when-applied-remotely" >}})

VS Code's local user settings are reused when you connect to a remote endpoint. While this keeps your user experience consistent, you may need to vary absolute path settings between your local machine and each host / container / WSL since the target locations are different.

​​	当您连接到远程端点时，VS Code 的本地用户设置会被重复使用。虽然这使您的用户体验保持一致，但您可能需要在本地计算机和每个主机/容器/WSL 之间改变绝对路径设置，因为目标位置不同。

**Resolution:** You can set endpoint-specific settings after you connect to a remote endpoint by running the **Preferences: Open Remote Settings** command from the Command Palette (F1) or by selecting the **Remote** tab in the Settings editor. These settings will override any local settings you have in place whenever you connect.

​​	解决方法：连接到远程端点后，您可以通过从命令面板 (F1) 运行“首选项：打开远程设置”命令或在“设置”编辑器中选择“远程”选项卡来设置特定于端点的设置。无论何时连接，这些设置都会覆盖您已设置的任何本地设置。

### [Need to install local VSIX on remote endpoint 需要在远程端点上安装本地 VSIX]({{< ref "/Remote/TipsandTricks#_need-to-install-local-vsix-on-remote-endpoint" >}})

Sometimes you want to install a local VSIX on a remote machine, either during development or when an extension author asks you to try out a fix.

​​	有时您想在远程计算机上安装本地 VSIX，无论是在开发期间还是当扩展作者要求您尝试修复时。

**Resolution:** Once you have connected to an SSH host, container, or WSL, you can install the VSIX the same way you would locally. Run the **Extensions: Install from VSIX...** command from the Command Palette (F1). You may also want to add `"extensions.autoUpdate": false` to `settings.json` to prevent auto-updating to the latest Marketplace version. See [Supporting Remote Development](https://code.visualstudio.com/api/advanced-topics/remote-extensions) for more information on developing and testing extensions in a remote environment.

​​	解决方案：连接到 SSH 主机、容器或 WSL 后，您可以像在本地一样安装 VSIX。从命令面板 (F1) 运行扩展：从 VSIX 安装... 命令。您可能还希望将 `"extensions.autoUpdate": false` 添加到 `settings.json` 以防止自动更新到最新的 Marketplace 版本。有关在远程环境中开发和测试扩展的详细信息，请参阅支持远程开发。

### [Browser does not open locally 浏览器未在本地打开]({{< ref "/Remote/TipsandTricks#_browser-does-not-open-locally" >}})

Some extensions use external node modules or custom code to launch a browser window. Unfortunately, this may cause the extension to launch the browser remotely instead of locally.

​​	某些扩展使用外部节点模块或自定义代码来启动浏览器窗口。遗憾的是，这可能导致扩展在远程而不是本地启动浏览器。

**Resolution:** The extension can use the `vscode.env.openExternal` API to resolve this problem. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#opening-something-in-a-local-browser-or-application) for details.

​​	解决方案：扩展可以使用 `vscode.env.openExternal` API 来解决此问题。有关详细信息，请参阅扩展作者指南。

### [Clipboard does not work 剪贴板不起作用]({{< ref "/Remote/TipsandTricks#_clipboard-does-not-work" >}})

Some extensions use node modules like `clipboardy` to integrate with the clipboard. Unfortunately, this may cause the extension to incorrectly integrate with the clipboard on the remote side.

​​	某些扩展使用诸如 `clipboardy` 之类的节点模块与剪贴板集成。遗憾的是，这可能导致扩展与远程端的剪贴板集成不正确。

**Resolution:** The extension can switch to the VS Code clipboard API to resolve the problem. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#using-the-clipboard) for details.

​​	解决方案：扩展程序可以切换到 VS Code 剪贴板 API 来解决此问题。有关详细信息，请参阅扩展程序作者指南。

### [Cannot access local web server from browser or application 无法从浏览器或应用程序访问本地 Web 服务器]({{< ref "/Remote/TipsandTricks#_cannot-access-local-web-server-from-browser-or-application" >}})

When working inside a container, SSH host, or through GitHub Codespaces, the port the browser is connecting to may be blocked.

​​	在容器、SSH 主机或通过 GitHub Codespaces 内部工作时，浏览器连接到的端口可能会被阻止。

**Resolution:** Extensions can use the `vscode.env.openExternal` or `vscode.env.asExternalUri` APIs (which automatically forwards localhost ports) to resolve this problem. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#opening-something-in-a-local-browser-or-application) for details. As a workaround, use the **Forward a Port** command to do so manually.

​​	解决方案：扩展程序可以使用 `vscode.env.openExternal` 或 `vscode.env.asExternalUri` API（自动转发 localhost 端口）来解决此问题。有关详细信息，请参阅扩展程序作者指南。作为一种解决方法，使用“转发端口”命令手动执行此操作。

### [Webview contents do not appear Webview 内容未显示]({{< ref "/Remote/TipsandTricks#_webview-contents-do-not-appear" >}})

If the extension's webview content uses an `iframe` to connect to a local web server, the port the webview is connecting to may be blocked. In addition, if the extension hard codes `vscode-resource://` URIs instead of using `asWebviewUri`, content may not appear in the Codespaces browser editor.

​​	如果扩展程序的 webview 内容使用 `iframe` 连接到本地 Web 服务器，则 webview 连接到的端口可能会被阻止。此外，如果扩展程序硬编码 `vscode-resource://` URI 而非使用 `asWebviewUri` ，则内容可能不会显示在 Codespaces 浏览器编辑器中。

**Resolution:** The extension can use the `webview.asWebviewUri` to resolve issues with `vscode-resource://` URIs.

​​	解决方案：扩展程序可以使用 `webview.asWebviewUri` 来解决 `vscode-resource://` URI 的问题。

If ports are being blocked, the best approach is to instead use the [webview message passing](https://code.visualstudio.com/api/extension-guides/webview#scripts-and-message-passing) API. As a workaround, `vscode.env.asExternalUri` can be used allow the webview to connect to spawned localhost web servers from VS Code. However, this is currently blocked for the Codespaces browser-based editor (only) by [MicrosoftDocs/vscodespaces#11](https://github.com/MicrosoftDocs/vscodespaces/issues/11). See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#workarounds-for-using-localhost-from-a-webview) for details on the workaround.

​​	如果端口被阻止，最好的方法是改用 webview 消息传递 API。作为一种解决方法， `vscode.env.asExternalUri` 可用于允许 webview 从 VS Code 连接到生成的 localhost Web 服务器。但是，目前仅 MicrosoftDocs/vscodespaces#11 阻止了基于浏览器的 Codespaces 编辑器。有关解决方法的详细信息，请参阅扩展作者指南。

### [Blocked localhost ports 阻止的 localhost 端口]({{< ref "/Remote/TipsandTricks#_blocked-localhost-ports" >}})

If you are trying to connect to a localhost port from an external application, the port may be blocked.

​​	如果您尝试从外部应用程序连接到 localhost 端口，则该端口可能会被阻止。

**Resolution:** VS Code 1.40 introduced a new `vscode.env.asExternalUri` API for extensions to programmatically forward arbitrary ports. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#forwarding-localhost) for details. As a workaround, you can use the **Forward a Port** command to do so manually.

​​	解决方案：VS Code 1.40 为扩展引入了一个新的 `vscode.env.asExternalUri` API，用于以编程方式转发任意端口。有关详细信息，请参阅扩展作者指南。作为一种解决方法，您可以使用“转发端口”命令手动执行此操作。

### [Errors storing extension data 存储扩展数据时出错]({{< ref "/Remote/TipsandTricks#_errors-storing-extension-data" >}})

Extensions may try to persist global data by looking for the `~/.config/Code` folder on Linux. This folder may not exist, which can cause the extension to throw errors like `ENOENT: no such file or directory, open '/root/.config/Code/User/filename-goes-here`.

​​	扩展可能会尝试通过查找 Linux 上的 `~/.config/Code` 文件夹来保留全局数据。此文件夹可能不存在，这会导致扩展引发类似 `ENOENT: no such file or directory, open '/root/.config/Code/User/filename-goes-here` 的错误。

**Resolution:** Extensions can use the `context.globalStorageUri` or `context.storageUri` property to resolve this problem. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#persisting-extension-data-or-state) for details.

​​	解决方案：扩展可以使用 `context.globalStorageUri` 或 `context.storageUri` 属性来解决此问题。有关详细信息，请参阅扩展作者指南。

### [Cannot sign in / have to sign in each time I connect to a new endpoint 无法登录/每次连接到新端点时都必须登录]({{< ref "/Remote/TipsandTricks#_cannot-sign-in-have-to-sign-in-each-time-i-connect-to-a-new-endpoint" >}})

Extensions that require sign in may persist secrets using their own code. This code can fail due to missing dependencies. Even if it succeeds, the secrets will be stored remotely, which means you have to sign in for every new endpoint.

​​	需要登录的扩展程序可以使用自己的代码保留机密。此代码可能会因缺少依赖项而失败。即使成功，机密也会远程存储，这意味着您必须为每个新端点登录。

**Resolution:** Extensions can use the [SecretStorage API](https://code.visualstudio.com/api/references/vscode-api#SecretStorage) to solve this problem. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#persisting-secrets) for details.

​​	解决方案：扩展程序可以使用 SecretStorage API 来解决此问题。有关详细信息，请参阅扩展程序作者指南。

### [An incompatible extension prevents VS Code from connecting 不兼容的扩展程序阻止 VS Code 连接]({{< ref "/Remote/TipsandTricks#_an-incompatible-extension-prevents-vs-code-from-connecting" >}})

If an incompatible extension has been installed on a remote host, container, or in WSL, we have seen instances where the VS Code Server hangs or crashes due to the incompatibility. If the extension activates right away, this can prevent you from connecting and being able to uninstall the extension.

​​	如果在远程主机、容器或 WSL 中安装了不兼容的扩展程序，我们已经看到由于不兼容性，VS Code Server 挂起或崩溃的实例。如果扩展程序立即激活，这可能会阻止您连接并卸载扩展程序。

**Resolution:** Manually delete the remote extensions folder by following these steps:

​​	解决方案：按照以下步骤手动删除远程扩展程序文件夹：

1. For containers, ensure your `devcontainer.json` no longer includes a reference to the faulty extension.

   ​​	对于容器，请确保您的 `devcontainer.json` 不再包含对有故障扩展程序的引用。

2. Next, use a separate terminal / command prompt to connect to the remote host, container, or WSL.

   ​​	接下来，使用单独的终端/命令提示符连接到远程主机、容器或 WSL。

   - If SSH or WSL, connect to the environment accordingly (run `ssh` to connect to the server or open WSL terminal).
     如果是 SSH 或 WSL，请相应地连接到环境（运行 `ssh` 以连接到服务器或打开 WSL 终端）。
   - If using a container, identify the container ID by calling `docker ps -a` and looking through the list for an image with the correct name. If the container is stopped, run `docker run -it <id> /bin/sh`. If it is running, run `docker exec -it <id> /bin/sh`.
     如果使用容器，请通过调用 `docker ps -a` 并查看列表中具有正确名称的映像来标识容器 ID。如果容器已停止，请运行 `docker run -it <id> /bin/sh` 。如果正在运行，请运行 `docker exec -it <id> /bin/sh` 。

3. Once you are connected, run `rm -rf ~/.vscode-server/extensions` for VS Code stable and/or `rm -rf ~/.vscode-server-insiders/extensions` for VS Code Insiders to remove all extensions.

   ​​	连接后，运行 `rm -rf ~/.vscode-server/extensions` 以获取 VS Code 稳定版和/或 `rm -rf ~/.vscode-server-insiders/extensions` 以获取 VS Code Insiders 以删除所有扩展。

### [Extensions that ship or acquire pre-built native modules fail 预先构建的本机模块随附或获取的扩展失败]({{< ref "/Remote/TipsandTricks#_extensions-that-ship-or-acquire-prebuilt-native-modules-fail" >}})

Native modules bundled with (or dynamically acquired for) a VS Code extension must be recompiled [using Electron's `electron-rebuild`](https://electronjs.org/docs/tutorial/using-native-node-modules). However, VS Code Server runs a standard (non-Electron) version of Node.js, which can cause binaries to fail when used remotely.

​​	与 VS Code 扩展捆绑（或动态获取）的本机模块必须使用 Electron 的 `electron-rebuild` 重新编译。但是，VS Code Server 运行 Node.js 的标准（非 Electron）版本，这会导致二进制文件在远程使用时失败。

**Resolution:** Extensions need to be modified to solve this problem. They will need to include (or dynamically acquire) both sets of binaries (Electron and standard Node.js) for the "modules" version in Node.js that VS Code ships and then check to see if `context.executionContext === vscode.ExtensionExecutionContext.Remote` in their activation function to set up the correct binaries. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#using-native-node.js-modules) for details.

​​	解决方案：需要修改扩展来解决此问题。它们需要为 VS Code 预先构建的 Node.js 中的“模块”版本包含（或动态获取）两组二进制文件（Electron 和标准 Node.js），然后检查 `context.executionContext === vscode.ExtensionExecutionContext.Remote` 是否在它们的激活函数中设置正确的二进制文件。有关详细信息，请参阅扩展作者指南。

### [Extension only fails on non-x86_64 hosts or Alpine Linux 扩展仅在非 x86_64 主机或 Alpine Linux 上失败]({{< ref "/Remote/TipsandTricks#_extension-only-fails-on-nonx8664-hosts-or-alpine-linux" >}})

If an extension works on Debian 9+, Ubuntu 16.04+, or RHEL / CentOS 7+ remote SSH hosts, containers, or WSL, but fails on supported non-x86_64 hosts (for example, ARMv7l) or Alpine Linux containers, the extension may only include native code or runtimes that do not support these platforms. For example, the extensions may only include x86_64 compiled versions of native modules or runtimes. For Alpine Linux, the included native code or runtimes may not work due to [fundamental differences](https://wiki.musl-libc.org/functional-differences-from-glibc.html) between how `libc` is implemented in Alpine Linux (`musl`) and other distributions (`glibc`).

​​	如果某个扩展在 Debian 9+、Ubuntu 16.04+ 或 RHEL/CentOS 7+ 远程 SSH 主机、容器或 WSL 上运行正常，但在受支持的非 x86_64 主机（例如 ARMv7l）或 Alpine Linux 容器上运行失败，则该扩展可能只包含本机代码或不支持这些平台的运行时。例如，这些扩展可能只包含本机模块或运行时的 x86_64 编译版本。对于 Alpine Linux，包含的本机代码或运行时可能无法正常工作，因为 Alpine Linux（ `musl` ）和其他发行版（ `glibc` ）在实现 `libc` 方面存在根本差异。

**Resolution:** Extensions will need to opt-in to supporting these platforms by compiling / including binaries for these additional targets. It is important to note that some third-party npm modules may also include native code that can cause this problem. So, in some cases you may need to work with the npm module author to add additional compilation targets. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#supporting-nonx8664-hosts-or-alpine-linux-containers) for details.

​​	解决方案：扩展需要选择支持这些平台，方法是为这些其他目标编译/包含二进制文件。需要注意的是，某些第三方 npm 模块也可能包含可能导致此问题的本机代码。因此，在某些情况下，您可能需要与 npm 模块作者合作以添加其他编译目标。有关详细信息，请参阅扩展作者指南。

### [Extensions fail due to missing modules 由于缺少模块导致扩展失败]({{< ref "/Remote/TipsandTricks#_extensions-fail-due-to-missing-modules" >}})

Extensions that rely on Electron or VS Code base modules (not exposed by the extension API) without providing a fallback can fail when running remotely. You may see errors in the Developer Tools console like `original-fs` not being found.

​​	依赖于 Electron 或 VS Code 基本模块（未通过扩展 API 公开）且未提供后备的扩展在远程运行时可能会失败。您可能会在开发人员工具控制台中看到错误，例如找不到 `original-fs` 。

**Resolution:** Remove the dependency on an Electron module or provide a fallback. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions#avoid-using-electron-modules) for details.

​​	解决方案：删除对 Electron 模块的依赖项或提供后备。有关详细信息，请参阅扩展作者指南。

### [Cannot access / transfer remote workspace files to local machines 无法访问/将远程工作区文件传输到本地计算机]({{< ref "/Remote/TipsandTricks#_cannot-access-transfer-remote-workspace-files-to-local-machines" >}})

Extensions that open workspace files in external applications may encounter errors because the external application cannot directly access the remote files.

​​	在外部应用程序中打开工作区文件的扩展可能会遇到错误，因为外部应用程序无法直接访问远程文件。

**Resolution:** If you create a "UI" extension designed to run locally, you can use the `vscode.workspace.fs` API to interact with the remote workspace filesystem. You can then make this a dependency of your "Workspace" extension and invoke it using a command as needed. See the [extension author's guide](https://code.visualstudio.com/api/advanced-topics/remote-extensions) for details on different types of extensions and how to use commands to communicate between them.

​​	解决方案：如果您创建了旨在本地运行的“UI”扩展，则可以使用 `vscode.workspace.fs` API 与远程工作区文件系统进行交互。然后，您可以将其作为“工作区”扩展的依赖项，并根据需要使用命令调用它。有关不同类型的扩展以及如何使用命令在它们之间进行通信的详细信息，请参阅扩展作者指南。

### [Cannot access attached device from extension 无法从扩展访问已连接的设备]({{< ref "/Remote/TipsandTricks#_cannot-access-attached-device-from-extension" >}})

Extensions that access locally attached devices will be unable to connect to them when running remotely.

​​	访问本地连接设备的扩展在远程运行时将无法连接到这些设备。

**Resolution:** None currently. We are investigating the best approach to solve this problem.

​​	解决方案：目前没有。我们正在研究解决此问题的最佳方法。

## [Questions and feedback 问题和反馈]({{< ref "/Remote/TipsandTricks#_questions-and-feedback" >}})

### [Reporting issues 报告问题]({{< ref "/Remote/TipsandTricks#_reporting-issues" >}})

If you run into an issue with one of the remote development extensions, it's important to collect the correct logs so that we'll be able to help [diagnose your issue](https://aka.ms/vscode-remote/issues/new).

​​	如果您在使用某个远程开发扩展时遇到问题，收集正确的日志非常重要，以便我们能够帮助诊断您的问题。

Each remote extension has a command to view its logs.

​​	每个远程扩展都有一个查看其日志的命令。

You can get the Remote - SSH extension logs with **Remote-SSH: Show Log** from the Command Palette (F1). When reporting Remote - SSH issues, please also verify if you're able to SSH into your machine from an external terminal (not using Remote - SSH).

​​	您可以通过命令面板（F1）中的“Remote-SSH：显示日志”获取 Remote - SSH 扩展日志。报告 Remote - SSH 问题时，请同时验证您是否能够从外部终端（不使用 Remote - SSH）SSH 到您的计算机。

Similarly, you can get the Dev Containers extension logs with **Dev Containers: Show Container Log**.

​​	同样，您可以通过“Dev Containers：显示容器日志”获取 Dev Containers 扩展日志。

Like the two above, you can get the WSL extension logs with **WSL: Show Log**. Also check whether your issue is being tracked upstream in the [WSL repo](https://github.com/microsoft/WSL/issues) (and is not due to the WSL extension).

​​	与上述两个类似，您可以通过“WSL：显示日志”获取 WSL 扩展日志。还要检查您的问题是否在 WSL 存储库中被跟踪（并且不是由于 WSL 扩展导致的）。

If you're experiencing issues using other extensions remotely (for example, other extensions aren't loading or installing properly in a remote context), it's helpful to grab the log from the **Remote Extension Host** output channel (**Output: Focus on Output View**), and select **Log (Remote Extension Host)** from the dropdown.

​​	如果您在远程使用其他扩展时遇到问题（例如，其他扩展在远程上下文中无法正确加载或安装），则从“远程扩展主机”输出通道（输出：关注输出视图）中获取日志并从下拉列表中选择“日志（远程扩展主机）”会有所帮助。

> **Note**: If you only see **Log (Extension Host)**, this is the local extension host, and the remote extension host didn't launch. This is because the log channel is created only after the log file is created, so if the remote extension host does not launch, the remote extension host log file was not created and is not shown in the Output view. This is still helpful information to include in your issue.
>
> ​​	注意：如果您只看到日志（扩展主机），则这是本地扩展主机，并且远程扩展主机未启动。这是因为日志通道仅在创建日志文件后才创建，因此，如果远程扩展主机未启动，则不会创建远程扩展主机日志文件，并且不会在输出视图中显示。这仍然是包含在您的问题中的有用信息。

### [Remote question and feedback resources 远程问题和反馈资源]({{< ref "/Remote/TipsandTricks#_remote-question-and-feedback-resources" >}})

We have a variety of other remote resources:

​​	我们还有各种其他远程资源：

- See [Remote Development FAQ]({{< ref "/Remote/FAQ" >}}).
  请参阅远程开发常见问题解答。
- Search on [Stack Overflow](https://stackoverflow.com/questions/tagged/vscode-remote).
  在 Stack Overflow 上搜索。
- Add a [feature request](https://aka.ms/vscode-remote/feature-requests) or [report a problem](https://aka.ms/vscode-remote/issues/new).
  添加功能请求或报告问题。
