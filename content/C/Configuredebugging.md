+++
title = "Configure debugging"
date = 2024-01-12T22:36:24+08:00
weight = 100
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/cpp/launch-json-reference](https://code.visualstudio.com/docs/cpp/launch-json-reference)

# Configure C/C++ debugging 配置 C/C++ 调试



A `launch.json` file is used to configure the [debugger](https://code.visualstudio.com/docs/editor/debugging) in Visual Studio Code.

&zeroWidthSpace;A `launch.json` 文件用于配置 Visual Studio Code 中的调试器。

Visual Studio Code generates a `launch.json` (under a `.vscode` folder in your project) with almost all of the required information. To get started with debugging you need to fill in the `program` field with the path to the executable you plan to debug. This must be specified for both the launch and attach (if you plan to attach to a running instance at any point) configurations.

&zeroWidthSpace;Visual Studio Code 会生成一个 `launch.json` （在项目中的 `.vscode` 文件夹下），其中包含几乎所有所需的信息。若要开始调试，您需要使用要调试的可执行文件的路径填充 `program` 字段。必须为启动和附加（如果您计划在任何时候附加到正在运行的实例）配置指定此路径。

The generated file contains two sections, one that configures debugging for launch and a second that configures debugging for attach.

&zeroWidthSpace;生成的文件包含两个部分，一个用于配置启动调试，另一个用于配置附加调试。

## [Configure VS Code's debugging behavior 配置 VS Code 的调试行为](https://code.visualstudio.com/docs/cpp/launch-json-reference#_configure-vs-codes-debugging-behavior)

Set or change the following options to control VS Code's behavior during debugging:

&zeroWidthSpace;设置或更改以下选项以控制 VS Code 在调试期间的行为：

### [program (required) 程序（必需）](https://code.visualstudio.com/docs/cpp/launch-json-reference#_program-required)

Specifies the full path to the executable the debugger will launch or attach to. The debugger requires this location in order to load debug symbols.

&zeroWidthSpace;指定调试器将启动或附加到的可执行文件的完整路径。调试器需要此位置才能加载调试符号。

### [symbolSearchPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_symbolsearchpath)

Tells the Visual Studio Windows Debugger what paths to search for symbol (.pdb) files. Separate multiple paths with a semicolon. For example: `"C:\\Symbols;C:\\SymbolDir2"`.

&zeroWidthSpace;告诉 Visual Studio Windows 调试器搜索符号 (.pdb) 文件的路径。用分号分隔多个路径。例如： `"C:\\Symbols;C:\\SymbolDir2"` .

### [requireExactSource](https://code.visualstudio.com/docs/cpp/launch-json-reference#_requireexactsource)

An optional flag that tells the Visual Studio Windows Debugger to require current source code to match the pdb.

&zeroWidthSpace;一个可选标志，指示 Visual Studio Windows 调试器要求当前源代码与 pdb 匹配。

### [additionalSOLibSearchPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_additionalsolibsearchpath)

Tells GDB or LLDB what paths to search for .so files. Separate multiple paths with a semicolon. For example: `"/Users/user/dir1;/Users/user/dir2"`.

&zeroWidthSpace;告诉 GDB 或 LLDB 在何处搜索 .so 文件的路径。用分号分隔多个路径。例如： `"/Users/user/dir1;/Users/user/dir2"` .

### [externalConsole](https://code.visualstudio.com/docs/cpp/launch-json-reference#_externalconsole)

Used only when launching the debuggee. For `attach`, this parameter does not change the debuggee's behavior.

&zeroWidthSpace;仅在启动被调试程序时使用。对于 `attach` ，此参数不会更改被调试程序的行为。

- **Windows**: When set to true, it will spawn an external console. When set to false, it will use VS Code's integratedTerminal.
  Windows：当设置为 true 时，它将生成一个外部控制台。当设置为 false 时，它将使用 VS Code 的 integratedTerminal。
- **Linux**: When set to true, it will notify VS Code to spawn an external console. When set to false, it will use VS Code's integratedTerminal.
  Linux：当设置为 true 时，它将通知 VS Code 生成一个外部控制台。当设置为 false 时，它将使用 VS Code 的 integratedTerminal。
- **macOS**: When set to true, it will spawn an external console through `lldb-mi`. When set to false, the output can be seen in VS Code's debugConsole. Due to limitations within `lldb-mi`, integratedTerminal support is not available.
  macOS：当设置为 true 时，它将通过 `lldb-mi` 生成一个外部控制台。当设置为 false 时，可以在 VS Code 的 debugConsole 中看到输出。由于 `lldb-mi` 中的限制，integratedTerminal 支持不可用。

### [avoidWindowsConsoleRedirection](https://code.visualstudio.com/docs/cpp/launch-json-reference#_avoidwindowsconsoleredirection)

In order to support VS Code's Integrated Terminal with gdb on Windows, the extension adds console redirection commands to the debuggee's arguments to have console input and output show up in the integrated terminal. Setting this option to `true` will disable it.

&zeroWidthSpace;为了在 Windows 上支持 VS Code 的集成终端与 gdb，扩展将控制台重定向命令添加到被调试程序的参数中，以便控制台输入和输出显示在集成终端中。将此选项设置为 `true` 将禁用它。

### [logging 日志记录](https://code.visualstudio.com/docs/cpp/launch-json-reference#_logging)

Optional flags to determine what types of messages should be logged to the Debug Console.

&zeroWidthSpace;用于确定应将哪些类型的消息记录到调试控制台的可选标志。

- **exceptions**: Optional flag to determine whether exception messages should be logged to the Debug Console. Defaults to true.
  异常：用于确定是否应将异常消息记录到调试控制台的可选标志。默认为 true。
- **moduleLoad**: Optional flag to determine whether module load events should be logged to the Debug Console. Defaults to true.
  模块加载：用于确定是否应将模块加载事件记录到调试控制台的可选标志。默认为 true。
- **programOutput**: Optional flag to determine whether program output should be logged to the Debug Console. Defaults to true.
  程序输出：用于确定是否应将程序输出记录到调试控制台的可选标志。默认为 true。
- **engineLogging**: Optional flag to determine whether diagnostic engine logs should be logged to the Debug Console. Defaults to false.
  引擎日志记录：用于确定是否应将诊断引擎日志记录到调试控制台的可选标志。默认为 false。
- **trace**: Optional flag to determine whether diagnostic adapter command tracing should be logged to the Debug Console. Defaults to false.
  跟踪：用于确定是否应将诊断适配器命令跟踪记录到调试控制台的可选标志。默认为 false。
- **traceResponse**: Optional flag to determine whether diagnostic adapter command and response tracing should be logged to the Debug Console. Defaults to false.
  跟踪响应：用于确定是否应将诊断适配器命令和响应跟踪记录到调试控制台的可选标志。默认为 false。

### [visualizerFile 可视化程序文件](https://code.visualstudio.com/docs/cpp/launch-json-reference#_visualizerfile)

`.natvis` file to be used when debugging. See [Create custom views of native objects](https://learn.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects) for information on how to create Natvis files.

&zeroWidthSpace; `.natvis` 调试时要使用的文件。有关如何创建 Natvis 文件的信息，请参阅创建本机对象的自定义视图。

### [showDisplayString](https://code.visualstudio.com/docs/cpp/launch-json-reference#_showdisplaystring)

When a `visualizerFile` is specified, `showDisplayString` will enable the display string. Turning on this option can cause slower performance during debugging.

&zeroWidthSpace;当指定 `visualizerFile` 时， `showDisplayString` 将启用显示字符串。打开此选项可能会导致调试期间性能下降。

**Example:
示例：**

```
{
  "name": "C++ Launch (Windows)",
  "type": "cppvsdbg",
  "request": "launch",
  "program": "C:\\app1\\Debug\\app1.exe",
  "symbolSearchPath": "C:\\Symbols;C:\\SymbolDir2",
  "externalConsole": true,
  "logging": {
    "moduleLoad": false,
    "trace": true
  },
  "visualizerFile": "${workspaceFolder}/my.natvis",
  "showDisplayString": true
}
```

## [Configure the target application 配置目标应用程序](https://code.visualstudio.com/docs/cpp/launch-json-reference#_configure-the-target-application)

The following options enable you to modify the state of the target application when it is launched:

&zeroWidthSpace;以下选项允许您在启动目标应用程序时修改其状态：

### [args](https://code.visualstudio.com/docs/cpp/launch-json-reference#_args)

JSON array of command-line arguments to pass to the program when it is launched. Example `["arg1", "arg2"]`. If you are escaping characters, you will need to double escape them. For example, `["{\\\"arg1\\\": true}"]` will send `{"arg1": true}` to your application.

&zeroWidthSpace;启动程序时要传递给该程序的命令行参数的 JSON 数组。示例 `["arg1", "arg2"]` 。如果您要转义字符，则需要对其进行双重转义。例如， `["{\\\"arg1\\\": true}"]` 会将 `{"arg1": true}` 发送到您的应用程序。

### [cwd](https://code.visualstudio.com/docs/cpp/launch-json-reference#_cwd)

Sets the working directory of the application launched by the debugger.

&zeroWidthSpace;设置由调试器启动的应用程序的工作目录。

### [environment](https://code.visualstudio.com/docs/cpp/launch-json-reference#_environment)

Environment variables to add to the environment for the program. Example: `[ { "name": "config", "value": "Debug" } ]`, not `[ { "config": "Debug" } ]`.

&zeroWidthSpace;要添加到程序环境中的环境变量。示例： `[ { "name": "config", "value": "Debug" } ]` ，而不是 `[ { "config": "Debug" } ]` 。

**Example:
示例：**

```
{
  "name": "C++ Launch",
  "type": "cppdbg",
  "request": "launch",
  "program": "${workspaceFolder}/a.out",
  "args": ["arg1", "arg2"],
  "environment": [{ "name": "config", "value": "Debug" }],
  "cwd": "${workspaceFolder}"
}
```

## [Customizing GDB or LLDB 自定义 GDB 或 LLDB](https://code.visualstudio.com/docs/cpp/launch-json-reference#_customizing-gdb-or-lldb)

You can change the behavior of GDB or LLDB by setting the following options:

&zeroWidthSpace;您可以通过设置以下选项来更改 GDB 或 LLDB 的行为：

### [MIMode](https://code.visualstudio.com/docs/cpp/launch-json-reference#_mimode)

Indicates the debugger that VS Code will connect to. Must be set to `gdb` or `lldb`. This is pre-configured on a per-operating system basis and can be changed as needed.

&zeroWidthSpace;指示 VS Code 将连接到的调试器。必须设置为 `gdb` 或 `lldb` 。这是根据每个操作系统进行预先配置的，可以根据需要进行更改。

### [miDebuggerPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_midebuggerpath)

The path to the debugger (such as gdb). When only the executable is specified, it will search the operating system's PATH variable for a debugger (GDB on Linux and Windows, LLDB on OS X).

&zeroWidthSpace;调试器的路径（例如 gdb）。仅指定可执行文件时，它将在操作系统 PATH 变量中搜索调试器（Linux 和 Windows 上的 GDB，OS X 上的 LLDB）。

### [miDebuggerArgs](https://code.visualstudio.com/docs/cpp/launch-json-reference#_midebuggerargs)

Additional arguments to pass to the debugger (such as gdb).

&zeroWidthSpace;传递给调试器的其他参数（例如 gdb）。

### [stopAtEntry](https://code.visualstudio.com/docs/cpp/launch-json-reference#_stopatentry)

If set to true, the debugger should stop at the entry-point of the target (ignored on attach). Default value is `false`.

&zeroWidthSpace;如果设置为 true，调试器应在目标的入口点处停止（在附加时忽略）。默认值为 `false` 。

### [stopAtConnect](https://code.visualstudio.com/docs/cpp/launch-json-reference#_stopatconnect)

If set to true, the debugger should stop after connecting to the target. If set to false, the debugger will continue after connecting. Default value is `false`.

&zeroWidthSpace;如果设置为 true，则调试器应在连接到目标后停止。如果设置为 false，则调试器将在连接后继续。默认值为 `false` 。

### [setupCommands](https://code.visualstudio.com/docs/cpp/launch-json-reference#_setupcommands)

JSON array of commands to execute in order to set up the GDB or LLDB. Example: `"setupCommands": [ { "text": "target-run", "description": "run target", "ignoreFailures": false }]`.

&zeroWidthSpace;要执行的 JSON 数组命令，以便设置 GDB 或 LLDB。示例： `"setupCommands": [ { "text": "target-run", "description": "run target", "ignoreFailures": false }]` 。

### [customLaunchSetupCommands](https://code.visualstudio.com/docs/cpp/launch-json-reference#_customlaunchsetupcommands)

If provided, this replaces the default commands used to launch a target with some other commands. For example, this can be "-target-attach" in order to attach to a target process. An empty command list replaces the launch commands with nothing, which can be useful if the debugger is being provided launch options as command-line options. Example: `"customLaunchSetupCommands": [ { "text": "target-run", "description": "run target", "ignoreFailures": false }]`.

&zeroWidthSpace;如果提供，则此命令将用其他一些命令替换用于启动目标的默认命令。例如，这可以是“-target-attach”，以便附加到目标进程。空命令列表将启动命令替换为空，如果将启动选项作为命令行选项提供给调试器，这可能很有用。示例： `"customLaunchSetupCommands": [ { "text": "target-run", "description": "run target", "ignoreFailures": false }]` 。

### [launchCompleteCommand](https://code.visualstudio.com/docs/cpp/launch-json-reference#_launchcompletecommand)

The command to execute after the debugger is fully set up in order to cause the target process to run. Allowed values are "exec-run", "exec-continue", "None". The default value is "exec-run".

&zeroWidthSpace;在调试器完全设置好后执行的命令，以便使目标进程运行。允许的值为“exec-run”、“exec-continue”、“None”。默认值为“exec-run”。

**Example:
示例：**

```
{
  "name": "C++ Launch",
  "type": "cppdbg",
  "request": "launch",
  "program": "${workspaceFolder}/a.out",
  "stopAtEntry": false,
  "customLaunchSetupCommands": [
    { "text": "target-run", "description": "run target", "ignoreFailures": false }
  ],
  "launchCompleteCommand": "exec-run",
  "linux": {
    "MIMode": "gdb",
    "miDebuggerPath": "/usr/bin/gdb"
  },
  "osx": {
    "MIMode": "lldb"
  },
  "windows": {
    "MIMode": "gdb",
    "miDebuggerPath": "C:\\MinGw\\bin\\gdb.exe"
  }
}
```

### [symbolLoadInfo](https://code.visualstudio.com/docs/cpp/launch-json-reference#_symbolloadinfo)

- **loadAll**: If true, symbols for all libs will be loaded, otherwise no solib symbols will be loaded. Modified by ExceptionList. Default value is true.
  loadAll：如果为 true，则将加载所有库的符号，否则将不加载任何 solib 符号。由 ExceptionList 修改。默认值为 true。
- **exceptionList**: List of filenames (wildcards allowed) separated by semicolons `;`. Modifies behavior of LoadAll. If LoadAll is true then don't load symbols for libs that match any name in the list. Otherwise only load symbols for libs that match. Example: `"foo.so;bar.so"`
  exceptionList：以分号分隔的文件名列表（允许使用通配符） `;` 。修改 LoadAll 的行为。如果 LoadAll 为 true，则不要加载与列表中任何名称匹配的库的符号。否则，仅加载与匹配的库的符号。示例： `"foo.so;bar.so"`

## [Debugging dump files 调试转储文件](https://code.visualstudio.com/docs/cpp/launch-json-reference#_debugging-dump-files)

The C/C++ extension enables debugging dump files on Windows and core dump files Linux and OS X.

&zeroWidthSpace;C/C++ 扩展支持在 Windows 上调试转储文件，在 Linux 和 OS X 上调试核心转储文件。

### [dumpPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_dumppath)

If you want to debug a Windows dump file, set this to the path to the dump file to start debugging in the `launch` configuration.

&zeroWidthSpace;如果要调试 Windows 转储文件，请将其设置为转储文件的路径，以便在 `launch` 配置中开始调试。

### [coreDumpPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_coredumppath)

Full path to a core dump file to debug for the specified program. Set this to the path to the core dump file to start debugging in the `launch` configuration. *Note: core dump debugging is not supported with MinGw.*

&zeroWidthSpace;要为指定程序调试的核心转储文件的完整路径。将其设置为核心转储文件的路径，以便在 `launch` 配置中开始调试。注意：MinGw 不支持核心转储调试。

## [Remote debugging or debugging with a local debugger server 使用本地调试器服务器进行远程调试或调试](https://code.visualstudio.com/docs/cpp/launch-json-reference#_remote-debugging-or-debugging-with-a-local-debugger-server)

### [miDebuggerServerAddress](https://code.visualstudio.com/docs/cpp/launch-json-reference#_midebuggerserveraddress)

Network address of the debugger server (for example, gdbserver) to connect to for remote debugging (example: `localhost:1234`).

&zeroWidthSpace;要连接进行远程调试的调试器服务器（例如，gdbserver）的网络地址（例如： `localhost:1234` ）。

### [debugServerPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_debugserverpath)

Full path to debug server to launch.

&zeroWidthSpace;要启动的调试服务器的完整路径。

### [debugServerArgs](https://code.visualstudio.com/docs/cpp/launch-json-reference#_debugserverargs)

Arguments for the debugger server.

&zeroWidthSpace;调试器服务器的参数。

### [serverStarted](https://code.visualstudio.com/docs/cpp/launch-json-reference#_serverstarted)

Server-started pattern to look for in the debug server output. Regular expressions are supported.

&zeroWidthSpace;在调试服务器输出中查找的服务器已启动模式。支持正则表达式。

### [filterStdout](https://code.visualstudio.com/docs/cpp/launch-json-reference#_filterstdout)

If set to true, search `stdout` stream for server-started pattern and log stdout to debug output. Default value is `true`.

&zeroWidthSpace;如果设置为 true，则在 `stdout` 流中搜索服务器已启动模式并将 stdout 记录到调试输出。默认值为 `true` 。

### [filterStderr](https://code.visualstudio.com/docs/cpp/launch-json-reference#_filterstderr)

If set to true, search `stderr` stream for server-started pattern and log stderr to debug output. Default value is `false`.

&zeroWidthSpace;如果设置为 true，则在 `stderr` 流中搜索服务器已启动模式并将 stderr 记录到调试输出。默认值为 `false` 。

### [serverLaunchTimeout](https://code.visualstudio.com/docs/cpp/launch-json-reference#_serverlaunchtimeout)

Time in milliseconds, for the debugger to wait for the debugServer to start up. Default is 10000.

&zeroWidthSpace;调试器等待 debugServer 启动的时间（以毫秒为单位）。默认值为 10000。

### [pipeTransport](https://code.visualstudio.com/docs/cpp/launch-json-reference#_pipetransport)

For information about attaching to a remote process, such as debugging a process in a Docker container, see the [Pipe transport](https://code.visualstudio.com/docs/cpp/pipe-transport) settings article.

&zeroWidthSpace;有关如何附加到远程进程（例如调试 Docker 容器中的进程）的信息，请参阅管道传输设置一文。

### [hardwareBreakpoints](https://code.visualstudio.com/docs/cpp/launch-json-reference#_hardwarebreakpoints)

If provided, this explicitly controls hardware breakpoint behavior for remote targets. If `require` is set to true, always use hardware breakpoints. Default value is `false`. `limit` is an optional limit on the number of available hardware breakpoints to use which is only enforced when `require` is true and `limit` is greater than 0. Defaults value is 0. Example: `"hardwareBreakpoints": { require: true, limit: 6 }`.

&zeroWidthSpace;如果提供，则此项明确控制远程目标的硬件断点行为。如果将 `require` 设置为 true，则始终使用硬件断点。默认值为 `false` 。 `limit` 是可用于的硬件断点数量的可选限制，仅在 `require` 为 true 且 `limit` 大于 0 时强制执行。默认值为 0。示例： `"hardwareBreakpoints": { require: true, limit: 6 }` 。

## [Additional properties 其他属性](https://code.visualstudio.com/docs/cpp/launch-json-reference#_additional-properties)

### [processId](https://code.visualstudio.com/docs/cpp/launch-json-reference#_processid)

Defaults to `${command:pickProcess}` which will display a list of available processes the debugger can attach to. We recommend that you leave this default, but the property can be explicitly set to a specific process ID for the debugger to attach to.

&zeroWidthSpace;默认为 `${command:pickProcess}` ，这会显示调试器可以附加到的可用进程列表。我们建议您保留此默认值，但可以将该属性明确设置为调试器要附加到的特定进程 ID。

### [request](https://code.visualstudio.com/docs/cpp/launch-json-reference#_request)

Indicates whether the configuration section is intended to `launch` the program or `attach` to an already running instance.

&zeroWidthSpace;指示配置部分是打算 `launch` 程序还是 `attach` 到已运行的实例。

### [targetArchitecture](https://code.visualstudio.com/docs/cpp/launch-json-reference#_targetarchitecture)

`Deprecated` This option is no longer needed as the target architecture is automatically detected.

&zeroWidthSpace; `Deprecated` 不再需要此选项，因为会自动检测目标体系结构。

### [type](https://code.visualstudio.com/docs/cpp/launch-json-reference#_type)

Indicates the underlying debugger being used. Must be `cppvsdbg` when using the Visual Studio Windows debugger, and `cppdbg` when using GDB or LLDB. This is automatically set to the correct value when the `launch.json` file is created.

&zeroWidthSpace;指示正在使用的底层调试器。使用 Visual Studio Windows 调试器时必须为 `cppvsdbg` ，使用 GDB 或 LLDB 时必须为 `cppdbg` 。创建 `launch.json` 文件时，会自动将其设置为正确的值。

### [sourceFileMap](https://code.visualstudio.com/docs/cpp/launch-json-reference#_sourcefilemap)

This allows mapping of the compile-time paths for source to local source locations. It is an object of key/value pairs and will resolve the first string-matched path. (example: `"sourceFileMap": { "/mnt/c": "c:\\" }` will map any path returned by the debugger that begins with `/mnt/c` and convert it to `c:\\`. You can have multiple mappings in the object but they will be handled in the order provided.)

&zeroWidthSpace;这允许将源的编译时路径映射到本地源位置。它是一个键/值对的对象，并将解析第一个字符串匹配的路径。（示例： `"sourceFileMap": { "/mnt/c": "c:\\" }` 将映射调试器返回的任何以 `/mnt/c` 开头的路径并将其转换为 `c:\\` 。您可以在对象中有多个映射，但它们将按提供的顺序处理。）

## [Environment variable definitions file 环境变量定义文件](https://code.visualstudio.com/docs/cpp/launch-json-reference#_environment-variable-definitions-file)

An environment variable definitions file is a simple text file containing key-value pairs in the form of `environment_variable=value`, with `#` used for comments. Multiline values are not supported.

&zeroWidthSpace;环境变量定义文件是一个简单的文本文件，其中包含键值对，格式为 `environment_variable=value` ， `#` 用于注释。不支持多行值。

The `cppvsdbg` debugger configuration also contains an `envFile` property that allows you to easily set variables for debugging purposes.

&zeroWidthSpace;调试器配置还包含一个 `envFile` 属性，允许您轻松设置变量以进行调试。

For example:

&zeroWidthSpace;例如：

**project.env file**:

&zeroWidthSpace;project.env 文件：

```
# project.env

# Example environment with key as 'MYENVRIONMENTPATH' and value as C:\\Users\\USERNAME\\Project
MYENVRIONMENTPATH=C:\\Users\\USERNAME\\Project

# Variables with spaces
SPACED_OUT_PATH="C:\\This Has Spaces\\Project"
```

## [Symbol Options 符号选项](https://code.visualstudio.com/docs/cpp/launch-json-reference#_symbol-options)

The `symbolOptions` element allows customization of how the debugger searches for symbols. Example:

&zeroWidthSpace; `symbolOptions` 元素允许自定义调试器搜索符号的方式。示例：

```
    "symbolOptions": {
        "searchPaths": [
            "C:\\src\\MyOtherProject\\bin\\debug",
            "https://my-companies-symbols-server"
        ],
        "searchMicrosoftSymbolServer": true,
        "cachePath": "%TEMP%\\symcache",
        "moduleFilter": {
            "mode": "loadAllButExcluded",
            "excludedModules": [ "DoNotLookForThisOne*.dll" ]
        }
    }
```

### [Properties 属性](https://code.visualstudio.com/docs/cpp/launch-json-reference#_properties)

**searchPaths**: Array of symbol server URLs (example: https://msdl.microsoft.com/download/symbols) or directories (example: /build/symbols) to search for .pdb files. These directories will be searched in addition to the default locations -- next to the module and the path where the pdb was originally dropped to.

&zeroWidthSpace;searchPaths：符号服务器 URL（例如：https://msdl.microsoft.com/download/symbols）或目录（例如：/build/symbols）的数组，用于搜索 .pdb 文件。除了默认位置（模块旁边和最初将 pdb 放置到的路径）之外，还将在这些目录中进行搜索。

**searchMicrosoftSymbolServer**: If `true` the Microsoft Symbol server (https://msdl.microsoft.com/download/symbols) is added to the symbols search path. If unspecified, this option defaults to `false`.

&zeroWidthSpace;searchMicrosoftSymbolServer：如果将 Microsoft 符号服务器 (https://msdl.microsoft.com/download/symbols) 添加到符号搜索路径中。如果未指定，此选项默认为 `false` 。

**cachePath**": Directory where symbols downloaded from symbol servers should be cached. If unspecified, the debugger will default to %TEMP%\SymbolCache..

&zeroWidthSpace;cachePath": 从符号服务器下载的符号应缓存到的目录。如果未指定，调试器将默认为 %TEMP%\SymbolCache..

**moduleFilter.mode**: This value is either `"loadAllButExcluded"` or `"loadOnlyIncluded"`. In `"loadAllButExcluded"` mode, the debugger loads symbols for all modules unless the module is in the 'excludedModules' array. In `"loadOnlyIncluded"` mode, the debugger will not attempt to load symbols for ANY module unless it is in the 'includedModules' array, or it is included through the 'includeSymbolsNextToModules' setting.

&zeroWidthSpace;moduleFilter.mode：此值是 `"loadAllButExcluded"` 或 `"loadOnlyIncluded"` 。在 `"loadAllButExcluded"` 模式下，调试器会加载所有模块的符号，除非该模块位于“excludedModules”数组中。在 `"loadOnlyIncluded"` 模式下，调试器不会尝试加载任何模块的符号，除非该模块位于“includedModules”数组中，或通过“includeSymbolsNextToModules”设置包含该模块。

#### [Properties for "loadAllButExcluded" mode “loadAllButExcluded”模式的属性](https://code.visualstudio.com/docs/cpp/launch-json-reference#_properties-for-loadallbutexcluded-mode)

**moduleFilter.excludedModules**: Array of modules that the debugger should NOT load symbols for. Wildcards (example: MyCompany.*.dll) are supported.

&zeroWidthSpace;moduleFilter.excludedModules：调试器不应加载符号的模块数组。支持通配符（例如：MyCompany.*.dll）。

#### [Properties for "loadOnlyIncluded" mode “loadOnlyIncluded”模式的属性](https://code.visualstudio.com/docs/cpp/launch-json-reference#_properties-for-loadonlyincluded-mode)

**moduleFilter.includedModules**: Array of modules that the debugger should load symbols for. Wildcards (example: MyCompany.*.dll) are supported.

&zeroWidthSpace;moduleFilter.includedModules：调试器应加载符号的模块数组。支持通配符（例如：MyCompany.*.dll）。

**moduleFilter.includeSymbolsNextToModules**: If true, for any module NOT in the 'includedModules' array, the debugger will still check next to the module itself and the launching executable, but it will not check paths on the symbol search list. This option defaults to 'true'.

&zeroWidthSpace;moduleFilter.includeSymbolsNextToModules：如果为 true，对于“includedModules”数组中没有的任何模块，调试器仍会检查模块本身和启动的可执行文件旁边，但不会检查符号搜索列表中的路径。此选项默认为“true”。
