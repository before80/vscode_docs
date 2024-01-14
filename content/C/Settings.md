+++
title = "Settings"
date = 2024-01-12T22:36:24+08:00
weight = 110
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/cpp/customize-default-settings-cpp](https://code.visualstudio.com/docs/cpp/customize-default-settings-cpp)

# Customizing default settings 自定义默认设置



You can override the default values for properties set in `c_cpp_properties.json`.

​​​	您可以在 `c_cpp_properties.json` 中设置的属性的默认值中进行覆盖。

## [Visual Studio Code settings Visual Studio Code 设置]({{< ref "/C/Settings#_visual-studio-code-settings" >}})

The following `C_Cpp.default.*` settings map to each of the properties in a configuration block of `c_cpp_properties.json`. Namely:

​​​	以下 `C_Cpp.default.*` 设置映射到 `c_cpp_properties.json` 的配置块中的每个属性。即：

```
C_Cpp.default.includePath                          : string[]
C_Cpp.default.defines                              : string[]
C_Cpp.default.compileCommands                      : string
C_Cpp.default.macFrameworkPath                     : string[]
C_Cpp.default.forcedInclude                        : string[]
C_Cpp.default.intelliSenseMode                     : string
C_Cpp.default.compilerPath                         : string
C_Cpp.default.compilerArgs                         : string[]
C_Cpp.default.configurationProvider                : string
C_Cpp.default.customConfigurationVariables         : object | null
C_Cpp.default.cStandard                            : c89 | c99 | c11 | c17
C_Cpp.default.cppStandard                          : c++98 | c++03 | c++11 | c++14 | c++17 | c++20 | c++23
C_Cpp.default.enableConfigurationSquiggles         : boolean
C_Cpp.default.mergeConfigurations                  : boolean
C_Cpp.default.systemIncludePath                    : string[]
C_Cpp.default.windowsSdkVersion                    : string
C_Cpp.default.browse.path                          : string[]
C_Cpp.default.browse.defines                       : string[]
C_Cpp.default.browse.dotConfig                     : string
C_Cpp.default.browse.databaseFilename              : string
C_Cpp.default.browse.limitSymbolsToIncludedHeaders : boolean
```

These settings have all of the benefits of VS Code settings, meaning that they can have default, "User", "Workspace", and "Folder" values. So you can set a global value for `C_Cpp.default.cppStandard` in your "User" settings and have it apply to all of the folders you open. If any one folder needs a different value, you can override the value by adding a "Folder" or "Workspace" value.

​​​	这些设置具有 VS Code 设置的所有优点，这意味着它们可以具有默认值、“用户”、“工作区”和“文件夹”值。因此，您可以在“用户”设置中为 `C_Cpp.default.cppStandard` 设置全局值，并将其应用于您打开的所有文件夹。如果任何一个文件夹需要不同的值，您可以通过添加“文件夹”或“工作区”值来覆盖该值。

This property of VS Code settings allows you to configure each of your workspaces independently - making the `c_cpp_properties.json` file optional.

​​​	VS Code 设置的此属性允许您独立配置每个工作区 - 使 `c_cpp_properties.json` 文件成为可选的。

## [Updated c_cpp_properties.json syntax 更新的 c_cpp_properties.json 语法]({{< ref "/C/Settings#_updated-ccpppropertiesjson-syntax" >}})

A special variable has been added to the accepted syntax of `c_cpp_properties.json` that will instruct the extension to insert the value from the VS Code settings mentioned above. If you set the value of any setting in `c_cpp_properties.json` to "${default}" it will instruct the extension to read the VS Code default setting for that property and insert it. For example:

​​​	已将一个特殊变量添加到 `c_cpp_properties.json` 的接受语法中，该变量将指示扩展插入上述 VS Code 设置中的值。如果您将 `c_cpp_properties.json` 中的任何设置的值设置为“${default}”，它将指示扩展读取该属性的 VS Code 默认设置并将其插入。例如：

```
"configurations": [
    {
        "name": "Win32",
        "includePath": [
            "additional/paths",
            "${default}"
        ],
        "defines": [
            "${default}"
        ],
        "macFrameworkPath": [
            "${default}",
            "additional/paths"
        ],
        "forcedInclude": [
            "${default}",
            "additional/paths"
        ],
        "compileCommands": "${default}",
        "browse": {
            "limitSymbolsToIncludedHeaders": true,
            "databaseFilename": "${default}",
            "path": [
                "${default}",
                "additional/paths"
            ]
        },
        "intelliSenseMode": "${default}",
        "cStandard": "${default}",
        "cppStandard": "${default}",
        "compilerPath": "${default}"
    }
],
```

Note that for the properties that accept string[], the syntax proposed above allows you to augment the VS Code setting with additional values, thus allowing you to have common paths listed in the VS Code settings and configuration-specific settings in `c_cpp_properties.json`.

​​​	请注意，对于接受 string[] 的属性，上述建议的语法允许您使用其他值来扩充 VS Code 设置，从而允许您在 VS Code 设置和 `c_cpp_properties.json` 中的特定于配置的设置中列出常见路径。

If a property is missing from `c_cpp_properties.json`, the extension will use the value in the VS Code setting. If a developer assigns values to all of the settings that apply for a given folder, then `c_cpp_properties.json` could be removed from the .vscode folder as it will no longer be needed.

​​​	如果 `c_cpp_properties.json` 中缺少某个属性，则扩展程序将使用 VS Code 设置中的值。如果开发人员为适用于给定文件夹的所有设置分配值，则可以从 .vscode 文件夹中删除 `c_cpp_properties.json` ，因为它不再需要。

For in-depth information about the c_cpp_properties.json settings file, See [c_cpp_properties.json reference](https://code.visualstudio.com/docs/cpp/c-cpp-properties-schema-reference).

​​​	有关 c_cpp_properties.json 设置文件的详细信息，请参阅 c_cpp_properties.json 参考。

### [System includes 系统包含]({{< ref "/C/Settings#_system-includes" >}})

A new setting will be added that allows you specify the system include path separate from the folder's include path. If this setting has a value, then the system include path the extension gets from the compiler specified in the `compilerPath` setting will not be added to the path array that the extension uses for IntelliSense. We may want to provide a VS Code command to populate this value from the compiler's default for users who are interested in using it in case they want to make some modifications to the defaults.

​​​	将添加一个新设置，允许您指定系统包含路径，该路径与文件夹的包含路径分开。如果此设置具有值，则扩展程序从 `compilerPath` 设置中指定的编译器获取的系统包含路径不会添加到扩展程序用于 IntelliSense 的路径数组中。我们可能希望提供一个 VS Code 命令，以便为有兴趣使用此值的用户的编译器默认值填充此值，以防他们想要对默认值进行一些修改。

```
C_Cpp.default.systemIncludePath : string[]
```

### [System include path/defines resolution strategies 系统包含路径/定义解析策略]({{< ref "/C/Settings#_system-include-pathdefines-resolution-strategies" >}})

The extension determines the system includePath and defines to send to the IntelliSense engine in the following manner:

​​​	扩展名以以下方式确定要发送到 IntelliSense 引擎的系统 includePath 和定义：

1. If `compileCommands` has a valid value and the file open in the editor is in the database, use the compile command in the database entry to determine the include path and defines.

   ​​​	如果 `compileCommands` 具有有效值，并且编辑器中打开的文件位于数据库中，请使用数据库条目中的编译命令来确定包含路径和定义。

   - The system include path and defines are determined using the following logic (in order):

     
     系统包含路径和定义使用以下逻辑（按顺序）确定：

     1. If `systemIncludePath` has a value, use it (continue to the next step to search for system defines).
        如果 `systemIncludePath` 具有值，请使用它（继续执行下一步以搜索系统定义）。
     2. If `compilerPath` is valid, query it.
        如果 `compilerPath` 有效，请查询它。
     3. Interpret the first argument in the command as the compiler and attempt to query it.
        将命令中的第一个参数解释为编译器，并尝试查询它。
     4. If `compilerPath` is "", use an empty array for system include path and defines.
        如果 `compilerPath` 为“”，请对系统包含路径和定义使用一个空数组。
     5. If `compilerPath` is undefined, look for a compiler on the system and query it.
        如果 `compilerPath` 未定义，请在系统上查找编译器并查询它。

2. If `compileCommands` is invalid or the current file is not listed in the database, use the `includePath` and `defines` properties in the configuration for IntelliSense.

   ​​​	如果 `compileCommands` 无效或当前文件未在数据库中列出，请使用 IntelliSense 配置中的 `includePath` 和 `defines` 属性。

   - The system include path and defines are determined using the following logic (in order):

     
     系统包含路径和定义使用以下逻辑（按顺序）确定：

     1. If `systemIncludePath` has a value, use it (continue to the next step to search for system defines).
        如果 `systemIncludePath` 有值，则使用它（继续执行下一步以搜索系统定义）。
     2. If `compilerPath` is valid, query it.
        如果 `compilerPath` 有效，则查询它。
     3. If `compilerPath` is "", use an empty array for system include path and defines (they are assumed to be in the `includePath` and `defines` for the current config already).
        如果 `compilerPath` 为“”，则对系统包含路径和定义使用一个空数组（假定它们已在当前配置的 `includePath` 和 `defines` 中）。
     4. If `compilerPath` is undefined, look for a compiler on the system and query it.
        如果 `compilerPath` 未定义，则在系统上查找编译器并查询它。

System includes should not be added to the `includePath` or `browse.path` variables. If the extension detects any system include paths in the `includePath` property it will silently remove them so that it can ensure system include paths are added last and in the correct order (this is especially important for GCC/Clang).

​​​	不应将系统包含项添加到 `includePath` 或 `browse.path` 变量中。如果扩展在 `includePath` 属性中检测到任何系统包含路径，它将静默删除它们，以便确保系统包含路径最后添加且按正确顺序添加（这对于 GCC/Clang 尤为重要）。

### [Enhanced semantic colorization 增强的语义着色]({{< ref "/C/Settings#_enhanced-semantic-colorization" >}})

When IntelliSense is enabled, the Visual Studio Code C/C++ extension supports semantic colorization. See [Enhanced colorization](https://code.visualstudio.com/docs/cpp/colorization-cpp) for more details about setting colors for classes, functions, variables and so on.

​​​	启用 IntelliSense 时，Visual Studio Code C/C++ 扩展支持语义着色。有关为类、函数、变量等设置颜色的详细信息，请参阅增强的着色。

### [Extension logging 扩展日志记录]({{< ref "/C/Settings#_extension-logging" >}})

If you are experiencing a problem with the extension that we can't diagnose based on information in your issue report, we might ask you to enable logging and send us your logs. See [C/C++ extension logging](https://code.visualstudio.com/docs/cpp/enable-logging-cpp) for information about how to collect logs.

​​​	如果您遇到扩展问题，而我们无法根据您的问题报告中的信息进行诊断，我们可能会要求您启用日志记录并向我们发送您的日志。请参阅 C/C++ 扩展日志记录，了解有关如何收集日志的信息。
