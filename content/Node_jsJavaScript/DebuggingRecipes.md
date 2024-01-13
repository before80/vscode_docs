+++
title = "Debugging Recipes"
date = 2024-01-12T22:36:24+08:00
weight = 80
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/nodejs/debugging-recipes](https://code.visualstudio.com/docs/nodejs/debugging-recipes)

# JavaScript Debugging Recipes JavaScript 调试秘籍



Visual Studio Code supports debugging of many languages and platforms via debuggers that are either built-in or contributed by extensions.

​​	Visual Studio Code 支持通过内置或扩展提供的调试器来调试多种语言和平台。

To make it easier to get started with debugging, we have made a collection of debugging "recipes" which contain the steps and configuration you need to set up debugging for your favorite platform. The recipes are in GitHub at https://github.com/microsoft/vscode-recipes.

​​	为了让您更轻松地开始调试，我们整理了一系列调试“配方”，其中包含为您的常用平台设置调试所需的步骤和配置。 这些配方位于 GitHub 中，网址为 https://github.com/microsoft/vscode-recipes。

## [Debug server-side JavaScript in Node.js 在 Node.js 中调试服务器端 JavaScript](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_debug-serverside-javascript-in-nodejs)

The Visual Studio Code editor supports debugging Node.js applications via the built-in [Node.js](https://nodejs.org/) debugger.

​​	Visual Studio Code 编辑器支持通过内置 Node.js 调试器来调试 Node.js 应用程序。

![Node.js logo](./DebuggingRecipes_img/nodejs.png)

**Recipes:
配方：**

- [Debugging Node.js with Nodemon
  使用 Nodemon 调试 Node.js](https://github.com/microsoft/vscode-recipes/tree/main/nodemon)
- [Debugging Node.js AWS Lambda functions
  调试 Node.js AWS Lambda 函数](https://github.com/microsoft/vscode-recipes/tree/main/debugging-lambda-functions)

## [Debug client-side JavaScript in Browsers 在浏览器中调试客户端 JavaScript](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_debug-clientside-javascript-in-browsers)

The Visual Studio Code editor supports debugging of JavaScript running in [Microsoft Edge](https://www.microsoft.com/edge) and [Google Chrome](https://www.google.com/chrome/).

​​	Visual Studio Code 编辑器支持调试在 Microsoft Edge 和 Google Chrome 中运行的 JavaScript。

![JavaScript, Edge, and Chrome logo](./DebuggingRecipes_img/browsers.png)

You can read more about debugging browsers works in the [Browser Debugging documentation](https://code.visualstudio.com/docs/nodejs/browser-debugging).

​​	您可以在浏览器调试文档中阅读有关调试浏览器工作原理的更多信息。

**Recipes:
食谱：**

- [Debugging Angular apps with Angular CLI
  使用 Angular CLI 调试 Angular 应用](https://github.com/microsoft/vscode-recipes/tree/main/Angular-CLI)
- [Debugging Next.js apps
  调试 Next.js 应用](https://github.com/microsoft/vscode-recipes/tree/main/Next-js)
- [Debugging Meteor apps
  调试 Meteor 应用](https://github.com/microsoft/vscode-recipes/tree/main/meteor)
- [Debugging Vue.js apps
  调试 Vue.js 应用](https://github.com/microsoft/vscode-recipes/tree/main/vuejs-cli)
- [Debugging Mocha tests
  调试 Mocha 测试](https://github.com/microsoft/vscode-recipes/tree/main/debugging-mocha-tests)
- [Debugging Jest tests
  调试 Jest 测试](https://github.com/microsoft/vscode-recipes/tree/main/debugging-jest-tests)

**Blog posts**:

​​	博客文章：

- [Live edit and debug your React apps directly from VS Code
  直接从 VS Code 实时编辑和调试 React 应用](https://medium.com/@auchenberg/live-edit-and-debug-your-react-apps-directly-from-vs-code-without-leaving-the-editor-3da489ed905f)
- [Super-charged live editing and JavaScript debugging for Angular using VS Code
  使用 VS Code 对 Angular 进行超级实时编辑和 JavaScript 调试](https://medium.com/@auchenberg/super-charged-live-editing-and-javascript-debugging-for-angular-using-visual-studio-code-c29da251ec71)

## [Electron - Debug Electron applications Electron - 调试 Electron 应用程序](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_electron-debug-electron-applications)

The Visual Studio Code editor supports debugging [Electron](https://www.electronjs.org/) applications via the built-in JavaScript debugger.

​​	Visual Studio Code 编辑器支持通过内置 JavaScript 调试器调试 Electron 应用程序。

![electron logo](./DebuggingRecipes_img/electron.png)

**Recipes:
配方：**

- [Debugging Electron Main and Renderer processes
  调试 Electron 主进程和渲染器进程](https://github.com/microsoft/vscode-recipes/tree/main/Electron)

## [Next steps 后续步骤](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_next-steps)

- [Debugging](https://code.visualstudio.com/docs/editor/debugging) - Read about general VS Code debugging features.
  调试 - 阅读有关常规 VS Code 调试功能的信息。
- [Node.js Debugging](https://code.visualstudio.com/docs/nodejs/nodejs-debugging) - Learn about the built-in Node.js debugger.
  Node.js 调试 - 了解内置的 Node.js 调试器。
- [Video: Getting started with Node.js debugging](https://www.youtube.com/watch?v=2oFKNL7vYV8) - Attach to a running Node.js process.
  视频：开始使用 Node.js 调试 - 附加到正在运行的 Node.js 进程。
