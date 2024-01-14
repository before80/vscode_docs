+++
title = "Formatting"
date = 2024-01-12T22:36:24+08:00
weight = 30
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/python/formatting](https://code.visualstudio.com/docs/python/formatting)

# Formatting Python in VS Code 在 VS Code 中设置 Python 格式



Formatting makes source code easier to read by human beings. By enforcing particular rules and conventions such as line spacing, indents, and spacing around operators, the code becomes more visually organized and comprehensible. You can view an example on the [autopep8](https://pypi.org/project/autopep8/) page. Keep in mind, formatting doesn't affect the functionality of the code itself.

​​​	格式化使源代码更易于人类阅读。通过强制执行特定规则和约定（例如行距、缩进和运算符周围的间距），代码在视觉上变得更有条理和易于理解。您可以在 autopep8 页面上查看示例。请记住，格式化不会影响代码本身的功能。

[Linting]({{< ref "/Python/Linting" >}}) helps to prevent errors by analyzing code for common syntactical, stylistic, and functional errors and unconventional programming practices. Although there is a little overlap between formatting and linting, the two capabilities are complementary.

​​​	通过分析代码中的常见语法、风格和功能错误以及非常规编程实践，Linting 有助于防止错误。尽管格式化和 linting 之间存在一些重叠，但这两个功能是互补的。

## [Choose a formatter 选择格式化程序]({{< ref "/Python/Formatting#_choose-a-formatter" >}})

Install the formatting tool of your choice from the VS Code [Marketplace](https://marketplace.visualstudio.com/vscode).

​​​	从 VS Code Marketplace 安装您选择的格式化工具。

Microsoft publishes the following formatting extensions:

​​​	Microsoft 发布以下格式化扩展：

| Formatter 格式化程序             | Extension 扩展                                               |
| :------------------------------- | :----------------------------------------------------------- |
| autopep8                         | https://marketplace.visualstudio.com/items?itemName=ms-python.autopep8 |
| Black formatter Black 格式化程序 | https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter |

Formatter extensions offered by the community:

​​​	社区提供的格式化程序扩展：

| Formatter 格式化程序 | Extension 扩展                                               |
| :------------------- | :----------------------------------------------------------- |
| Ruff                 | https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff |
| yapf                 | https://marketplace.visualstudio.com/items?itemName=eeyore.yapf |

Furthermore, below are formatter extensions that support import sorting:

​​​	此外，以下是支持导入排序的格式化程序扩展：

| Formatter 格式化程序 | Extension 扩展                                               |
| :------------------- | :----------------------------------------------------------- |
| Ruff                 | https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff |
| isort                | https://marketplace.visualstudio.com/items?itemName=ms-python.isort |

> **Note**: If you don't find your preferred formatter in the table above or in the Marketplace, you can add support for it via an extension. You can use the [Python Extension Template](https://code.visualstudio.com/api/advanced-topics/python-extension-template) to integrate new Python tools into VS Code.
>
> ​​​	注意：如果您在上面的表格或市场中找不到您喜欢的格式化程序，您可以通过扩展来添加对它的支持。您可以使用 Python 扩展模板将新的 Python 工具集成到 VS Code 中。

## [Set a default formatter 设置默认格式化程序]({{< ref "/Python/Formatting#_set-a-default-formatter" >}})

Once you install a formatter extension, you can select it as the default formatter for Python files in VS Code by following the steps below:

​​​	安装格式化程序扩展后，您可以按照以下步骤将其选为 VS Code 中 Python 文件的默认格式化程序：

1. Open a Python file in VS Code.
   在 VS Code 中打开一个 Python 文件。
2. Right-click on the editor to display the context menu.
   右键单击编辑器以显示上下文菜单。
3. Select **Format Document With...**.
   选择“使用...格式化文档”。
4. Select **Configure Default Formatter...** from the drop-down menu.
   从下拉菜单中选择“配置默认格式化程序...”。
5. Select your preferred formatter extension from the list.
   从列表中选择您喜欢的格式化程序扩展。

Alternatively, you can set it as the default formatter for all Python files by setting `"editor.defaultFormatter"` in your User `settings.json` file, under a `[python]` scope. You can open `settings.json` with the **Preferences: Open User Settings (JSON)** command.

​​​	或者，您也可以通过在 `"editor.defaultFormatter"` 文件中，在 `[python]` 范围内设置 `settings.json` ，将其设置为所有 Python 文件的默认格式化程序。您可以使用“首选项：打开用户设置 (JSON)”命令打开 `settings.json` 。

For example, to set Black Formatter as the default formatter, add the following setting to your User `settings.json` file:

​​​	例如，要将 Black Formatter 设置为默认格式化程序，请将以下设置添加到您的用户 `settings.json` 文件中：

```
  "[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter"
  }
```

In order to set a formatter extension as an import sorter, you can set your preference under `"editor.codeActionsOnSave"` in your User `settings.json` file or your Workspace `settings.json` file, under a `[python]` scope. You can open these `settings.json` files using the **Preferences: Open User Settings (JSON)** and **Preferences: Open Workspace Settings (JSON)** commands respectively. This will enable import sorting on save for all Python files.

​​​	为了将格式化程序扩展名设置为导入排序器，您可以在用户 `settings.json` 文件或工作区 `settings.json` 文件中的 `[python]` 范围内设置您的首选项。您可以分别使用“首选项：打开用户设置 (JSON)”和“首选项：打开工作区设置 (JSON)”命令打开这些 `settings.json` 文件。这将为所有 Python 文件启用保存时的导入排序。

For example, to set Ruff as your preferred import sorter, you can add the following setting to your User `settings.json` or your Workspace `settings.json` file:

​​​	例如，要将 Ruff 设置为您的首选导入排序器，您可以将以下设置添加到您的用户 `settings.json` 或工作区 `settings.json` 文件中：

```
{
  "[python]": {
    "editor.codeActionsOnSave": {
      "source.organizeImports.ruff": "explicit"
    }
  }
}
```

## [Format your code 格式化您的代码]({{< ref "/Python/Formatting#_format-your-code" >}})

You can format your code by right-clicking on the editor and selecting **Format Document**, or by using the Shift+Alt+F keyboard shortcut.

​​​	您可以通过右键单击编辑器并选择“格式化文档”或使用 Shift+Alt+F 键盘快捷键来格式化您的代码。

You can also add the following setting to your User `settings.json` file to enable formatting on save for your code:

​​​	您还可以将以下设置添加到您的用户 `settings.json` 文件中，以便为您的代码启用保存时格式化：

```
  "[python]": {
    "editor.formatOnSave": true
  }
```

## [General formatting settings 常规格式化设置]({{< ref "/Python/Formatting#_general-formatting-settings" >}})

Each formatter extension may have its own settings, but the ones below are supported by both [autopep8](https://marketplace.visualstudio.com/items?itemName=ms-python.autopep8) and [Black Formatter](https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter):

​​​	每个格式化程序扩展名可能都有其自己的设置，但以下设置受 autopep8 和 Black Formatter 支持：

| Setting Suffix 设置 后缀   | Default value 默认值 | Description 说明                                             |
| :------------------------- | :------------------- | :----------------------------------------------------------- |
| args                       | `[]`                 | Arguments to be passed to the formatter. Each argument should be passed as a separate string in the array. 要传递给格式化程序的参数。每个参数都应作为数组中的一个单独字符串传递。 For example: 例如： `black-formatter.args: ["--line-length", "100"]` |
| importStrategy             | `useBundled`         | When set to `useBundled`, the extension uses the version of the tool that it ships with. When set to `fromEnvironment`, it attempts to load from your selected Python environment first, otherwise it falls back to the bundled version. 当设置为 `useBundled` 时，扩展使用它附带的工具版本。当设置为 `fromEnvironment` 时，它首先尝试从您选择的 Python 环境中加载，否则它会回退到捆绑版本。 |
| path 路径                  | `""`                 | Path to the formatter binary to be used for formatting. **Note:** Using this option may slow down formatting. 要用于格式化的格式化程序二进制文件的路径。注意：使用此选项可能会降低格式化速度。 |
| interpreter 解释器         | `[]`                 | When set to a path to a Python executable, the extension will use that to launch the formatter server and its subprocesses. 当设置为 Python 可执行文件的路径时，扩展程序将使用该路径启动格式化程序服务器及其子进程。 |
| showNotifications 显示通知 | `off`                | Controls when notifications are displayed by this extension. Supported values are `off`, `always`, `onError`, and `onWarning`. 控制此扩展程序何时显示通知。支持的值为 `off` 、 `always` 、 `onError` 和 `onWarning` 。 |

## [Troubleshoot formatting 解决格式化问题]({{< ref "/Python/Formatting#_troubleshoot-formatting" >}})

If formatting fails, check the following possible causes:

​​​	如果格式化失败，请检查以下可能原因：

| Problem 问题                                                 | Solution 解决方案                                            |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| There are multiple formatters available for Python files. Python 文件有多种可用的格式化程序。 | Set the default formatter by following the instructions in [the section above]({{< ref "/Python/Formatting#_set-a-default-formatter" >}}). 按照上面部分中的说明设置默认格式化程序。 |
| Custom arguments for the formatter are incorrect. 格式化程序的自定义参数不正确。 | Check that the appropriate `<formatter>.path` setting does not contain arguments, and that `<formatter>.args` contains a list of individual top-level argument elements. 检查相应的 `<formatter>.path` 设置是否不包含参数，以及 `<formatter>.args` 是否包含单独的顶级参数元素列表。 |
| The **Format Selection** command fails when using Black Formatter. 使用 Black 格式化程序时，格式选择命令会失败。 | `black` does not support formatting sections of code. To work around this limitation, you can disable format on paste and set `formatOnSave` to format the whole file with the following settings: `"[python]": {"editor.formatOnPaste": false, "editor.formatOnSaveMode": "file"}`. `black` 不支持格式化代码部分。要解决此限制，您可以禁用粘贴时格式化，并将 `formatOnSave` 设置为使用以下设置格式化整个文件： `"[python]": {"editor.formatOnPaste": false, "editor.formatOnSaveMode": "file"}` 。 |
| The document isn't formatted. 文档未格式化。                 | Check the formatter extension's Output channel to understand why the formatter has failed (run the **Output: Focus on Output** command in the Command Palette and then select the formatter extension channel). 检查格式化程序扩展的输出通道以了解格式化程序失败的原因（在命令面板中运行输出：关注输出命令，然后选择格式化程序扩展通道）。 |

> **Note**: If you don't find your preferred formatter listed above, you can add support via an extension. The [Python Extension Template](https://code.visualstudio.com/api/advanced-topics/python-extension-template) makes it easy to integrate new Python tools into VS Code.
>
> ​​​	注意：如果您在上面未找到您首选的格式化程序，您可以通过扩展添加支持。Python 扩展模板可以轻松地将新的 Python 工具集成到 VS Code 中。

## [Next steps 后续步骤]({{< ref "/Python/Formatting#_next-steps" >}})

- [Debugging]({{< ref "/Python/Debugging" >}}) - Learn to debug Python both locally and remotely.
  调试 - 了解如何在本地和远程调试 Python。
- [Testing]({{< ref "/Python/Testing" >}}) - Configure test environments and discover, run, and debug tests.
  测试 - 配置测试环境并发现、运行和调试测试。
- [Basic Editing]({{< ref "/UserGuide/BasicEditing" >}}) - Learn about the powerful VS Code editor.
  基本编辑 - 了解功能强大的 VS Code 编辑器。
- [Code Navigation]({{< ref "/UserGuide/CodeNavigation" >}}) - Move quickly through your source code.
  代码导航 - 快速浏览源代码。
- [Python Extension Template](https://code.visualstudio.com/api/advanced-topics/python-extension-template) - Create an extension to integrate your favorite linter into VS Code.
  Python 扩展模板 - 创建一个扩展，将您最喜欢的 linter 集成到 VS Code 中。
