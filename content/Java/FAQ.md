+++
title = "FAQ"
date = 2024-01-12T22:36:24+08:00
weight = 130
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/java/java-faq](https://code.visualstudio.com/docs/java/java-faq)

# Frequent Asked Questions 常见问题



Thanks for your interest in Java on Visual Studio Code! This FAQ will hopefully answer some of the questions you may have.

​​​	感谢您对 Visual Studio Code 上的 Java 感兴趣！此常见问题解答有望解答您可能遇到的部分问题。

## [Are these Java extensions open source? 这些 Java 扩展是开源的吗？]({{< ref "/Java/FAQ#_are-these-java-extensions-open-source" >}})

Yes. All the [Java Extensions]({{< ref "/Java/Extensions" >}}) provided by Red Hat, Microsoft, and VMware are open source, as well as most extensions supported by the community. You can find their corresponding repositories on GitHub from the Marketplace pages.

​​​	是。Red Hat、Microsoft 和 VMware 提供的所有 Java 扩展都是开源的，社区支持的大多数扩展也是如此。您可以在 GitHub 上的 Marketplace 页面中找到它们相应的存储库。

## [Are there any other features coming to Java on Visual Studio Code? Visual Studio Code 上的 Java 是否还有其他功能？]({{< ref "/Java/FAQ#_are-there-any-other-features-coming-to-java-on-visual-studio-code" >}})

Definitely. We use GitHub issues to track incoming requests and planned work for each of our extensions. Currently we're working on adding more refactoring and linting features to enhance the editing productivity, as well as some performance improvements to make it even faster.

​​​	当然。我们使用 GitHub 问题来跟踪传入的请求和我们每个扩展的计划工作。我们目前正致力于添加更多重构和 linting 功能以提高编辑效率，以及一些性能改进以使其更快。

Most of our work is collected from and prioritized by customer feedback. If you're interested in providing your thoughts, you can go directly to our project repositories to submit a new issue to share your thoughts.

​​​	我们的大部分工作都是从客户反馈中收集并按优先级排列的。如果您有兴趣提供您的想法，您可以直接转到我们的项目存储库提交新问题以分享您的想法。

We do have limited capacity within the team and we'd really like to encourage more contributions from the great Java community. If you're passionate about your idea and would like to help fellow Java developers, you're welcome to join us! Some areas worth considering including Gradle support, code analysis and test coverage tools, profiler, and additional framework support including DropWizard, JavaFX, JPA, Play, Akka, OSGi.

​​​	团队内我们的能力有限，我们非常希望鼓励更多来自 Java 社区的贡献。如果您对自己的想法充满热情，并希望帮助其他 Java 开发人员，欢迎您加入我们！一些值得考虑的领域包括 Gradle 支持、代码分析和测试覆盖率工具、分析器以及其他框架支持，包括 DropWizard、JavaFX、JPA、Play、Akka、OSGi。

## [Can I use keyboard shortcuts from other IDE? 我可以使用其他 IDE 的键盘快捷键吗？]({{< ref "/Java/FAQ#_can-i-use-keyboard-shortcuts-from-other-ide" >}})

Sure. [Keymap extensions]({{< ref "/GetStarted/KeyBindings#_keymap-extensions" >}}) in VS Code modify the VS Code shortcuts to match those of other editors. You can find [IntelliJ IDEA Keybindings](https://marketplace.visualstudio.com/items?itemName=k--kato.intellij-idea-keybindings), [Eclipse Keymap](https://marketplace.visualstudio.com/items?itemName=alphabotsec.vscode-eclipse-keybindings) as well as keymaps for other popular editors in [Keymaps category](https://marketplace.visualstudio.com/search?target=VSCode&category=Keymaps&sortBy=Installs) of extensions in the Marketplace.

​​​	当然可以。VS Code 中的按键映射扩展修改了 VS Code 快捷键，使其与其他编辑器的快捷键相匹配。您可以在 Marketplace 的扩展类别中找到 IntelliJ IDEA 键绑定、Eclipse 键映射以及其他流行编辑器的键映射。

## [Where can I find the latest progress of Java support on Visual Studio Code? 我可以在哪里找到 Visual Studio Code 上 Java 支持的最新进展？]({{< ref "/Java/FAQ#_where-can-i-find-the-latest-progress-of-java-support-on-visual-studio-code" >}})

You can follow us on the [Java at Microsoft](https://devblogs.microsoft.com/java/) blog, which will keep you updated on our progress.

​​​	您可以在 Microsoft 博客上的 Java 中关注我们，这将使您了解我们的进展情况。

While you're using Java within VS Code, you may also see a **Release Notes** section after you update the [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack). The notes will give you an overview on the notable updates included in the extensions.

​​​	在 VS Code 中使用 Java 时，您还可能会在更新 Java 扩展包后看到发行说明部分。这些说明将概述扩展中包含的值得注意的更新。

## [How can I use Visual Studio Code with new Java versions? 我如何将 Visual Studio Code 与新版 Java 一起使用？]({{< ref "/Java/FAQ#_how-can-i-use-visual-studio-code-with-new-java-versions" >}})

Thanks to the upstream update from JDT, you can now build your project up to Java 14 with VS Code as well. To use the experimental/preview language features, you need to modify your project settings.

​​​	借助 JDT 的上游更新，您现在也可以使用 VS Code 将项目构建到 Java 14。若要使用实验性/预览语言功能，您需要修改项目设置。

Maven - modify `pom.xml`:

​​​	Maven - 修改 `pom.xml` ：

```
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <configuration>
            <release>14</release>
            <compilerArgs>--enable-preview</compilerArgs>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
```

Gradle:

​​​	Gradle：

```
sourceCompatibility = 14
tasks.withType(JavaCompile) {
    options.compilerArgs += '--enable-preview'
}
tasks.withType(Test) {
    jvmArgs += "--enable-preview"
}
```

> Note: If you are modifying a project that was already opened in VS Code, you may need to force clean the workspace and reload. To do so, run command **Java: Clean Java Language Server Workspace**.
>
> ​​​	注意：如果您正在修改已在 VS Code 中打开的项目，您可能需要强制清除工作区并重新加载。为此，请运行命令 Java：清除 Java 语言服务器工作区。

## [How can I use it behind a corporate proxy? 如何在公司代理后面使用它？]({{< ref "/Java/FAQ#_how-can-i-use-it-behind-a-corporate-proxy" >}})

When using the Java Language Support (redhat.java) extension behind a corporate proxy, you might need to let the Java Language server know how to connect to the Internet, in order to download build runtimes, Java dependencies, and their sources through that proxy.

​​​	在公司代理后面使用 Java 语言支持 (redhat.java) 扩展时，您可能需要让 Java 语言服务器知道如何连接到 Internet，以便通过该代理下载构建运行时、Java 依赖项及其源。

This is done by configuring the `java.jdt.ls.vmargs` setting in VS Code preferences (all on one line):

​​​	这可以通过在 VS Code 首选项中配置 `java.jdt.ls.vmargs` 设置来完成（一行）：

```
{
  "java.jdt.ls.vmargs": "-Dhttp.proxyHost=webproxy.corp.net -Dhttp.proxyPort=proxyport -Dhttp.proxyUser=user -Dhttp.proxyPassword=password -Dhttps.proxyHost=webproxy.corp.net -Dhttps.proxyPort=proxyport -Dhttps.proxyUser=user -Dhttps.proxyPassword=password"
}
```

## [Will this be available for Visual Studio? 这是否适用于 Visual Studio？]({{< ref "/Java/FAQ#_will-this-be-available-for-visual-studio" >}})

Currently we don't plan to extend the Java support to Visual Studio. There are already great IDEs for Java and we're focusing on VS Code to provide a lightweight experience in a polyglot editor.

​​​	目前我们不打算将 Java 支持扩展到 Visual Studio。已经有很多适用于 Java 的优秀 IDE，我们专注于 VS Code，以便在多语言编辑器中提供轻量级体验。

## [Does VS Code Java support other display languages? VS Code Java 是否支持其他显示语言？]({{< ref "/Java/FAQ#_does-vs-code-java-support-other-display-languages" >}})

Currently we support Chinese in addition to English for a few extensions including [Debugger for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug), [Test Runner for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-test), [Maven for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven), [Project Manager for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency). To learn how to switch the VS Code display language, see [Display Languages]({{< ref "/GetStarted/DisplayLanguage" >}}).

​​​	目前，除了英语之外，我们还为一些扩展提供中文支持，包括 Java 调试器、Java 测试运行器、Java 的 Maven、Java 项目管理器。若要了解如何切换 VS Code 显示语言，请参阅显示语言。

You can contribute to the extension repositories if you're interested in additional display language support.

​​​	如果您有兴趣获得其他显示语言支持，可以为扩展存储库做出贡献。

## [How to troubleshoot and contribute to the Java Language Server 如何对 Java 语言服务器进行故障排除和贡献]({{< ref "/Java/FAQ#_how-to-troubleshoot-and-contribute-to-the-java-language-server" >}})

You can visit the [Java for Visual Studio Code wiki](https://github.com/redhat-developer/vscode-java/wiki) to find answers regarding:

​​​	您可以访问适用于 Visual Studio Code 的 Java Wiki，以查找有关以下内容的解答：

1. ["Classpath is incomplete" warning
   “类路径不完整”警告](https://github.com/redhat-developer/vscode-java/wiki/"Classpath-is-incomplete"-warning)
2. [Annotation Processing support for Maven projects
   Maven 项目的注释处理支持](https://github.com/redhat-developer/vscode-java/wiki/Annotation-Processing-support-for-Maven-projects)
3. [Contribute a Java extension
   贡献 Java 扩展](https://github.com/redhat-developer/vscode-java/wiki/Contribute-a-Java-Extension)
4. [Formatter settings
   格式化程序设置](https://github.com/redhat-developer/vscode-java/wiki/Formatter-settings)
5. [Lombok Support
   Lombok 支持](https://github.com/redhat-developer/vscode-java/wiki/Lombok-support)
6. [Using a Proxy
   使用代理](https://github.com/redhat-developer/vscode-java/wiki/Using-a-Proxy)
7. [Troubleshooting
   故障排除](https://github.com/redhat-developer/vscode-java/wiki/Troubleshooting)
