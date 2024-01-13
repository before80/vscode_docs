+++
title = "Settings Reference"
date = 2024-01-12T22:36:24+08:00
weight = 140
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/python/settings-reference](https://code.visualstudio.com/docs/python/settings-reference)

# Python settings reference Python 设置参考



The Python Extension for Visual Studio Code is highly configurable. This page describes the key settings you can work with.

​​​	Visual Studio Code 的 Python 扩展高度可配置。此页面介绍您可以使用的主要设置。

For general information about working with settings in VS Code, refer to [User and workspace settings](https://code.visualstudio.com/docs/getstarted/settings), as well as the [Variables reference](https://code.visualstudio.com/docs/editor/variables-reference) for information about predefined variable support.

​​​	有关在 VS Code 中使用设置的常规信息，请参阅用户和工作区设置，以及变量参考以了解有关预定义变量支持的信息。

## [General Python settings 常规 Python 设置](https://code.visualstudio.com/docs/python/settings-reference#_general-python-settings)

| Setting 设置 (python.)                | Default 默认                   | Description 说明                                             |
| :------------------------------------ | :----------------------------- | :----------------------------------------------------------- |
| condaPath                             | `"conda"`                      | Path to the `conda` executable. 可执行文件的路径。           |
| defaultInterpreterPath                | `"python"`                     | Path to the default Python interpreter to be used by the Python extension on the first time it loads for a workspace, or the path to a folder containing the Python interpreter. Python 扩展在首次为工作区加载时要使用的默认 Python 解释器的路径，或包含 Python 解释器的文件夹的路径。 Can use variables like `${workspaceFolder}` and `${workspaceFolder}/.venv`. 可以使用变量，如 `${workspaceFolder}` 和 `${workspaceFolder}/.venv` 。 Using a path to a folder allows anyone working with a project to create an environment in the `.venv` folder as appropriate to their operating system, rather than having to specify an exact platform-dependent path. The `settings.json` file can then be included in a source code repository. 使用文件夹的路径允许与项目合作的任何人在 `.venv` 文件夹中创建适合其操作系统的环境，而无需指定确切的平台相关路径。然后可以将 `settings.json` 文件包含在源代码存储库中。 **Note**: Changes to this setting made after an interpreter has been selected for a workspace will not be applied or considered by the Python extension. The Python extension doesn't automatically add or change this setting. 注意：在为工作区选择解释器后对该设置所做的更改不会被 Python 扩展应用或考虑。Python 扩展不会自动添加或更改此设置。 |
| interpreter.infoVisibility            | `"onPythonRelated"`            | Controls when to display the selected interpreter information on the status bar. 控制何时在状态栏中显示所选解释器信息。 By default, it only shows when there are Python related files open in the editor. 默认情况下，它仅在编辑器中打开 Python 相关文件时显示。 You can set it to `"always"` if you'd like it to always show on the status bar, or `"never"` to hide it entirely. 如果希望它始终显示在状态栏中，可以将其设置为 `"always"` ，或者将其设置为 `"never"` 以完全隐藏它。 |
| pipenvPath                            | `"pipenv"`                     | Path to the pipenv executable to use for activation. 要用于激活的 pipenv 可执行文件的路径。 |
| venvFolders                           | `[]`                           | Paths to folders where virtual environments are created. 创建虚拟环境的文件夹的路径。 Depending on the virtualization tool used, it can be the project itself: `${workspaceFolder}`, or separate folders for all virtual environments located side by side: `.\envs`, `~/.virtualenvs`, and so on. 根据所使用的虚拟化工具，它可以是项目本身： `${workspaceFolder}` ，或者并排放置所有虚拟环境的单独文件夹： `.\envs` 、 `~/.virtualenvs` 等。 |
| envFile                               | `"${workspaceFolder}/` `.env"` | Absolute path to a file containing environment variable definitions. 包含环境变量定义的文件的绝对路径。 See [Configuring Python environments - environment variable definitions file](https://code.visualstudio.com/docs/python/environments#_environment-variable-definitions-file). 请参阅配置 Python 环境 - 环境变量定义文件。 |
| globalModuleInstallation              | `false`                        | Specifies whether to install packages for the current user only using the `--user` command-line argument (the default), or to install for all users in the global environment (when set to `true`). Ignored when using a virtual environment. 指定是仅使用 `--user` 命令行参数为当前用户安装软件包（默认），还是在全局环境中为所有用户安装软件包（设置为 `true` 时）。使用虚拟环境时忽略。 For more information on the `--user` argument, see [pip - User Installs](https://pip.pypa.io/en/stable/user_guide/#user-installs). 有关 `--user` 参数的更多信息，请参阅 pip - 用户安装。 |
| poetryPath                            | `"poetry"`                     | Specifies the location of the [Poetry dependency manager](https://poetry.eustace.io/) executable, if installed. The default value `"poetry"` assumes the executable is in the current path. 如果已安装，指定 Poetry 依赖项管理器可执行文件的位置。默认值 `"poetry"` 假设可执行文件位于当前路径中。 The Python extension uses this setting to install packages when Poetry is available and there's a `poetry.lock` file in the workspace folder. Python 扩展使用此设置在工作区文件夹中存在 `poetry.lock` 文件时安装软件包。 |
| terminal.launchArgs                   | `[]`                           | Launch arguments that are given to the Python interpreter when you run a file using commands such as **Python: Run Python File in Terminal**. 使用诸如 Python: 在终端中运行 Python 文件之类的命令运行文件时提供给 Python 解释器的启动参数。 In the `launchArgs` list, each item is a top-level command-line element that's separated by a space (quoted values that contain spaces are a single top-level element and are thus one item in the list). 在 `launchArgs` 列表中，每个项目都是一个顶级命令行元素，由空格分隔（包含空格的引号值是一个顶级元素，因此是列表中的一个项目）。 For example, for the arguments `--a --b --c {"value1" : 1, "value2" : 2}`, the list items should be `["--a", "--b", "--c", "{\"value1\" : 1, \"value2\" : 2}\""]`. 例如，对于参数 `--a --b --c {"value1" : 1, "value2" : 2}` ，列表项应为 `["--a", "--b", "--c", "{\"value1\" : 1, \"value2\" : 2}\""]` 。 Note that VS Code ignores this setting when debugging because it instead uses arguments from your selected debugging configuration in `launch.json`. 请注意，VS Code 在调试时会忽略此设置，因为它会使用 `launch.json` 中所选调试配置中的参数。 |
| terminal.executeInFileDir             | `false`                        | Indicates whether to run a file in the file's directory instead of the current folder. 指示是否在文件的目录中运行文件，而不是在当前文件夹中运行文件。 |
| terminal.activateEnvironment          | `true`                         | Indicates whether to automatically activate the environment you select using the **Python: Select Interpreter** command when a new terminal is created. 指示在创建新终端时是否自动激活使用 Python: 选择解释器命令选择的 Python 环境。 For example, when this setting is `true` and you select a virtual environment, the extension automatically runs the environment's *activate* command when creating a new terminal (`source env/bin/activate` on macOS/Linux; `env\scripts\activate` on Windows). 例如，当此设置是 `true` 且您选择虚拟环境时，扩展将在创建新终端时自动运行环境的激活命令（在 macOS/Linux 上为 `source env/bin/activate` ；在 Windows 上为 `env\scripts\activate` ）。 |
| terminal.activateEnvInCurrentTerminal | `false`                        | Specifies whether to activate the currently open terminal when the Python extension is activated, using the virtual environment selected. 指定在使用所选虚拟环境激活 Python 扩展时是否激活当前打开的终端。 |
| terminal.focusAfterLaunch             | `false`                        | Whether to switch the cursor focus to the terminal when launching a Python terminal. 启动 Python 终端时是否将光标焦点切换到终端。 |
| logging.level                         | `error`                        | Specifies the level of logging to be performed by the extension. 指定扩展程序执行的日志记录级别。 The possible levels of logging, in increasing level of information provided, are `off`, `error`, `warn`, `info`, and `debug`. 日志记录的可能级别（提供的信息量依次增加）为 `off` 、 `error` 、 `warn` 、 `info` 和 `debug` 。 When set to `off`, which is not recommended, basic information will still be shown such as startup information and commands run by the Python extension. 如果设置为 `off` （不推荐），仍会显示基本信息，例如 Python 扩展程序运行的启动信息和命令。 At the `error` level, basic information and errors will be shown. 在 `error` 级别，将显示基本信息和错误。 At the `warn` level, basic, error, and warning information will be shown. At the `info` level, basic, error, warning, and additional information like method execution times and return values will be shown. At this time, the `debug` level doesn't display additional information. 在 `warn` 级别，将显示基本、错误和警告信息。在 `info` 级别，将显示基本、错误、警告以及其他信息，如方法执行时间和返回值。此时， `debug` 级别不会显示其他信息。 |
| experiments.enabled                   | `true`                         | Enables [A/B experiments in the Python extension](https://aka.ms/AAjvt9q). If enabled, you may be provided with proposed enhancements and/or features. 在 Python 扩展程序中启用 A/B 实验。如果启用，可能会向您提供建议的增强功能和/或特性。 |

## [Code analysis settings 代码分析设置](https://code.visualstudio.com/docs/python/settings-reference#_code-analysis-settings)

### [IntelliSense engine settings IntelliSense 引擎设置](https://code.visualstudio.com/docs/python/settings-reference#_intellisense-engine-settings)

> **Note:** If you have never changed your language server setting, your language server is set to Pylance via the “Default” setting value.
>
> ​​​	注意：如果您从未更改过语言服务器设置，则您的语言服务器将通过“默认”设置值设置为 Pylance。

| Setting 设置 (python.) | Default 默认 | Description 说明                                             |
| :--------------------- | :----------- | :----------------------------------------------------------- |
| languageServer         | Default 默认 | Defines type of the language server (Default, [Pylance](https://devblogs.microsoft.com/python/announcing-pylance-fast-feature-rich-language-support-for-python-in-visual-studio-code/), Jedi, and None). 定义语言服务器的类型（默认、Pylance、Jedi 和无）。 |

### [Python Language Server settings Python 语言服务器设置](https://code.visualstudio.com/docs/python/settings-reference#_python-language-server-settings)

#### [Pylance Language Server Pylance 语言服务器](https://code.visualstudio.com/docs/python/settings-reference#_pylance-language-server)

The language server settings apply when `python.languageServer` is `Pylance` or `Default`. If you have difficulties with the language server, see [Troubleshooting](https://github.com/microsoft/pylance-release/blob/main/TROUBLESHOOTING.md) in the language server repository.

​​​	当 `python.languageServer` 为 `Pylance` 或 `Default` 时，应用语言服务器设置。如果您在使用语言服务器时遇到困难，请参阅语言服务器存储库中的故障排除。

| Setting 设置 (python.analysis.) | Default 默认  | Description 说明                                             |
| :------------------------------ | :------------ | :----------------------------------------------------------- |
| typeCheckingMode                | off           | Specifies the level of type checking analysis to perform. 指定要执行的类型检查分析级别。 Available values are `off`, `basic`, and `strict`. 可用值是 `off` 、 `basic` 和 `strict` 。 When set to `off` no type checking analysis is conducted; unresolved imports/variables diagnostics are produced. 设置为 `off` 时，不执行任何类型检查分析；生成未解决的导入/变量诊断信息。 When set to `basic` non-type checking-related rules (all rules in `off`), as well as basic type checking rules are used. 设置为 `basic` 时，使用与类型检查无关的规则（ `off` 中的所有规则）以及基本类型检查规则。 When set to `strict` all type checking rules at the highest severity of error (including all rules in `off` and `basic` categories) are used. 设置为 `strict` 时，使用最高严重性错误的所有类型检查规则（包括 `off` 和 `basic` 类别中的所有规则）。 |
| diagnosticMode                  | openFilesOnly | Specifies what code files the language server analyzes for problems. 指定语言服务器分析哪些代码文件的问题。 Available values are `workspace` and `openFilesOnly`. 可用值是 `workspace` 和 `openFilesOnly` 。 |
| include                         | []            | Paths of directories or files that should be included in analysis. 应包含在分析中的目录或文件路径。 If no paths are specified, Pylance defaults to the directory that contains the workspace root. 如果未指定路径，Pylance 将默认为包含工作区根目录的目录。 Paths may contain wildcard characters such as `**` (a directory or multiple levels of directories), `*` (a sequence of zero or more characters), or `?` (a single character). 路径可能包含通配符，例如 `**` （目录或多级目录）、 `*` （零个或多个字符的序列）或 `?` （单个字符）。 |
| exclude                         | []            | Paths of directories or files that should not be included in analysis. 不应包含在分析中的目录或文件路径。 These override the directories listed under the `python.analysis.include` setting, allowing specific subdirectories to be excluded. 这些路径会覆盖在 `python.analysis.include` 设置下列出的目录，从而允许排除特定的子目录。 Note that files listed in this `exclude` setting may still be included in the analysis if they are referenced/imported by source files that are not in the excluded list. 请注意，如果此 `exclude` 设置中列出的文件被未在排除列表中的源文件引用/导入，则这些文件仍可能包含在分析中。 Paths may contain wildcard characters such as `**` (a directory or multiple levels of directories), `*` (a sequence of zero or more characters), or `?` (a single character). 路径可能包含通配符，例如 `**` （目录或多级目录）、 `*` （零个或多个字符的序列）或 `?` （单个字符）。 If no exclude paths are specified, Pylance automatically excludes the following: `**/node_modules`, `**/\_\_pycache\_\_`, `.git` and any virtual environment directories. 如果未指定排除路径，Pylance 会自动排除以下内容： `**/node_modules` 、 `**/\_\_pycache\_\_` 、 `.git` 以及任何虚拟环境目录。 |
| ignore                          | []            | Paths of directories or files whose diagnostic output (errors and warnings) should be suppressed, even if they are an included file or within the transitive closure of an included file. 即使是包含的文件或包含文件的传递闭包内，也应禁止其诊断输出（错误和警告）的目录或文件的路径。 Paths may contain wildcard characters such as `**` (a directory or multiple levels of directories), `*` (a sequence of zero or more characters), or `?` (a single character). 路径可能包含通配符，例如 `**` （目录或多级目录）、 `*` （零个或多个字符的序列）或 `?` （单个字符）。 If no value is provided, the value of `python.linting.ignorePatterns` (if set) will be used. 如果未提供值，则将使用 `python.linting.ignorePatterns` 的值（如果已设置）。 |
| stubPath                        | ./typings     | Specifies a path to a directory that contains custom type stubs. Each package's type stub file(s) are expected to be in its own subdirectory. 指定包含自定义类型存根的目录的路径。每个包的类型存根文件应位于其自己的子目录中。 |
| autoSearchPaths                 | true          | Indicates whether to automatically add search paths based on some predefined names (like `src`). Available values are `true` and `false`. 指示是否根据一些预定义的名称（如 `src` ）自动添加搜索路径。可用值是 `true` 和 `false` 。 |
| extraPaths                      | []            | Specifies extra search paths for import resolution. 指定用于导入解析的额外搜索路径。 Accepts paths specified as strings and separated by commas if there are multiple paths. For example: `["path 1","path 2"]`. 如果有多个路径，则接受指定为字符串并用逗号分隔的路径。例如： `["path 1","path 2"]` . |
| indexing                        | true          | Used to specify whether Pylance should index user files as well as installed third party libraries at start up, to provide a more complete set of symbols in features such as auto imports, Quick Fixes, auto completions, etc. 用于指定 Pylance 是否应在启动时对用户文件以及已安装的第三方库进行索引，以便在自动导入、快速修复、自动完成等功能中提供更完整的符号集。 Accepted values are `true` or `false`. 可接受的值为 `true` 或 `false` 。 When set to `true`, by default Pylance indexes top-level symbols of installed packages (i.e., symbols in `__all__` under `package/__init__.py`), as well as all symbols from up to 2000 user files. 当设置为 `true` 时，默认情况下，Pylance 会对已安装包的顶级符号（即 `package/__init__.py` 下 `__all__` 中的符号）以及最多 2000 个用户文件的全部符号进行索引。 When set to `false`, Pylance will only display symbols already referenced or used in files that were previously opened in or loaded by the editor. 当设置为 `false` 时，Pylance 将仅显示在之前由编辑器打开或加载的文件中已引用或使用的符号。 |
| packageIndexDepths              | []            | Used to override how many levels under installed packages to index on a per package basis. 用于覆盖在每个包的基础上对已安装包下的多少层进行索引。 By default, only top-level modules are indexed (depth = 1). 默认情况下，仅对顶级模块进行索引（深度 = 1）。 To index submodules, increase depth by 1 for each level of submodule you want to index. 要对子模块进行索引，请针对要索引的每个子模块级别将深度增加 1。 Accepted values are tuples of objects like `{"name": "package name (str)", "depth": "depth to scan (int)", "includeAllSymbols": "whether to include all symbols (bool)"}`. 可接受的值是类似于 `{"name": "package name (str)", "depth": "depth to scan (int)", "includeAllSymbols": "whether to include all symbols (bool)"}` 的对象元组。 If `includeAllSymbols` is set to `false`, only symbols in each package's `__all__` are included. When it's set to `true`, Pylance will index every module/top level symbol declarations in the file. 如果将 `includeAllSymbols` 设置为 `false` ，则仅包含每个包的 `__all__` 中的符号。当将其设置为 `true` 时，Pylance 将对文件中的每个模块/顶级符号声明进行索引。 Usage example: `[{"name": "sklearn", "depth": 2, "includeAllSymbols": true}, {"name": "matplotlib", "depth": 3, "includeAllSymbols": false}]` 使用示例： `[{"name": "sklearn", "depth": 2, "includeAllSymbols": true}, {"name": "matplotlib", "depth": 3, "includeAllSymbols": false}]` |
| userFileIndexingLimit           | 2000          | Sets the maximum number of user files for Pylance to index in the workspace. When set to -1, Pylance will index all files. 设置 Pylance 在工作区中索引的用户文件数上限。当设置为 -1 时，Pylance 将索引所有文件。 Note that indexing files is a performance-intensive task. 请注意，索引文件是一项性能密集型任务。 |
| autoFormatStrings               | false         | When typing "{" inside a string, whether to automatically prefix it with an "f". 在字符串中键入“{”时，是否自动在其前面加上“f”。 |
| completeFunctionParens          | false         | Adds parentheses to function completions. Accepted values are `true` and `false`. 向函数补全添加括号。可接受的值是 `true` 和 `false` 。 |
| useLibraryCodeForTypes          | true          | Parses the source code for a package when a type stub is not found. Available values are `true` and `false`. 在找不到类型存根时解析包的源代码。可用值是 `true` 和 `false` 。 |
| autoImportCompletions           | false         | Controls the offering of auto imports in completions. Available values are `true` and `false`. 控制在补全中提供自动导入。可用值是 `true` 和 `false` 。 |
| importFormat                    | `absolute`    | Defines the default format when auto importing modules. Accepted values are `absolute` or `relative`. 定义自动导入模块时的默认格式。接受的值是 `absolute` 或 `relative` 。 |
| inlayHints.variableTypes        | false         | Whether to display inlay hints for variable types. Accepted values are `true` or `false`. 是否显示变量类型的内联提示。接受的值是 `true` 或 `false` 。 |
| inlayHints.functionReturnTypes  | false         | Whether to display inlay hints for function return types. Accepted values are `true` or `false`. 是否显示函数返回类型的内联提示。接受的值是 `true` 或 `false` 。 |
| inlayHints.callArgumentNames    | false         | Whether to display inlay hints for call argument names. Accepted values are `true` or `false`. 是否显示调用参数名称的内联提示。接受的值是 `true` 或 `false` 。 |
| inlayHints.pytestParameters     | false         | Whether to display inlay hints for pytest fixture argument types. Accepted values are `true` or `false`. 是否为 pytest 固定参数类型显示内联提示。接受的值是 `true` 或 `false` 。 |
| diagnosticSeverityOverrides     | {}            | Allows a user to override the severity levels for individual diagnostics. 允许用户覆盖各个诊断的严重性级别。 For each rule, the available severity levels are `error` (red squiggle), `warning` (yellow squiggle), `information` (blue squiggle), and `none` (rule disabled). 对于每条规则，可用的严重性级别为 `error` （红色波浪线）、 `warning` （黄色波浪线）、 `information` （蓝色波浪线）和 `none` （禁用规则）。 For information about the keys to use for the diagnostic severity rules, see the **Diagnostic severity rules** section below. 有关用于诊断严重性规则的键的信息，请参阅下面的诊断严重性规则部分。 |
| fixAll                          | `[]`          | A list of code actions to run when running the **Fix All** command or the `source.fixAll` code action. 运行修复所有命令或 `source.fixAll` 代码操作时要运行的代码操作列表。 Accepted values in this list: 此列表中接受的值：`source.unusedImports`: removes all unused imports in the open file `source.unusedImports` ：删除打开文件中所有未使用的导入`source.convertImportFormat`: converts the imports according to the `python.analysis.importFormat` setting `source.convertImportFormat` ：根据 `python.analysis.importFormat` 设置 |
| logLevel                        | `Error`       | Specifies the level of logging to be performed by the language server. 转换导入项 The possible levels of logging, in increasing level of information provided, are `Error`, `Warning`, `Information`, and `Trace`. 指定语言服务器执行的日志记录级别。 |

**Diagnostic severity rules
日志记录的可能级别（按提供的信息量递增）为 、、 和 。**

This section details all the available rules that can be customized using the `python.analysis.diagnosticSeverityOverrides` setting as shown in the following example.

​​​	诊断严重性规则

```
{
  "python.analysis.diagnosticSeverityOverrides": {
    "reportUnboundVariable": "information",
    "reportImplicitStringConcatenation": "warning"
  }
}
```

| Value 值                                                     | Description 说明                                             |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| reportGeneralTypeIssues 本部分详细介绍了所有可用的规则，可以使用 设置进行自定义，如下例所示。 | Diagnostics for general type inconsistencies, unsupported operations, argument/parameter mismatches, etc. This covers all of the basic type-checking rules not covered by other rules. It does not include syntax errors. reportGeneralTypeIssues |
| reportPropertyTypeMismatch 一般类型不一致、不受支持的操作、参数/参数不匹配等的诊断。这涵盖了其他规则未涵盖的所有基本类型检查规则。不包括语法错误。 | Diagnostics for properties where the type of the value passed to the setter is not assignable to the value returned by the getter. Such mismatches violate the intended use of properties, which are meant to act like variables. reportPropertyTypeMismatch |
| reportFunctionMemberAccess                                   | Diagnostics for member accesses on functions. 函数成员访问的诊断。 |
| reportMissingImports                                         | Diagnostics for imports that have no corresponding imported python file or type stub file. 没有相应的导入的 Python 文件或类型存根文件的导入的诊断。 |
| reportMissingModuleSource                                    | Diagnostics for imports that have no corresponding source file. This happens when a type stub is found, but the module source file was not found, indicating that the code may fail at runtime when using this execution environment. Type checking will be done using the type stub. 没有相应源文件的导入的诊断。当找到类型存根，但未找到模块源文件时，就会发生这种情况，这表明在使用此执行环境时，代码在运行时可能会失败。类型检查将使用类型存根来完成。 |
| reportMissingTypeStubs                                       | Diagnostics for imports that have no corresponding type stub file (either a typeshed file or a custom type stub). The type checker requires type stubs to do its best job at analysis. 没有相应的类型存根文件（类型库文件或自定义类型存根）的导入的诊断。类型检查器需要类型存根来对其分析进行最佳处理。 |
| reportImportCycles                                           | Diagnostics for cyclical import chains. These are not errors in Python, but they do slow down type analysis and often hint at architectural layering issues. Generally, they should be avoided. 循环导入链的诊断。这些不是 Python 中的错误，但它们确实会减慢类型分析的速度，并且通常暗示着体系结构分层问题。通常，应避免这些问题。 |
| reportUnusedImport                                           | Diagnostics for an imported symbol that is not referenced within that file. 诊断文件内未引用的导入符号。 |
| reportUnusedClass                                            | Diagnostics for a class with a private name (starting with an underscore) that is not accessed. 诊断名称为私有（以一个下划线开头）且未访问的类。 |
| reportUnusedFunction                                         | Diagnostics for a function or method with a private name (starting with an underscore) that is not accessed. 诊断名称为私有（以一个下划线开头）且未访问的函数或方法。 |
| reportUnusedVariable                                         | Diagnostics for a variable that is not accessed. 诊断未访问的变量。 |
| reportDuplicateImport                                        | Diagnostics for an imported symbol or module that is imported more than once. 诊断导入多次的导入符号或模块。 |
| reportWildcardImportFromLibrary                              | Diagnostics for a wildcard import from an external library. 来自外部库的通配符导入的诊断。 |
| reportOptionalSubscript                                      | Diagnostics for an attempt to subscript (index) a variable with an Optional type. 尝试使用 Optional 类型对变量进行下标（索引）的诊断。 |
| reportOptionalMemberAccess                                   | Diagnostics for an attempt to access a member of a variable with an Optional type. 尝试访问具有 Optional 类型的变量的成员的诊断。 |
| reportOptionalCall                                           | Diagnostics for an attempt to call a variable with an Optional type. 尝试调用具有 Optional 类型的变量的诊断。 |
| reportOptionalIterable                                       | Diagnostics for an attempt to use an Optional type as an iterable value (e.g. within a for statement). 尝试将 Optional 类型用作可迭代值（例如，在 for 语句中）的诊断。 |
| reportOptionalContextManager                                 | Diagnostics for an attempt to use an Optional type as a context manager (as a parameter to a with statement). 诊断尝试将 Optional 类型用作上下文管理器（作为 with 语句的参数）。 |
| reportOptionalOperand                                        | Diagnostics for an attempt to use an Optional type as an operand to a binary or unary operator (like '+', '==', 'or', 'not'). 诊断尝试将 Optional 类型用作二元或一元运算符（如“+”、“==”、“or”、“not”）的操作数。 |
| reportUntypedFunctionDecorator                               | Diagnostics for function decorators that have no type annotations. These obscure the function type, defeating many type analysis features. 诊断没有类型注释的函数装饰器。这些装饰器会模糊函数类型，从而使许多类型分析功能失效。 |
| reportUntypedClassDecorator                                  | Diagnostics for class decorators that have no type annotations. These obscure the class type, defeating many type analysis features. 诊断没有类型注释的类装饰器。这些装饰器会模糊类类型，从而使许多类型分析功能失效。 |
| reportUntypedBaseClass                                       | Diagnostics for base classes whose type cannot be determined statically. These obscure the class type, defeating many type analysis features. 诊断无法静态确定其类型的基类的诊断。这些装饰器会模糊类类型，从而使许多类型分析功能失效。 |
| reportUntypedNamedTuple                                      | Diagnostics when “namedtuple” is used rather than “NamedTuple”. The former contains no type information, whereas the latter does. 当使用“namedtuple”而不是“NamedTuple”时，诊断。前者不包含类型信息，而后者包含。 |
| reportPrivateUsage                                           | Diagnostics for incorrect usage of private or protected variables or functions. Protected class members begin with a single underscore `_` and can be accessed only by subclasses. Private class members begin with a double underscore but do not end in a double underscore and can be accessed only within the declaring class. Variables and functions declared outside of a class are considered private if their names start with either a single or double underscore, and they cannot be accessed outside of the declaring module. 诊断不正确使用私有或受保护的变量或函数。受保护的类成员以单个下划线 `_` 开头，只能由子类访问。私有类成员以双下划线开头，但不以双下划线结尾，只能在声明类中访问。在类外部声明的变量和函数如果名称以单个或双下划线开头，则被视为私有，并且不能在声明模块外部访问。 |
| reportConstantRedefinition                                   | Diagnostics for attempts to redefine variables whose names are all-caps with underscores and numerals. 诊断尝试重新定义名称为全大写字母、下划线和数字的变量。 |
| reportIncompatibleMethodOverride                             | Diagnostics for methods that override a method of the same name in a base class in an incompatible manner (wrong number of parameters, incompatible parameter types, or incompatible return type). 诊断以不兼容的方式覆盖基类中同名方法的方法（参数数量错误、参数类型不兼容或返回类型不兼容）。 |
| reportIncompatibleVariableOverride                           | Diagnostics for class variable declarations that override a symbol of the same name in a base class with a type that is incompatible with the base class symbol type. 诊断用于类变量声明的情况，这些声明用与基类中同名符号不兼容的类型覆盖基类符号类型。 |
| reportInvalidStringEscapeSequence                            | Diagnostics for invalid escape sequences used within string literals. The Python specification indicates that such sequences will generate a syntax error in future versions. 诊断用于字符串文字中的无效转义序列的情况。Python 规范指出，此类序列将在未来版本中生成语法错误。 |
| reportUnknownParameterType                                   | Diagnostics for input or return parameters for functions or methods that have an unknown type. 诊断用于函数或方法的输入或返回参数，这些参数具有未知类型。 |
| reportUnknownArgumentType                                    | Diagnostics for call arguments for functions or methods that have an unknown type. 诊断用于函数或方法的调用参数，这些参数具有未知类型。 |
| reportUnknownLambdaType                                      | Diagnostics for input or return parameters for lambdas that have an unknown type. 诊断用于 lambda 的输入或返回参数，这些参数具有未知类型。 |
| reportUnknownVariableType                                    | Diagnostics for variables that have an unknown type. 类型未知的变量的诊断。 |
| reportUnknownMemberType                                      | Diagnostics for class or instance variables that have an unknown type. 类型未知的类或实例变量的诊断。 |
| reportMissingTypeArgument                                    | Diagnostics for when a generic class is used without providing explicit or implicit type arguments. 在未提供显式或隐式类型参数的情况下使用泛型类时的诊断。 |
| reportInvalidTypeVarUse                                      | Diagnostics for improper use of type variables in a function signature. 函数签名中不当使用类型变量的诊断。 |
| reportCallInDefaultInitializer                               | Diagnostics for function calls within a default value initialization expression. Such calls can mask expensive operations that are performed at module initialization time. 默认值初始化表达式中的函数调用诊断。此类调用可能会掩盖模块初始化时执行的昂贵操作。 |
| reportUnnecessaryIsInstance                                  | Diagnostics for 'isinstance' or 'issubclass' calls where the result is statically determined to be always true or always false. Such calls are often indicative of a programming error. 对于结果静态确定为始终为真或始终为假的“isinstance”或“issubclass”调用的诊断。此类调用通常表示编程错误。 |
| reportUnnecessaryCast                                        | Diagnostics for 'cast' calls that are statically determined to be unnecessary. Such calls are sometimes indicative of a programming error. 对于静态确定为不必要的“cast”调用的诊断。此类调用有时表示编程错误。 |
| reportAssertAlwaysTrue                                       | Diagnostics for 'assert' statement that will probably always assert. This can be indicative of a programming error. 对于可能始终断言的“assert”语句的诊断。这可能表示编程错误。 |
| reportSelfClsParameterName                                   | Diagnostics for a missing or misnamed “self” parameter in instance methods and “cls” parameter in class methods. Instance methods in metaclasses (classes that derive from “type”) are allowed to use “cls” for instance methods. 对于实例方法中缺少或错误命名的“self”参数以及类方法中缺少或错误命名的“cls”参数的诊断。元类（派生自“type”的类）中的实例方法允许对实例方法使用“cls”。 |
| reportImplicitStringConcatenation                            | Diagnostics for two or more string literals that follow each other, indicating an implicit concatenation. This is considered a bad practice and often masks bugs such as missing commas. 对于连续出现的两个或多个字符串文字的诊断，表示隐式连接。这被认为是一种不好的做法，通常会掩盖诸如缺少逗号之类的错误。 |
| reportUndefinedVariable                                      | Diagnostics for undefined variables. 未定义变量的诊断。      |
| reportUnboundVariable                                        | Diagnostics for unbound and possibly unbound variables. 未绑定和可能未绑定的变量的诊断。 |
| reportInvalidStubStatement                                   | Diagnostics for statements that should not appear within a stub file. 不应出现在存根文件中的语句的诊断。 |
| reportUnusedCallResult                                       | Diagnostics for call expressions whose results are not consumed and are not None. 其结果未被使用且不是 None 的调用表达式的诊断。 |
| reportUnsupportedDunderAll                                   | Diagnostics for unsupported operations performed on `__all__`. 对 `__all__` 执行的操作不受支持的诊断。 |
| reportUnusedCoroutine                                        | Diagnostics for call expressions that return a Coroutine and whose results are not consumed. 诊断返回协程且结果未使用的调用表达式。 |

## [AutoComplete settings 自动完成设置](https://code.visualstudio.com/docs/python/settings-reference#_autocomplete-settings)

| Setting 设置 (python.autoComplete.) | Default 默认 | Description 说明                                             | See also 另请参阅                                            |
| :---------------------------------- | :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| extraPaths                          | `[]`         | Specifies locations of additional packages for which to load autocomplete data. 指定要加载自动完成数据的其他包的位置。 | [Editing 编辑](https://code.visualstudio.com/docs/python/editing#_autocomplete-and-intellisense) |

## [Testing settings 测试设置](https://code.visualstudio.com/docs/python/settings-reference#_testing-settings)

### [General testing 常规测试](https://code.visualstudio.com/docs/python/settings-reference#_general-testing)

| Setting 设置 (python.testing.) | Default 默认 | Description 说明                                             | See also 另请参阅                                            |
| :----------------------------- | :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| cwd                            | null         | Specifies an optional working directory for tests. 指定测试的可选工作目录。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| promptToConfigure              | `true`       | Specifies whether VS Code prompts to configure a test framework if potential tests are discovered. 指定 VS Code 是否在发现潜在测试时提示配置测试框架。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| debugPort                      | `3000`       | Port number used for debugging of unittest tests. 用于调试单元测试的端口号。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| autoTestDiscoverOnSaveEnabled  | `true`       | Specifies whether to enable or disable auto run test discovery when saving a test file. 指定在保存测试文件时是否启用或禁用自动运行测试发现。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |

### [unittest framework unittest 框架](https://code.visualstudio.com/docs/python/settings-reference#_unittest-framework)

| Setting 设置 (python.testing.) | Default 默认                           | Description 说明                                             | See also 另请参阅                                            |
| :----------------------------- | :------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| unittestEnabled                | `false`                                | Specifies whether unittest is enabled for testing. 指定是否启用 unittest 进行测试。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| unittestArgs                   | `["-v", "-s", ".", "-p", "*test*.py"]` | Arguments to pass to unittest, where each top-level element that's separated by a space is a separate item in the list. 要传递给 unittest 的参数，其中每个以空格分隔的顶级元素都是列表中的一个单独项。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |

### [pytest framework pytest 框架](https://code.visualstudio.com/docs/python/settings-reference#_pytest-framework)

| Setting 设置 (python.testing.) | Default 默认 | Description 说明                                             | See also 另请参阅                                            |
| :----------------------------- | :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| pytestEnabled                  | `false`      | Specifies whether pytest is enabled for testing. 指定是否启用 pytest 进行测试。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| pytestPath                     | `"pytest"`   | Path to pytest. Use a full path if pytest is located outside the current environment. 指向 pytest 的路径。如果 pytest 位于当前环境之外，请使用完整路径。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |
| pytestArgs                     | `[]`         | Arguments to pass to pytest, where each top-level element that's separated by a space is a separate item in the list. When debugging tests with pytest-cov installed, include `--no-cov` in these arguments. 要传递给 pytest 的参数，其中每个以空格分隔的顶级元素都是列表中的一个单独项。在安装了 pytest-cov 的情况下调试测试时，请在这些参数中包含 `--no-cov` 。 | [Testing 测试](https://code.visualstudio.com/docs/python/testing) |

## [Predefined variables 预定义变量](https://code.visualstudio.com/docs/python/settings-reference#_predefined-variables)

The Python extension settings support predefined variables. Similar to the general VS Code settings, variables use the **${variableName}** syntax. Specifically, the extension supports the following variables:

​​​	Python 扩展设置支持预定义变量。与常规 VS Code 设置类似，变量使用 ${variableName} 语法。具体来说，该扩展支持以下变量：

- **${cwd}** - the task runner's current working directory on startup

  ​​​	${cwd} - 任务运行器在启动时的当前工作目录

- **${workspaceFolder}** - the path of the folder opened in VS Code

  ​​​	${workspaceFolder} - 在 VS Code 中打开的文件夹的路径

- **${workspaceRootFolderName}** - the name of the folder opened in VS Code without any slashes (/)

  ​​​	${workspaceRootFolderName} - 在 VS Code 中打开的文件夹的名称，不带任何斜杠 (/)

- **${workspaceFolderBasename}** - the name of the folder opened in VS Code without any slashes (/)

  ​​​	${workspaceFolderBasename} - 在 VS Code 中打开的文件夹的名称，不带任何斜杠 (/)

- **${file}** - the current opened file

  ​​​	${file} - 当前打开的文件

- **${relativeFile}** - the current opened file relative to `workspaceFolder`

  ​​​	${relativeFile} - 当前打开的文件相对于 `workspaceFolder`

- **${relativeFileDirname}** - the current opened file's dirname relative to `workspaceFolder`

  ​​​	${relativeFileDirname} - 当前打开文件的 dirname 相对于 `workspaceFolder`

- **${fileBasename}** - the current opened file's basename

  ​​​	${fileBasename} - 当前打开文件的 basename

- **${fileBasenameNoExtension}** - the current opened file's basename with no file extension

  ​​​	${fileBasenameNoExtension} - 当前打开文件的 basename，不带文件扩展名

- **${fileDirname}** - the current opened file's dirname

  ​​​	${fileDirname} - 当前打开文件的 dirname

- **${fileExtname}** - the current opened file's extension

  ​​​	${fileExtname} - 当前打开文件的扩展名

- **${lineNumber}** - the current selected line number in the active file

  ​​​	${lineNumber} - 活动文件中当前选定的行号

- **${selectedText}** - the current selected text in the active file

  ​​​	${selectedText} - 活动文件中当前选定的文本

- **${execPath}** - the path to the running VS Code executable

  ​​​	${execPath} - 正在运行的 VS Code 可执行文件的路径

For additional information about predefined variables and example usages, see the [Variables reference](https://code.visualstudio.com/docs/editor/variables-reference) in the general VS Code docs.

​​​	有关预定义变量和示例用法的更多信息，请参阅常规 VS Code 文档中的变量参考。

## [Next steps 后续步骤](https://code.visualstudio.com/docs/python/settings-reference#_next-steps)

- [Python environments](https://code.visualstudio.com/docs/python/environments) - Control which Python interpreter is used for editing and debugging.
  Python 环境 - 控制用于编辑和调试的 Python 解释器。
- [Editing code](https://code.visualstudio.com/docs/python/editing) - Learn about autocomplete, IntelliSense, formatting, and refactoring for Python.
  编辑代码 - 了解 Python 的自动完成、IntelliSense、格式化和重构。
- [Linting](https://code.visualstudio.com/docs/python/linting) - Enable, configure, and apply a variety of Python linters.
  Linting - 启用、配置和应用各种 Python linter。
- [Debugging](https://code.visualstudio.com/docs/python/debugging) - Learn to debug Python both locally and remotely.
  调试 - 了解如何在本地和远程调试 Python。
- [Testing](https://code.visualstudio.com/docs/python/testing) - Configure test environments and discover, run, and debug tests.
  测试 - 配置测试环境并发现、运行和调试测试。
