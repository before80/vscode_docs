+++
title = "Enterprise"
date = 2024-01-12T22:36:24+08:00
weight = 70
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/setup/enterprise](https://code.visualstudio.com/docs/setup/enterprise)

# Enterprise Support 企业支持



Visual Studio Code can be used as a development tool for enterprise teams of all sizes. As an IT admin, you can configure VS Code to achieve consistency and compatibility across your organization.

​​​	Visual Studio Code 可用作各种规模的企业团队的开发工具。作为 IT 管理员，您可以配置 VS Code 以在整个组织中实现一致性和兼容性。

## [Network: Common hostnames 网络：常见主机名](https://code.visualstudio.com/docs/setup/enterprise#_network-common-hostnames)

A handful of features within VS Code require network communication to work, such as the auto-update mechanism, querying and installing extensions, and telemetry. For these features to work properly in a proxy environment, you must have the product correctly configured.

​​​	VS Code 中的一些功能需要网络通信才能工作，例如自动更新机制、查询和安装扩展以及遥测。为了让这些功能在代理环境中正常工作，您必须正确配置产品。

Refer to the [network common hostnames list](https://code.visualstudio.com/docs/setup/network#_common-hostnames) for the required domains.

​​​	请参阅网络常见主机名列表以了解所需域。

## [Group Policy on Windows Windows 上的组策略](https://code.visualstudio.com/docs/setup/enterprise#_group-policy-on-windows)

System administrators need a way to control default software settings across all client machines in their organization. Group Policy is a client solution that gives administrators flexibility to implement the behavior for each of the available policies and settings.

​​​	系统管理员需要一种方法来控制其组织中所有客户端计算机上的默认软件设置。组策略是一种客户端解决方案，它为管理员提供了灵活性，可以针对每个可用策略和设置实施行为。

VS Code now has support for [Windows Registry-based Group Policy](https://learn.microsoft.com/previous-versions/windows/desktop/policy/implementing-registry-based-policy). Starting from VS Code version 1.69, each release will ship with a `policies` directory containing ADMX template files that can be added to the following path: `C:\Windows\PolicyDefinitions`.

​​​	VS Code 现在支持基于 Windows 注册表的组策略。从 VS Code 版本 1.69 开始，每个版本都将附带一个 `policies` 目录，其中包含可添加到以下路径的 ADMX 模板文件： `C:\Windows\PolicyDefinitions` 。

Once the policy definitions are installed, admins can use the [Local Group Policy Editor](https://learn.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265982(v=ws.11)) to manage the policy values.

​​​	安装策略定义后，管理员可以使用本地组策略编辑器来管理策略值。

Policies can be set both at the Computer level and the User level. If both are set, Computer level will take precedence. When a policy value is set, the value overrides the VS Code [setting](https://code.visualstudio.com/docs/getstarted/settings) value configured at any level (default, user, workspace, etc.).

​​​	策略可以在计算机级别和用户级别设置。如果都设置了，则计算机级别将优先。设置策略值时，该值将覆盖在任何级别（默认、用户、工作区等）配置的 VS Code 设置值。

## [Additional Policies 其他策略](https://code.visualstudio.com/docs/setup/enterprise#_additional-policies)

The goal is to promote current VS Code settings as Policies and closely follow existing settings, so that the naming and behavior are consistent. If there are requests to enact more policies, please open an issue in the VS Code [GitHub repository](https://github.com/microsoft/vscode). The team will determine if there is already a corresponding setting for the behavior or if a new setting should be created to control the desired behavior.

​​​	目标是将当前 VS Code 设置作为策略进行推广，并紧密遵循现有设置，以便命名和行为保持一致。如果有请求制定更多策略，请在 VS Code GitHub 存储库中打开一个问题。团队将确定行为是否已有相应的设置，或者是否应该创建新的设置来控制所需的行为。
