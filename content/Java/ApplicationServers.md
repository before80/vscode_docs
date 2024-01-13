+++
title = "Application Servers"
date = 2024-01-12T22:36:24+08:00
weight = 90
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/java/java-tomcat-jetty](https://code.visualstudio.com/docs/java/java-tomcat-jetty)

# Working with Application Servers in VS Code 在 VS Code 中使用应用程序服务器



Visual Studio Code is a code editor-centric development tool, so it doesn't come with any embedded application server. For most servers, you will need to deploy them using the command line, and then use the appropriate debugger [configuration](https://code.visualstudio.com/docs/java/java-debugging#_configure) if you want to attach to it.

​​​	Visual Studio Code 是一款以代码编辑器为中心的开发工具，因此它不附带任何嵌入式应用程序服务器。对于大多数服务器，您需要使用命令行部署它们，然后使用适当的调试器配置（如果您想附加到它）。

On the other hand, we know that for certain Java workloads, server integration is very useful. With Visual Studio Code, you can find third party extensions for popular application servers, for example [Tomcat](https://tomcat.apache.org/), [Jetty](https://www.eclipse.org/jetty/), and [Open Liberty](https://openliberty.io/), which are helpful when working with those servers locally.

​​​	另一方面，我们知道对于某些 Java 工作负载，服务器集成非常有用。使用 Visual Studio Code，您可以找到流行应用程序服务器的第三方扩展，例如 Tomcat、Jetty 和 Open Liberty，在本地使用这些服务器时很有用。

For [Spring Boot Dashboard](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard), see [Spring Boot in Visual Studio Code](https://code.visualstudio.com/docs/java/java-spring-boot).

​​​	有关 Spring Boot Dashboard，请参阅 Visual Studio Code 中的 Spring Boot。

If you run into any issues when using the features below, you can contact us by entering an [issue](https://github.com/microsoft/vscode-java-pack/issues).

​​​	如果您在使用以下功能时遇到任何问题，可以通过输入问题与我们联系。

## [Community Server Connectors 社区服务器连接器](https://code.visualstudio.com/docs/java/java-tomcat-jetty#_community-server-connectors)

The [Community Server Connectors](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-community-server-connector) extension is published by Red Hat. It provides a Remote Server Protocol-based server connector, which can start, stop, publish to, and otherwise control community runtimes and servers like [Apache Felix](https://felix.apache.org/documentation/index.html), [Karaf](https://karaf.apache.org/), and [Tomcat](https://tomcat.apache.org/).

​​​	社区服务器连接器扩展由 Red Hat 发布。它提供了一个基于远程服务器协议的服务器连接器，该连接器可以启动、停止、发布到社区运行时和服务器（如 Apache Felix、Karaf 和 Tomcat），并以其他方式控制它们。

<video autoplay="" loop="" muted="" playsinline="" controls="" title="Community server connectors" data-immersive-translate-walked="d53be152-cfa7-4668-a286-4b93ad8ff5e7" style="box-sizing: border-box; font-family: &quot;Segoe UI&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; display: inline-block; vertical-align: baseline; margin-top: 1.5rem; margin-bottom: 2.5rem; width: 616.662px; max-width: 100%; color: rgb(36, 36, 36); font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: normal; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></video>



## [Other Servers 其他服务器](https://code.visualstudio.com/docs/java/java-tomcat-jetty#_other-servers)

The [Open Liberty Tools](https://marketplace.visualstudio.com/items?itemName=Open-Liberty.liberty-dev-vscode-ext) extension lets you run your application on Open Liberty, allowing you to deploy, test, and debug your application from Visual Studio Code.

​​​	Open Liberty Tools 扩展允许您在 Open Liberty 上运行应用程序，从而允许您从 Visual Studio Code 部署、测试和调试应用程序。

The [Server Connector](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-server-connector) extension by Red Hat allows you to start, stop, and deploy to a Red Hat server and runtime products like WildFly, JBoss EAP, Minishift, CDK.

​​​	Red Hat 的服务器连接器扩展程序允许您启动、停止和部署到 Red Hat 服务器和运行时产品，如 WildFly、JBoss EAP、Minishift、CDK。

[Extension Pack for MicroProfile](https://marketplace.visualstudio.com/items?itemName=MicroProfile-Community.vscode-microprofile-pack) provides tools for creating MicroProfile projects to develop and deploy to runtimes such as Open Liberty, Quarkus, and Payara.

​​​	MicroProfile 扩展包提供用于创建 MicroProfile 项目的工具，以开发和部署到 Open Liberty、Quarkus 和 Payara 等运行时。
