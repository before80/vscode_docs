+++
title = "FAQ"
date = 2024-01-12T22:36:24+08:00
weight = 140
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/cpp/faq-cpp](https://code.visualstudio.com/docs/cpp/faq-cpp)

# Frequently asked questions 常见问题



- [How do I get IntelliSense to work correctly?
  如何让 IntelliSense 正确工作？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-intellisense-to-work-correctly)
- [What is the difference between includePath and browse.path in c_cpp_properties.json?
  c_cpp_properties.json 中的 includePath 和 browse.path 有什么区别？](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-is-the-difference-between-includepath-and-browsepath)
- [Why do I see red squiggles under Standard Library types?
  为什么我在标准库类型下看到红色波浪线？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-do-i-see-red-squiggles-under-standard-library-types)
- [How do I get the new IntelliSense to work with MinGW on Windows?
  如何让新的 IntelliSense 在 Windows 上与 MinGW 配合使用？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-the-new-intellisense-to-work-with-mingw-on-windows)
- [How do I get the new IntelliSense to work with the Windows Subsystem for Linux?
  如何让新的 IntelliSense 在适用于 Linux 的 Windows 子系统中工作？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-the-new-intellisense-to-work-with-the-windows-subsystem-for-linux)
- [Why are my files corrupted on format?
  为什么我的文件在格式化时损坏？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-are-my-files-corrupted-on-format)
- [How do I recreate the IntelliSense database?
  如何重新创建 IntelliSense 数据库？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-recreate-the-intellisense-database)
- [What is the ipch folder?
  ipch 文件夹是什么？](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-is-the-ipch-folder)
- [How do I disable the IntelliSense cache (ipch)?
  如何禁用 IntelliSense 缓存 (ipch)？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-disable-the-intellisense-cache-ipch)
- [How do I set up debugging?
  如何设置调试？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-set-up-debugging)
- [How do I enable debug symbols?
  如何启用调试符号？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-enable-debug-symbols)
- [Why is debugging not working?
  为什么调试不起作用？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-is-debugging-not-working)
- [What do I do if I suspect a C/C++ extension problem
  如果我怀疑存在 C/C++ 扩展问题，该怎么办](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-do-i-do-if-i-suspect-a-cc-extension-problem)

## [How do I get IntelliSense to work correctly? 如何让 IntelliSense 正确工作？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-intellisense-to-work-correctly)

Without any configuration, the extension will attempt to locate headers by searching your workspace folder and by emulating a compiler it finds on your computer. (for example, cl.exe/MinGW for Windows, gcc/clang for macOS/Linux). If this automatic configuration is insufficient, you can modify the defaults by running the **C/C++: Edit Configurations (UI)** command. In that view, you can change the compiler you want to emulate, the paths to include files you want to use, preprocessor definitions, and more.

​​​	在没有任何配置的情况下，该扩展程序将尝试通过搜索工作区文件夹并模拟在计算机上找到的编译器来查找头文件。（例如，适用于 Windows 的 cl.exe/MinGW，适用于 macOS/Linux 的 gcc/clang）。如果此自动配置不足，可以通过运行 C/C++: 编辑配置 (UI) 命令来修改默认设置。在此视图中，您可以更改要模拟的编译器、要使用的包含文件的路径、预处理器定义等。

Or, if you install a build system extension that interfaces with our extension, you can allow that extension to provide the configurations for you. For example, the CMake Tools extension can configure projects that use the CMake build system. Use the **C/C++: Change Configuration Provider...** command to enable any such extension to provide the configurations for IntelliSense.

​​​	或者，如果您安装了与我们的扩展程序连接的构建系统扩展程序，则可以允许该扩展程序为您提供配置。例如，CMake Tools 扩展程序可以配置使用 CMake 构建系统的项目。使用 C/C++: 更改配置提供程序... 命令以启用任何此类扩展程序，以便为 IntelliSense 提供配置。

A third option for projects without build system extension support is to use a [compile_commands.json](https://clang.llvm.org/docs/JSONCompilationDatabase.html) file if your build system supports generating this file. In the "Advanced" section of the Configuration UI, you can supply the path to your `compile_commands.json` and the extension will use the compilation information listed in that file to configure IntelliSense.

​​​	对于不支持构建系统扩展的项目，第三种选择是使用 compile_commands.json 文件，如果您的构建系统支持生成此文件。在配置 UI 的“高级”部分，您可以提供 `compile_commands.json` 的路径，扩展程序将使用该文件中列出的编译信息来配置 IntelliSense。

**Note:** If the extension is unable to resolve any of the `#include` directives in your source code, it will not show linting information for the body of the source file. If you check the **Problems** window in VS Code, the extension will provide more information about which files it was unable to locate. If you want to show the linting information anyway, you can change the value of the `C_Cpp.errorSquiggles` setting.

​​​	注意：如果扩展程序无法解析源代码中的任何 `#include` 指令，它将不会显示源文件正文的 linting 信息。如果您检查 VS Code 中的问题窗口，扩展程序将提供有关它无法找到哪些文件的更多信息。如果您仍想显示 linting 信息，可以更改 `C_Cpp.errorSquiggles` 设置的值。

## [What is the difference between includePath and browse.path? includePath 和 browse.path 有什么区别？](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-is-the-difference-between-includepath-and-browsepath)

These two settings are available in `c_cpp_properties.json` and can be confusing.

​​​	这两个设置在 `c_cpp_properties.json` 中可用，可能会令人困惑。

### [includePath](https://code.visualstudio.com/docs/cpp/faq-cpp#_includepath)

This array of path strings is used by the "Default" IntelliSense engine, which provides semantic-aware IntelliSense features. The include paths are the same paths that you would send to your compiler via the `-I` switch. When your source files are parsed, the IntelliSense engine will prepend these paths to the files specified by your #include directives while attempting to resolve them. These paths are **not** searched recursively unless they end with `/**`.

​​​	“默认”IntelliSense 引擎使用此路径字符串数组，该引擎提供语义感知 IntelliSense 功能。包含路径与您通过 `-I` 开关发送给编译器的路径相同。解析源文件时，IntelliSense 引擎会在尝试解析 #include 指令指定的文件时将这些路径预置于这些文件之前。除非路径以 `/**` 结尾，否则不会递归搜索这些路径。

### [browse.path](https://code.visualstudio.com/docs/cpp/faq-cpp#_browsepath)

This array of path strings is used by the "Tag Parser" ("browse engine"), which populates a database with global symbol information. This engine will **recursively** enumerate all files under the paths specified and track them as potential includes while tag parsing your project folder. To disable recursive enumeration of a path, you can append a `/*` to the path string.

​​​	“标记解析器”（“浏览引擎”）使用此路径字符串数组，该引擎使用全局符号信息填充数据库。此引擎将在指定路径下的所有文件下递归枚举所有文件，并在标记解析项目文件夹时将它们作为潜在的包含项进行跟踪。若要禁用路径的递归枚举，可以将 `/*` 追加到路径字符串。

When you open a workspace for the first time, the extension adds `${workspaceFolder}/**` to the `includePath` and the `browse.path` is left undefined (so it defaults to the `includePath`). If this is undesirable, you can open your **c_cpp_properties.json** file and change it.

​​​	首次打开工作区时，扩展会将 `${workspaceFolder}/**` 添加到 `includePath` 中，而 `browse.path` 保持未定义状态（因此它默认为 `includePath` ）。如果这不可取，可以打开 c_cpp_properties.json 文件并对其进行更改。

## [Why do I see red squiggles under Standard Library types? 为什么在标准库类型下看到红色波浪线？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-do-i-see-red-squiggles-under-standard-library-types)

The most common reason for this is missing include paths and defines. The easiest way to fix this is to set `compilerPath` in **c_cpp_properties.json** to the path to your compiler.

​​​	最常见的原因是缺少 include 路径和定义。最简单的修复方法是在 c_cpp_properties.json 中将 `compilerPath` 设置为编译器的路径。

## [How do I get the new IntelliSense to work with MinGW on Windows? 如何在 Windows 上使用 MinGW 使新的 IntelliSense 生效？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-the-new-intellisense-to-work-with-mingw-on-windows)

See [Get Started with C++ and Mingw-w64 in Visual Studio Code](https://code.visualstudio.com/docs/cpp/config-mingw).

​​​	请参阅在 Visual Studio Code 中开始使用 C++ 和 Mingw-w64。

## [How do I get the new IntelliSense to work with the Windows Subsystem for Linux? 如何在 Windows 子系统中使用 Linux 使新的 IntelliSense 生效？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-get-the-new-intellisense-to-work-with-the-windows-subsystem-for-linux)

See [Get Started with C++ and Windows Subsystem for Linux in Visual Studio Code](https://code.visualstudio.com/docs/cpp/config-wsl).

​​​	请参阅在 Visual Studio Code 中开始使用 C++ 和 Windows 子系统 for Linux。

## [Why are my files corrupted on format? 为什么我的文件在格式化时损坏？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-are-my-files-corrupted-on-format)

Files can be corrupted (and other features can fail) if a workspace folder is opened via a path with symlinks (issue [vscode-cpptools#5061](https://github.com/microsoft/vscode-cpptools/issues/5061)). The workaround is to open the workspace folder using a path that has the symlinks resolved to their target.

​​​	如果工作区文件夹是通过带有符号链接的路径打开的，则文件可能会损坏（其他功能也可能会失败）（问题 vscode-cpptools#5061）。解决方法是使用已将符号链接解析为其目标的路径打开工作区文件夹。

## [How do I recreate the IntelliSense database? 如何重新创建 IntelliSense 数据库？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-recreate-the-intellisense-database)

Starting in version 0.12.3 of the extension, there is a command to reset your IntelliSense database. Open the Command Palette (Ctrl+Shift+P) and choose the **C/C++: Reset IntelliSense Database** command.

​​​	从扩展的 0.12.3 版本开始，有一个命令可以重置 IntelliSense 数据库。打开命令面板 (Ctrl+Shift+P)，然后选择 C/C++: 重置 IntelliSense 数据库命令。

## [What is the ipch folder? ipch 文件夹是什么？](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-is-the-ipch-folder)

The language server caches information about included header files to improve the performance of IntelliSense. When you edit C/C++ files in your workspace folder, the language server will store cache files in the `ipch` folder. By default, the `ipch` folder is stored under the user directory. Specifically, it is stored under `%LocalAppData%/Microsoft/vscode-cpptools` on Windows, `$XDG_CACHE_HOME/vscode-cpptools/` on Linux (or `$HOME/.cache/vscode-cpptools/` if `XDG_CACHE_HOME` is not defined), and `$HOME/Library/Caches/vscode-cpptools/` on macOS. By using the user directory as the default path, it will create one cache location per user for the extension. As the cache size limit is applied to a cache location, having one cache location per user will limit the disk space usage of the cache to that one folder for everyone using the default setting value.

​​​	语言服务器会缓存有关包含的头文件的信息，以提高 IntelliSense 的性能。当您编辑工作区文件夹中的 C/C++ 文件时，语言服务器会将缓存文件存储在 `ipch` 文件夹中。默认情况下， `ipch` 文件夹存储在用户目录下。具体来说，它存储在 Windows 上的 `%LocalAppData%/Microsoft/vscode-cpptools` 、Linux 上的 `$XDG_CACHE_HOME/vscode-cpptools/` （如果未定义 `XDG_CACHE_HOME` ，则为 `$HOME/.cache/vscode-cpptools/` ）和 macOS 上的 `$HOME/Library/Caches/vscode-cpptools/` 下。通过将用户目录用作默认路径，它将为扩展创建每个用户的缓存位置。由于缓存大小限制应用于缓存位置，因此每个用户有一个缓存位置会将缓存的磁盘空间使用情况限制在使用默认设置值的所有人的一个文件夹中。

VS Code per-workspace storage folders were not used because the location provided by VS Code is not well known and we didn't want to write GB's of files where users may not see them or know where to find them.

​​​	未使用 VS Code 每个工作区存储文件夹，因为 VS Code 提供的位置不为人所知，我们不想在用户可能看不到或不知道在哪里找到它们的位置写入 GB 的文件。

With this in mind, we knew that we would not be able to meet the needs of every different development environment, so we provided settings to allow you to customize the way that works best for your situation.

​​​	考虑到这一点，我们知道我们无法满足每个不同开发环境的需求，因此我们提供了设置，允许您自定义最适合您情况的方式。

### ["C_Cpp.intelliSenseCachePath":  “C_Cpp.intelliSenseCachePath”：](https://code.visualstudio.com/docs/cpp/faq-cpp#_ccppintellisensecachepath-string)

This setting allows you to set workspace or global overrides for the cache path. For example, if you want to share a single cache location for all workspace folders, open the VS Code settings, and add a User setting for **IntelliSense Cache Path**.

​​​	此设置允许您为缓存路径设置工作区或全局覆盖。例如，如果您想为所有工作区文件夹共享一个缓存位置，请打开 VS Code 设置，并为 IntelliSense 缓存路径添加用户设置。

### ["C_Cpp.intelliSenseCacheSize":  “C_Cpp.intelliSenseCacheSize”：](https://code.visualstudio.com/docs/cpp/faq-cpp#_ccppintellisensecachesize-number)

This setting allows you to set a limit on the amount of caching the extension does. This is an approximation, but the extension will make a best effort to keep the cache size as close to the limit you set as possible. If you are sharing the cache location across workspaces as explained above, you can still increase/decrease the limit, but you should make sure that you add a User setting for **IntelliSense Cache Size**.

​​​	此设置允许您对扩展程序执行的缓存量设置限制。这是一个近似值，但扩展程序会尽最大努力使缓存大小尽可能接近您设置的限制。如果您按照上述说明在工作区之间共享缓存位置，您仍然可以增加/减少限制，但您应该确保为 IntelliSense 缓存大小添加用户设置。

## [How do I disable the IntelliSense cache (ipch)? 如何禁用 IntelliSense 缓存 (ipch)？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-disable-the-intellisense-cache-ipch)

If you do not want to use the IntelliSense caching feature (such as to work around a bug that may only occur when the cache is enabled), you can disable the feature by setting the **IntelliSense Cache Size** setting to 0 (or `"C_Cpp.intelliSenseCacheSize": 0"` in the JSON settings editor). Disabling the cache may also be beneficial if you're seeing excessive disk writing, particularly when editing headers.

​​​	如果您不想使用 IntelliSense 缓存功能（例如，为了解决仅在启用缓存时才会出现的错误），您可以通过将 IntelliSense 缓存大小设置设置为 0（或在 JSON 设置编辑器中设置为 `"C_Cpp.intelliSenseCacheSize": 0"` ）来禁用该功能。如果您看到过多的磁盘写入，尤其是在编辑头文件时，禁用缓存也可能会有帮助。

## [How do I set up debugging? 如何设置调试？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-set-up-debugging)

The debugger needs to be configured to know which executable and debugger to use:

​​​	调试器需要配置为知道要使用哪个可执行文件和调试器：

From the main menu, select **Run** > **Add Configuration...**.

​​​	从主菜单中，选择运行 > 添加配置....

The file `launch.json` will now be open for editing with a new configuration. The default settings will *probably* work except that you need to specify the `program` setting.

​​​	现在将使用新配置打开文件 `launch.json` 进行编辑。默认设置可能会起作用，但您需要指定 `program` 设置。

See [Configure C/C++ debugging](https://code.visualstudio.com/docs/cpp/launch-json-reference) for more in-depth documentation on how to configure the debugger.

​​​	有关如何配置调试器的更深入文档，请参阅配置 C/C++ 调试。

## [How do I enable debug symbols? 如何启用调试符号？](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-enable-debug-symbols)

Enabling debug symbols is dependent on the type of compiler you are using. Below are some of the compilers and the compiler options necessary to enable debug symbols.

​​​	启用调试符号取决于您使用的编译器类型。以下是启用调试符号所需的一些编译器和编译器选项。

When in doubt, please check your compiler's documentation for the options necessary to include debug symbols in the output. This may be some variant of `-g` or `--debug`.

​​​	如有疑问，请查看编译器的文档，了解在输出中包含调试符号所需的选项。这可能是 `-g` 或 `--debug` 的某个变体。

### [Clang (C++)](https://code.visualstudio.com/docs/cpp/faq-cpp#_clang-c)

- If you invoke the compiler manually, add the `--debug` option.
  如果您手动调用编译器，请添加 `--debug` 选项。
- If you're using a script, make sure the `CXXFLAGS` environment variable is set. For example, `export CXXFLAGS="${CXXFLAGS} --debug"`.
  如果您使用的是脚本，请确保设置了 `CXXFLAGS` 环境变量。例如， `export CXXFLAGS="${CXXFLAGS} --debug"` 。
- If you're using CMake, make sure the `CMAKE_CXX_FLAGS` is set. For example, `export CMAKE_CXX_FLAGS=${CXXFLAGS}`.
  如果您使用的是 CMake，请确保设置了 `CMAKE_CXX_FLAGS` 。例如， `export CMAKE_CXX_FLAGS=${CXXFLAGS}` 。

### [Clang (C)](https://code.visualstudio.com/docs/cpp/faq-cpp#_clang-c)

See Clang C++ but use `CFLAGS` instead of `CXXFLAGS`.

​​​	请参阅 Clang C++，但使用 `CFLAGS` 代替 `CXXFLAGS` 。

### [gcc or g++ gcc 或 g++](https://code.visualstudio.com/docs/cpp/faq-cpp#_gcc-or-g)

If you invoke the compiler manually, add the `-g` option.

​​​	如果您手动调用编译器，请添加 `-g` 选项。

### [cl.exe](https://code.visualstudio.com/docs/cpp/faq-cpp#_clexe)

Symbols are located in the `*.pdb` file.

​​​	符号位于 `*.pdb` 文件中。

## [Why is debugging not working? 为什么调试不起作用？](https://code.visualstudio.com/docs/cpp/faq-cpp#_why-is-debugging-not-working)

### [My breakpoints aren't being hit 我的断点没有被命中](https://code.visualstudio.com/docs/cpp/faq-cpp#_my-breakpoints-arent-being-hit)

When you start debugging, if your breakpoints aren't bound (solid red circle) or they are not being hit, you may need to enable [debug symbols](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-enable-debug-symbols) during compilation.

​​​	当您开始调试时，如果您的断点未绑定（实心红圈）或未被命中，您可能需要在编译期间启用调试符号。

### [Debugging starts but all the lines in my stack trace are grey 调试已启动，但堆栈跟踪中的所有行都是灰色的](https://code.visualstudio.com/docs/cpp/faq-cpp#_debugging-starts-but-all-the-lines-in-my-stack-trace-are-grey)

If your debugger is showing a grey stack trace, won't stop at a breakpoint, or the symbols in the call stack are grey, then your executable was compiled without [debug symbols](https://code.visualstudio.com/docs/cpp/faq-cpp#_how-do-i-enable-debug-symbols).

​​​	如果你的调试器显示灰色的堆栈跟踪，不会在断点处停止，或者调用堆栈中的符号是灰色的，那么你的可执行文件是在没有调试符号的情况下编译的。

## [What do I do if I suspect a C/C++ extension problem 如果我怀疑是 C/C++ 扩展问题，我该怎么办](https://code.visualstudio.com/docs/cpp/faq-cpp#_what-do-i-do-if-i-suspect-a-cc-extension-problem)

If you have any other questions, please start a discussion at [GitHub discussions](https://github.com/microsoft/vscode-cpptools/discussions), or if you find an issue that needs to be fixed, file an issue at [GitHub issues](https://github.com/microsoft/vscode-cpptools/issues).

​​​	如果你还有其他问题，请在 GitHub 讨论中发起讨论，或者如果你发现需要修复的问题，请在 GitHub 问题中提交问题。

If you are experiencing a problem with the extension that we can't diagnose based on information in your issue report, we might ask you to enable debug logging and send us your logs. See [C/C++ extension logging](https://code.visualstudio.com/docs/cpp/enable-logging-cpp) for how to get C/C++ extension logs.

​​​	如果你遇到我们无法根据问题报告中的信息诊断的扩展问题，我们可能会要求你启用调试日志并向我们发送你的日志。请参阅 C/C++ 扩展日志了解如何获取 C/C++ 扩展日志。
