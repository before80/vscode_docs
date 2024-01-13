+++
title = "Spring Boot"
date = 2024-01-12T22:36:24+08:00
weight = 80
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/java/java-spring-boot](https://code.visualstudio.com/docs/java/java-spring-boot)

# Spring Boot in Visual Studio Code Visual Studio Code 中的 Spring Boot



Visual Studio Code is an ideal lightweight development environment for Spring Boot application developers and there are several useful VS Code extensions including:

​​​	Visual Studio Code 是 Spring Boot 应用程序开发人员的理想轻量级开发环境，其中包括几个有用的 VS Code 扩展，包括：

- [Spring Boot Tools](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-spring-boot)
- [Spring Initializr](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr)
- [Spring Boot Dashboard](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard)

We recommend installing the [Spring Boot Extension Pack](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-boot-dev-pack) that includes all of the extensions above.

​​​	我们建议安装包含上述所有扩展的 Spring Boot Extension Pack。

If you run into any issues when using the features below, you can contact us by [opening an issue](https://github.com/microsoft/vscode-java-pack/issues).

​​​	如果您在使用以下功能时遇到任何问题，可以通过打开问题与我们联系。

## [Prerequisites 先决条件](https://code.visualstudio.com/docs/java/java-spring-boot#_prerequisites)

To develop a Spring Boot application in Visual Studio Code, you need to install the following:

​​​	要在 Visual Studio Code 中开发 Spring Boot 应用程序，您需要安装以下内容：

- [Java Development Kit (JDK)](https://www.microsoft.com/openjdk)
- [Extension Pack for Java
  适用于 Java 的扩展包](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
- [Spring Boot Extension Pack](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-boot-dev-pack)

[Install the Extension Pack for Java
安装 Java 扩展包](vscode:extension/vscjava.vscode-java-pack)

[Install the Spring Boot Extension Pack
安装 Spring Boot Extension Pack](vscode:extension/vmware.vscode-boot-dev-pack)

> **Note**: More information about how to get started can be found at [Getting Started with Java](https://code.visualstudio.com/docs/java/java-tutorial) tutorial.
>
> ​​​	注意：有关如何入门的信息，请参阅 Java 教程中的入门。

To help get you started with Java Spring Boot development, you can use the [Java Spring profile template](https://code.visualstudio.com/docs/editor/profiles#_java-spring-profile-template) that includes useful extensions, settings, and Java Spring Boot code snippets.

​​​	为了帮助您开始 Java Spring Boot 开发，您可以使用包含有用的扩展、设置和 Java Spring Boot 代码段的 Java Spring 配置文件模板。

## [Create the project 创建项目](https://code.visualstudio.com/docs/java/java-spring-boot#_create-the-project)

The [Spring Initializr](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr) extension allows you to search for dependencies and generate new Spring Boot projects.

​​​	Spring Initializr 扩展允许您搜索依赖项并生成新的 Spring Boot 项目。

To install, launch VS Code and from the Extensions view (Ctrl+Shift+X), search for `vscode-spring-initializr`.

​​​	要安装，请启动 VS Code，然后从扩展视图 (Ctrl+Shift+X) 中搜索 `vscode-spring-initializr` 。

Once you have the extension installed, open the **Command Palette** (Ctrl+Shift+P) and type `Spring Initializr` to start generating a Maven or Gradle project and then follow the wizard.

​​​	安装扩展后，打开命令面板 (Ctrl+Shift+P) 并键入 `Spring Initializr` 以开始生成 Maven 或 Gradle 项目，然后按照向导进行操作。

<video autoplay="" loop="" muted="" playsinline="" controls="" video="Create the project" data-immersive-translate-walked="315d21c0-2644-41d0-9760-e56a69eae041" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; display: inline-block; vertical-align: baseline; margin-top: 1.5rem; margin-bottom: 2.5rem; width: 616.662px; max-width: 100%; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></video>



## [Edit the project 编辑项目](https://code.visualstudio.com/docs/java/java-spring-boot#_edit-the-project)

The [Spring Initializr](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr) extension allows you to add dependencies after generating a new Spring Boot project.

​​​	Spring Initializr 扩展允许您在生成新的 Spring Boot 项目后添加依赖项。

Navigate to your `pom.xml` file and right-click to select **Add starters...**. A dropdown will show the dependencies you already have beginning with a `√` . You can search for other dependencies you want to add to your project. Or you can click on the existing dependencies to remove them.

​​​	导航到您的 `pom.xml` 文件，然后右键单击以选择添加启动器.... 下拉菜单将显示您已经拥有的依赖项，以 `√` 开头。您可以搜索要添加到项目中的其他依赖项。或者，您可以单击现有依赖项以将其删除。

<video autoplay="" loop="" muted="" playsinline="" controls="" title="Edit the project" data-immersive-translate-walked="315d21c0-2644-41d0-9760-e56a69eae041" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; display: inline-block; vertical-align: baseline; margin-top: 1.5rem; margin-bottom: 2.5rem; width: 616.662px; max-width: 100%; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></video>



## [Develop the application 开发应用程序](https://code.visualstudio.com/docs/java/java-spring-boot#_develop-the-application)

The [Spring Boot Tools](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-spring-boot) extension includes rich language support for working with Spring Boot `application.properties`, `application.yml`, and `.java` files.

​​​	Spring Boot Tools 扩展包括丰富的语言支持，可用于处理 Spring Boot `application.properties` 、 `application.yml` 和 `.java` 文件。

The extension supports the following features:

​​​	该扩展支持以下功能：

- Quickly navigate to a Spring element in your workspace
  快速导航到工作区中的 Spring 元素
- Smart code completion for Spring specific components
  针对特定于 Spring 的组件的智能代码补全
- Quick access to running Spring apps
  快速访问正在运行的 Spring 应用
- Live application information
  实时应用程序信息
- Code templates
  代码模板

Similar code completion and validation features are also available for `.properties` and `.yml` files.

​​​	类似的代码补全和验证功能也适用于 `.properties` 和 `.yml` 文件。

To learn how to use these features, you can visit this [detailed usage guide](https://github.com/spring-projects/sts4/tree/main/vscode-extensions/vscode-spring-boot#usage).

​​​	要了解如何使用这些功能，可以访问此详细使用指南。

Below is an example showing live application information.

​​​	下面是一个显示实时应用程序信息的示例。

<video autoplay="" loop="" muted="" playsinline="" controls="" title="Live application information and metrics" data-immersive-translate-walked="315d21c0-2644-41d0-9760-e56a69eae041" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; display: inline-block; vertical-align: baseline; margin-top: 1.5rem; margin-bottom: 2.5rem; width: 616.662px; max-width: 100%; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></video>



## [Run the application 运行应用程序](https://code.visualstudio.com/docs/java/java-spring-boot#_run-the-application)

In addition to using F5 to run your application, there's the [Spring Boot Dashboard](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard) extension, which lets you view and manage all available Spring Boot projects in your workspace as well as quickly start, stop, or debug your project.

​​​	除了使用 F5 运行应用程序外，还有 Spring Boot Dashboard 扩展，它允许您查看和管理工作区中的所有可用 Spring Boot 项目，以及快速启动、停止或调试项目。

<video autoplay="" loop="" muted="" playsinline="" controls="" title="Run the Spring Boot application from Spring Boot dashboard" data-immersive-translate-walked="315d21c0-2644-41d0-9760-e56a69eae041" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; display: inline-block; vertical-align: baseline; margin-top: 1.5rem; margin-bottom: 2.5rem; width: 616.662px; max-width: 100%; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></video>



## [Next steps 后续步骤](https://code.visualstudio.com/docs/java/java-spring-boot#_next-steps)

- [Java Spring profile template](https://code.visualstudio.com/docs/editor/profiles#_java-spring-profile-template) - Create a new [profile](https://code.visualstudio.com/docs/editor/profiles) with a curated set of extensions, settings, and snippets.
  Java Spring 配置文件模板 - 使用精选的扩展、设置和代码段创建新配置文件。
- To deploy your web app, see [Java Web Apps with VS Code](https://code.visualstudio.com/docs/java/java-webapp).
  要部署 Web 应用，请参阅使用 VS Code 的 Java Web 应用。
- To containerize a web app and deploy as a Docker container, check out [Docker in VS Code](https://code.visualstudio.com/docs/containers/overview).
  要将 Web 应用容器化并作为 Docker 容器部署，请查看 VS Code 中的 Docker。
- To learn more about Java debugging features, see [Running and debugging Java](https://code.visualstudio.com/docs/java/java-debugging).
  要详细了解 Java 调试功能，请参阅运行和调试 Java。
