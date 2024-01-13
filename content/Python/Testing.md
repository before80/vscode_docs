+++
title = "Testing"
date = 2024-01-12T22:36:24+08:00
weight = 60
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/python/testing](https://code.visualstudio.com/docs/python/testing)

# Python testing in Visual Studio Code Visual Studio Code 中的 Python 测试



The [Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python) supports testing with Python's built-in [unittest](https://docs.python.org/3/library/unittest.html) framework and [pytest](https://docs.pytest.org/).

&zeroWidthSpace;Python 扩展支持使用 Python 的内置 unittest 框架和 pytest 进行测试。

## [A little background on unit testing 单元测试的背景知识](https://code.visualstudio.com/docs/python/testing#_a-little-background-on-unit-testing)

(If you're already familiar with unit testing, you can skip to the [walkthroughs](https://code.visualstudio.com/docs/python/testing#_example-test-walkthroughs).)

&zeroWidthSpace;（如果您已经熟悉单元测试，可以跳过演练。）

A **unit** is a specific piece of code to be tested, such as a function or a class. **Unit tests** are then other pieces of code that specifically exercise the code unit with a full range of different inputs, including boundary and edge cases. Both the unittest and pytest frameworks can be used to write unit tests.

&zeroWidthSpace;单元是待测试的特定代码片段，例如函数或类。然后，单元测试是其他代码片段，它们使用各种不同的输入（包括边界和边缘情况）专门演练代码单元。unittest 和 pytest 框架都可以用于编写单元测试。

For example, say you have a function to validate the format of an account number that a user enters in a web form:

&zeroWidthSpace;例如，假设您有一个函数来验证用户在网络表单中输入的帐号格式：

```
def validate_account_number_format(account_string):
    # Return False if invalid, True if valid
    # ...
```

Unit tests are concerned only with the unit's **interface**—its arguments and return values—not with its implementation (which is why no code is shown here in the function body; often you'd be using other well-tested libraries to help implement the function). In this example, the function accepts any string and returns true if that string contains a properly formatted account number, false otherwise.

&zeroWidthSpace;单元测试只关注单元的接口——其参数和返回值——而不关注其实现（这就是为什么此处函数体中未显示任何代码；通常您会使用其他经过良好测试的库来帮助实现该函数）。在此示例中，该函数接受任何字符串，如果该字符串包含格式正确的帐号，则返回 true，否则返回 false。

To thoroughly test this function, you want to throw at it every conceivable input: valid strings, mistyped strings (off by one or two characters, or containing invalid characters), strings that are too short or too long, blank strings, null arguments, strings containing control characters (non-text codes), string containing HTML, strings containing injection attacks (such as SQL commands or JavaScript code), and so on. It's especially important to test security cases like injection attacks if the validated string is later used in database queries or displayed in the app's UI.

&zeroWidthSpace;为了彻底测试此功能，您需要向其抛出所有可以想象的输入：有效字符串、键入错误的字符串（差一个或两个字符，或包含无效字符）、太短或太长的字符串、空字符串、空参数、包含控制字符（非文本代码）的字符串、包含 HTML 的字符串、包含注入攻击（例如 SQL 命令或 JavaScript 代码）的字符串，等等。如果经过验证的字符串稍后用于数据库查询或显示在应用程序的 UI 中，则测试注入攻击等安全案例尤其重要。

For each input, you then define the function's expected return value (or values). In this example, again, the function should return true for only properly formatted strings. (Whether the number itself is a real account is a different matter that would be handled elsewhere through a database query.)

&zeroWidthSpace;对于每个输入，您随后定义函数的预期返回值（或值）。在此示例中，该函数应仅对格式正确的字符串返回 true。（数字本身是否为真实帐户是另一回事，将在其他地方通过数据库查询进行处理。）

With all the arguments and expected return values in hand, you now write the tests themselves, which are pieces of code that call the function with a particular input, then compare the actual return value with the expected return value (this comparison is called an **assertion**):

&zeroWidthSpace;掌握所有参数和预期返回值后，您现在编写测试本身，这些测试是使用特定输入调用函数的代码片段，然后将实际返回值与预期返回值进行比较（此比较称为断言）：

```
# Import the code to be tested
import validator

# Import the test framework (this is a hypothetical module)
import test_framework

# This is a generalized example, not specific to a test framework
class Test_TestAccountValidator(test_framework.TestBaseClass):
    def test_validator_valid_string():
        # The exact assertion call depends on the framework as well
        assert(validate_account_number_format("1234567890"), True)

    # ...

    def test_validator_blank_string():
        # The exact assertion call depends on the framework as well
        assert(validate_account_number_format(""), False)

    # ...

    def test_validator_sql_injection():
        # The exact assertion call depends on the framework as well
        assert(validate_account_number_format("drop database master"), False)

    # ... tests for all other cases
```

The exact structure of the code depends on the test framework you're using, and specific examples are provided later in this article. In any case, as you can see, each test is simple: invoke the function with an argument and assert the expected return value.

&zeroWidthSpace;代码的确切结构取决于您使用的测试框架，本文后面提供了具体示例。无论如何，正如您所见，每个测试都很简单：使用参数调用函数并断言预期的返回值。

The combined results of all the tests is your test report, which tells you whether the function (the unit), is behaving as expected across all test cases. That is, when a unit passes all of its tests, you can be confident that it's functioning properly. (The practice of **test-driven development** is where you actually write the tests first, then write the code to pass increasingly more tests until all of them pass.)

&zeroWidthSpace;所有测试的综合结果就是您的测试报告，它会告诉您函数（单元）是否在所有测试用例中按预期运行。也就是说，当一个单元通过所有测试时，您可以确信它运行正常。（测试驱动的开发实践是您实际上先编写测试，然后编写代码以通过越来越多的测试，直到所有测试都通过。）

Because unit tests are small, isolated pieces of code (in unit testing you avoid external dependencies and use mock data or otherwise simulated inputs), they're quick and inexpensive to run. This characteristic means that you can run unit tests early and often. Developers typically run unit tests even before committing code to a repository; gated check-in systems can also run unit tests before merging a commit. Many continuous integration systems also run unit tests after every build. Running the unit test early and often means that you quickly catch **regressions,** which are unexpected changes in the behavior of code that previously passed all its unit tests. Because the test failure can easily be traced to a particular code change, it's easy to find and remedy the cause of the failure, which is undoubtedly better than discovering a problem much later in the process!

&zeroWidthSpace;由于单元测试是代码中独立的小片段（在单元测试中，您避免外部依赖关系并使用模拟数据或其他模拟输入），因此运行起来快速且成本低廉。此特性意味着您可以尽早且频繁地运行单元测试。开发人员通常在将代码提交到存储库之前运行单元测试；受控签入系统还可以在合并提交之前运行单元测试。许多持续集成系统还会在每次构建后运行单元测试。尽早且频繁地运行单元测试意味着您可以快速捕获回归，回归是先前通过所有单元测试的代码行为的意外更改。由于测试失败可以很容易地追溯到特定的代码更改，因此很容易找到并补救失败的原因，这无疑比在流程的后期发现问题要好得多！

For a general background on unit testing, read [Unit testing](https://wikipedia.org/wiki/Unit_testing) on Wikipedia. For useful unit test examples, you can review https://github.com/gwtw/py-sorting, a repository with tests for different sorting algorithms.

&zeroWidthSpace;有关单元测试的一般背景信息，请阅读维基百科上的单元测试。有关有用的单元测试示例，您可以查看 https://github.com/gwtw/py-sorting，这是一个包含不同排序算法测试的存储库。

## [Example test walkthroughs 示例测试演练](https://code.visualstudio.com/docs/python/testing#_example-test-walkthroughs)

Python tests are Python classes that reside in separate files from the code being tested. Each test framework specifies the structure and naming of tests and test files. Once you write tests and enable a test framework, VS Code locates those tests and provides you with various commands to run and debug them.

&zeroWidthSpace;Python 测试是 Python 类，它位于与被测代码不同的文件中。每个测试框架都指定测试和测试文件的结构和命名。编写测试并启用测试框架后，VS Code 会找到这些测试并为你提供各种命令来运行和调试它们。

For this section, create a folder and open it in VS Code. Then create a file named `inc_dec.py` with the following code to be tested:

&zeroWidthSpace;对于本部分，创建一个文件夹并在 VS Code 中将其打开。然后创建一个名为 `inc_dec.py` 的文件，其中包含要测试的以下代码：

```
def increment(x):
    return x + 1

def decrement(x):
    return x - 1
```

With this code, you can experience working with tests in VS Code as described in the sections that follow.

&zeroWidthSpace;使用此代码，你可以体验在 VS Code 中使用测试，如以下部分所述。

## [Configure tests 配置测试](https://code.visualstudio.com/docs/python/testing#_configure-tests)

Once you have the Python extension installed and a Python file open within the editor, a test beaker icon will be displayed on the VS Code Activity bar. The beaker icon is for the **Test Explorer** view. When opening the Test Explorer, you will see a **Configure Tests** button if you don't have a test framework enabled. Once you select **Configure Tests**, you will be prompted to select a test framework and a folder containing the tests. If you're using unittest, you will also be asked to select the file glob pattern used to identify your test files.

&zeroWidthSpace;安装 Python 扩展并在编辑器中打开 Python 文件后，VS Code 活动栏中将显示一个测试烧杯图标。烧杯图标用于测试资源管理器视图。打开测试资源管理器时，如果你没有启用测试框架，将看到一个“配置测试”按钮。选择“配置测试”后，系统将提示你选择一个测试框架和一个包含测试的文件夹。如果你使用 unittest，系统还会要求你选择用于标识测试文件的 glob 文件模式。

> **Note**: A file glob pattern is a defined string pattern that matches file or folder names based on wildcards to then include or not include.
>
> &zeroWidthSpace;注意：文件 glob 模式是一种定义的字符串模式，它根据通配符匹配文件或文件夹名称，然后包含或不包含。

![Configure Python Tests button displayed in the Test Explorer when tests haven't been configured.](https://code.visualstudio.com/assets/docs/python/testing/test-explorer-no-tests.png)

You can configure your tests anytime by using the **Python: Configure Tests** command from the [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette). You can also configure testing manually by setting either `python.testing.unittestEnabled` or `python.testing.pytestEnabled`, which can be done either in the Settings editor or in the `settings.json` file as described in the VS Code [Settings](https://code.visualstudio.com/docs/getstarted/settings) documentation. Each framework also has specific configuration settings as described under [Test configuration settings](https://code.visualstudio.com/docs/python/testing#_test-configuration-settings) for their folders and patterns.

&zeroWidthSpace;您可以随时使用命令面板中的 Python：配置测试命令来配置测试。您还可以通过设置 `python.testing.unittestEnabled` 或 `python.testing.pytestEnabled` 来手动配置测试，这可以在设置编辑器中或 `settings.json` 文件中完成，如 VS Code 设置文档中所述。每个框架还具有特定配置设置，如其文件夹和模式的测试配置设置中所述。

If both frameworks are enabled, then the Python extension will only run `pytest`.

&zeroWidthSpace;如果启用这两个框架，那么 Python 扩展程序将只运行 `pytest` 。

If you enable pytest, VS Code prompts you to install the framework package if it's not already present in the currently activated environment:

&zeroWidthSpace;如果您启用 pytest，VS Code 会提示您安装框架包（如果它尚未在当前激活的环境中存在）：

![VS Code prompt to install a test framework when enabled](https://code.visualstudio.com/assets/docs/python/testing/install-framework.png)

## [Create tests 创建测试](https://code.visualstudio.com/docs/python/testing#_create-tests)

Each test framework has its own conventions for naming test files and structuring the tests within, as described in the following sections. Each case includes two test methods, one of which is intentionally set to fail for the purposes of demonstration.

&zeroWidthSpace;每个测试框架都有自己的命名测试文件和构建内部测试的约定，如下文所述。每种情况包括两种测试方法，其中一种方法故意设置为失败以进行演示。

### [Tests in unittest unittest 中的测试](https://code.visualstudio.com/docs/python/testing#_tests-in-unittest)

Create a file named `test_unittest.py` that contains a test class with two test methods:

&zeroWidthSpace;创建一个名为 `test_unittest.py` 的文件，其中包含一个具有两种测试方法的测试类：

```
import inc_dec    # The code to test
import unittest   # The test framework

class Test_TestIncrementDecrement(unittest.TestCase):
    def test_increment(self):
        self.assertEqual(inc_dec.increment(3), 4)

    # This test is designed to fail for demonstration purposes.
    def test_decrement(self):
        self.assertEqual(inc_dec.decrement(3), 4)

if __name__ == '__main__':
    unittest.main()
```

### [Tests in pytest pytest 中的测试](https://code.visualstudio.com/docs/python/testing#_tests-in-pytest)

Create a file named `test_pytest.py` that contains two test methods:

&zeroWidthSpace;创建一个名为 `test_pytest.py` 的文件，其中包含两个测试方法：

```
import inc_dec    # The code to test

def test_increment():
    assert inc_dec.increment(3) == 4

# This test is designed to fail for demonstration purposes.
def test_decrement():
    assert inc_dec.decrement(3) == 4
```

## [Test discovery 测试发现](https://code.visualstudio.com/docs/python/testing#_test-discovery)

By default, the Python extension attempts to discover tests once you enable a framework. You can also trigger test discovery at any time using the **Test: Refresh Tests** command from the Command Palette.

&zeroWidthSpace;默认情况下，一旦启用框架，Python 扩展将尝试发现测试。您还可以随时使用命令面板中的“测试：刷新测试”命令触发测试发现。

`python.testing.autoTestDiscoverOnSaveEnabled` is set to `true` by default, meaning that test discovery is also performed automatically whenever you add, delete, or update any Python file in the workspace. To disable this feature, set the value to `false`, which can be done either in the Settings editor or in the `settings.json` file as described in the VS Code [Settings](https://code.visualstudio.com/docs/getstarted/settings) documentation. You will need to reload the window for this setting to take effect.

&zeroWidthSpace; `python.testing.autoTestDiscoverOnSaveEnabled` 默认设置为 `true` ，这意味着每当您在工作区中添加、删除或更新任何 Python 文件时，也会自动执行测试发现。要禁用此功能，请将值设置为 `false` ，可以在“设置”编辑器中或 `settings.json` 文件中执行此操作，如 VS Code 设置文档中所述。您需要重新加载窗口才能使此设置生效。

Test discovery applies the discovery patterns for the current framework (which can be customized using the [Test configuration settings](https://code.visualstudio.com/docs/python/testing#_test-configuration-settings)). The default behavior is as follows:

&zeroWidthSpace;测试发现应用当前框架的发现模式（可以使用测试配置设置进行自定义）。默认行为如下：

- `python.testing.unittestArgs`: Looks for any Python (`.py`) file with "test" in the name in the top-level project folder. All test files must be importable modules or packages. You can customize the file matching pattern with the `-p` configuration setting, and customize the folder with the `-t` setting.

  &zeroWidthSpace; `python.testing.unittestArgs` ：在顶级项目文件夹中查找名称中包含“test”的任何 Python（ `.py` ）文件。所有测试文件都必须是可导入的模块或包。您可以使用 `-p` 配置设置自定义文件匹配模式，并使用 `-t` 设置自定义文件夹。

- `python.testing.pytestArgs`: Looks for any Python (`.py`) file whose name begins with "test_" or ends with "_test", located anywhere within the current folder and all subfolders.

  &zeroWidthSpace; `python.testing.pytestArgs` ：查找名称以“test_”开头或以“_test”结尾的任何 Python（ `.py` ）文件，该文件位于当前文件夹和所有子文件夹中的任何位置。

> **Tip**: Sometimes tests placed in subfolders aren't discovered because such test files cannot be imported. To make them importable, create an empty file named `__init__.py` in that folder.
>
> &zeroWidthSpace;提示：有时放在子文件夹中的测试不会被发现，因为无法导入此类测试文件。要使其可导入，请在该文件夹中创建一个名为 `__init__.py` 的空文件。

If the test discovery succeeds, you'll see tests listed in the Test Explorer:

&zeroWidthSpace;如果测试发现成功，您将在测试资源管理器中看到列出的测试：

![The VS Code Test Explorer for Python tests](https://code.visualstudio.com/assets/docs/python/testing/test-explorer.png)

If discovery fails (for example, the test framework isn't installed or you have a syntax error in your test file), you'll see an error message displayed in the Test Explorer. You can check the **Python** output panel to see the entire error message (use the **View** > **Output** menu command to show the **Output** panel, then select **Python** from the dropdown on the right side).

&zeroWidthSpace;如果发现失败（例如，未安装测试框架或测试文件中存在语法错误），您将在测试资源管理器中看到一条错误消息。您可以检查 Python 输出面板以查看整个错误消息（使用“视图”>“输出”菜单命令显示“输出”面板，然后从右侧的下拉菜单中选择“Python”）。

![Discovery failure error messaged displayed in the Test Explorer](https://code.visualstudio.com/assets/docs/python/testing/test-discovery-error.png)

Once VS Code recognizes tests, it provides several ways to run those tests as described in [Run tests](https://code.visualstudio.com/docs/python/testing#_run-tests).

&zeroWidthSpace;一旦 VS Code 识别出测试，它就会提供多种方法来运行这些测试，如在运行测试中所述。

## [Run tests 运行测试](https://code.visualstudio.com/docs/python/testing#_run-tests)

You can run tests using any of the following actions:

&zeroWidthSpace;您可以使用以下任何操作来运行测试：

- With a test file open, select the green run icon that is displayed in the gutter next to the test definition line, as shown in the previous section. This command runs only that one method.

  &zeroWidthSpace;打开测试文件后，选择上一部分中所示的测试定义行旁边显示在边距中的绿色运行图标。此命令仅运行该一个方法。

  ![Run test icon displayed on the gutter when the test file is open in the editor](https://code.visualstudio.com/assets/docs/python/testing/run-tests-gutter.png)

- From the **Command Palette**, by running any of the following commands:

  &zeroWidthSpace;通过运行以下任一命令，从命令面板中：

  - **Test: Run All Tests** - Runs all tests that have been discovered.
    测试：运行所有测试 - 运行已发现的所有测试。
  - **Test: Run Tests in Current File** - Runs all tests in a file that that is open in the editor.
    测试：运行当前文件中的测试 - 运行编辑器中打开的文件中的所有测试。
  - **Test: Run Test at Cursor** - Runs only the test method under your cursor in the editor.
    测试：运行光标处的测试 - 仅运行编辑器中光标下的测试方法。

- From the **Test Explorer**:

  &zeroWidthSpace;从测试资源管理器中：

  - To run all discovered tests, select the play button at the top of **Test Explorer**:

    &zeroWidthSpace;要运行所有已发现的测试，请选择测试资源管理器顶部的播放按钮：

    ![Running all tests through Test Explorer](https://code.visualstudio.com/assets/docs/python/testing/test-explorer-run-all-tests.png)

  - To run a specific group of tests, or a single test, select the file, class, or test, then select the play button to the right of that item:

    &zeroWidthSpace;要运行特定组的测试或单个测试，请选择文件、类或测试，然后选择该项右侧的播放按钮：

    ![Running tests at specific scopes through Test Explorer](https://code.visualstudio.com/assets/docs/python/testing/test-explorer-run-scoped-tests.png)

  - You can also run a selection of tests through the Test Explorer. To do that, Ctrl+Click (or Cmd+Click on macOS) on the tests you wish to run, right-click on one of them and then select **Run Test**.

    &zeroWidthSpace;您还可以通过测试资源管理器运行选定的测试。为此，请按住 Ctrl 键单击（或在 macOS 上按住 Cmd 键单击）要运行的测试，右键单击其中一个测试，然后选择“运行测试”。

After a test run, VS Code displays results directly in the editor as gutter decorations. Failed tests will also be highlighted in the editor, with a Peek View that displays the test run error message and a history of all of the tests' runs. You can press Escape to dismiss the view, and you can disable it by opening the User settings (**Preferences: Open Settings (UI)** command in the **Command Palette**) and changing the value of the **Testing: Automatically Open Peek View** setting to `never`.

&zeroWidthSpace;经过测试运行后，VS Code 会将结果直接显示在编辑器中，作为间距修饰。失败的测试也会在编辑器中突出显示，并带有显示测试运行错误消息和所有测试运行历史记录的 Peek 视图。您可以按 Escape 键关闭视图，也可以通过打开用户设置（首选项：在命令面板中打开设置（UI）命令）并更改测试的值：自动打开 Peek 视图设置到 `never` 来禁用它。

In the **Test Explorer**, results are shown for individual tests and any classes and files containing those tests. Folders will display a failure icon if any of the tests within that folder did not pass.

&zeroWidthSpace;在测试资源管理器中，结果会显示为各个测试以及包含这些测试的任何类和文件。如果该文件夹中的任何测试未通过，则该文件夹将显示一个失败图标。

![Test results on a unittest class and in Test Explorer](https://code.visualstudio.com/assets/docs/python/testing/test-results.png)

VS Code also shows test results in the **Python Test Log** output panel.

&zeroWidthSpace;VS Code 还会在 Python 测试日志输出面板中显示测试结果。

![Test results in the Python Test Log output panel](https://code.visualstudio.com/assets/docs/python/testing/python-test-log-output.png)

## [Run tests in parallel 并行运行测试](https://code.visualstudio.com/docs/python/testing#_run-tests-in-parallel)

Support for running tests in parallel with pytest is available through the `pytest-xdist` package. To enable parallel testing:

&zeroWidthSpace;通过 `pytest-xdist` 包支持并行运行 pytest 中的测试。若要启用并行测试：

1. Open the integrated terminal and install the `pytest-xdist` package. For more details, refer to the [project's documentation page](https://pypi.org/project/pytest-xdist/).

   &zeroWidthSpace;打开集成终端并安装 `pytest-xdist` 包。有关更多详细信息，请参阅项目的文档页面。

   **For Windows
   适用于 Windows**

   ```
   py -3 -m pip install pytest-xdist
   ```

   **For macOS/Linux
   适用于 macOS/Linux**

   ```
   python3 -m pip install pytest-xdist
   ```

2. Next, create a file named `pytest.ini` in your project directory and add the content below, specifying the number of CPUs to be used. For example, to set it up for 4 CPUs:

   &zeroWidthSpace;接下来，在项目目录中创建一个名为 `pytest.ini` 的文件，并添加以下内容，指定要使用的 CPU 数量。例如，要将其设置为 4 个 CPU：

   ```
    [pytest]
    addopts=-n4
   ```

   Or, if you are using a `pyproject.toml` file

   &zeroWidthSpace;或者，如果您使用的是 `pyproject.toml` 文件

   ```
    [tool.pytest.ini_options]
    addopts="-n 4"
   ```

3. Run your tests, which will now be run in parallel.

   &zeroWidthSpace;运行测试，现在将并行运行这些测试。

## [Debug tests 调试测试](https://code.visualstudio.com/docs/python/testing#_debug-tests)

You might occasionally need to step through and analyze tests in the debugger, either because the tests themselves have a code defect you need to track down or in order to better understand why an area of code being tested is failing. For more information on debugging or to understand how it works in VS Code, you can read the [Python debugging configurations](https://code.visualstudio.com/docs/python/debugging) and general VS Code [Debugging](https://code.visualstudio.com/docs/editor/debugging) articles.

&zeroWidthSpace;您可能偶尔需要在调试器中逐步执行并分析测试，原因可能是测试本身存在您需要跟踪的代码缺陷，或者为了更好地理解正在测试的代码区域为何失败。有关调试的更多信息或了解如何在 VS Code 中进行调试，您可以阅读 Python 调试配置和常规 VS Code 调试文章。

For example, the `test_decrement` functions given earlier are failing because the assertion itself is faulty. The following steps demonstrate how to analyze the test:

&zeroWidthSpace;例如，前面给出的 `test_decrement` 函数失败，因为断言本身有缺陷。以下步骤演示如何分析测试：

1. Set a breakpoint on the first line in the `test_decrement` function.

   &zeroWidthSpace;在 `test_decrement` 函数的第一行设置断点。

2. Right-click on the gutter decoration next to the function definition and select **Debug Test**, or select the **Debug Test** icon next to that test in the **Test Explorer**. VS Code starts the debugger and pauses at the breakpoint.

   &zeroWidthSpace;右键单击函数定义旁边的编辑器装饰，然后选择“调试测试”，或在测试资源管理器中该测试旁边选择“调试测试”图标。VS Code 启动调试器并在断点处暂停。

   ![Debug Test icon in the Test Explorer](https://code.visualstudio.com/assets/docs/python/testing/debug-test-in-explorer.png)

3. In the **Debug Console** panel, enter `inc_dec.decrement(3)` to see that the actual result is 2, whereas the expected result specified in the test is the incorrect value of 4.

   &zeroWidthSpace;在“调试控制台”面板中，输入 `inc_dec.decrement(3)` 以查看实际结果为 2，而测试中指定的预期结果为错误值 4。

4. Stop the debugger and correct the faulty code:

   &zeroWidthSpace;停止调试器并更正有问题的代码：

   ```
   # unittest
   self.assertEqual(inc_dec.decrement(3), 2)
   
   # pytest
   assert inc_dec.decrement(3) == 2
   ```

5. Save the file and run the tests again to confirm that they pass, and see that the gutter decorations also indicate passing status.

   &zeroWidthSpace;保存文件并再次运行测试以确认它们通过，并查看编辑器装饰也指示通过状态。

   > **Note**: Running or debugging a test does not automatically save the test file. Always be sure to save changes to a test before running it, otherwise you'll likely be confused by the results because they still reflect the previous version of the file!
   >
   > &zeroWidthSpace;注意：运行或调试测试不会自动保存测试文件。务必在运行测试前保存对测试所做的更改，否则您很可能会对结果感到困惑，因为它们仍反映文件的前一个版本！

You can use the following commands from the Command Palette to debug tests:

&zeroWidthSpace;您可以使用“命令面板”中的以下命令来调试测试：

- **Test: Debug All Tests** - Launches the debugger for all tests in your workspace.
  测试：调试所有测试 - 为工作区中的所有测试启动调试器。
- **Test: Debug Tests in Current File** - Launches the debugger for the tests you have defined in the file you have open in the editor.
  测试：调试当前文件中的测试 - 为您在编辑器中打开的文件中定义的测试启动调试器。
- **Test: Debug Test at Cursor** - Launches the debugger only for the method where you have your cursor focused on the editor. You can also use the **Debug Test** icons in Test Explorer to launch the debugger for all tests in a selected scope and all discovered tests.
  测试：调试光标处的测试 - 仅为光标在编辑器中聚焦的方法启动调试器。您还可以使用“测试资源管理器”中的“调试测试”图标为选定范围内的所有测试和所有发现的测试启动调试器。

You can also change the default behavior of clicking on the gutter decoration to debug tests instead of run, by changing the `testing.defaultGutterClickAction` setting value to `debug` in your `settings.json` file.

&zeroWidthSpace;您还可以通过将 `testing.defaultGutterClickAction` 设置值更改为 `debug` 来更改单击边距装饰以调试测试而不是运行的默认行为，方法是在 `settings.json` 文件中进行更改。

The debugger works the same for tests as for other Python code, including breakpoints, variable inspection, and so on. To customize settings for debugging tests, you can specify `"purpose": ["debug-test"]` in the `launch.json` file in the `.vscode` folder from your workspace. This configuration will be used when you run **Test: Debug All Tests**, **Test: Debug Tests in Current File** and **Test: Debug Test at Cursor** commands.

&zeroWidthSpace;调试器对测试和其它 Python 代码的工作方式相同，包括断点、变量检查等。要自定义调试测试的设置，您可以在工作区中的 `.vscode` 文件夹中的 `launch.json` 文件中指定 `"purpose": ["debug-test"]` 。当您运行“测试：调试所有测试”、“测试：调试当前文件中的测试”和“测试：调试光标处的测试”命令时，将使用此配置。

For example, the configuration below in the `launch.json` file disables the `justMyCode` setting for debugging tests:

&zeroWidthSpace;例如， `launch.json` 文件中的以下配置禁用了调试测试的 `justMyCode` 设置：

```
{
  "name": "Python: Debug Tests",
  "type": "python",
  "request": "launch",
  "program": "${file}",
  "purpose": ["debug-test"],
  "console": "integratedTerminal",
  "justMyCode": false
}
```

If you have more than one configuration entry with `"purpose": ["debug-test"]`, the first definition will be used since we currently don't support multiple definitions for this request type.

&zeroWidthSpace;如果您有多个带有 `"purpose": ["debug-test"]` 的配置条目，则将使用第一个定义，因为我们目前不支持此请求类型的多个定义。

## [Test commands 测试命令](https://code.visualstudio.com/docs/python/testing#_test-commands)

Below are all the supported commands for testing with the Python extension in VS Code. These are all found via the Command Palette:

&zeroWidthSpace;以下是 VS Code 中使用 Python 扩展进行测试的所有受支持命令。这些都可以在命令面板中找到：

| Command Name 命令名称                                        | Description 说明                                             |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **Python: Configure Tests Python：配置测试**                 | Configure the test framework to be used with the Python extension. 配置要与 Python 扩展一起使用的测试框架。 |
| **Test: Clear All Results 测试：清除所有结果**               | Clear all tests statuses, as the UI persists test results across sessions. 清除所有测试状态，因为 UI 会在各个会话中保留测试结果。 |
| **Test: Debug Failed Tests 测试：调试失败的测试**            | Debug tests that failed in the most recent test run. 调试在最近一次测试运行中失败的测试。 |
| **Test: Debug Last Run 测试：调试上次运行**                  | Debug tests that were executed in the most recent test run. 调试在最近一次测试运行中执行的测试。 |
| **Test: Debug Test at Cursor 测试：调试光标处的测试**        | Debug the test method where you have your cursor focused on the editor. Similar to **Python: Debug Test Method...** on versions prior to 2021.9. 调试您在编辑器中将光标聚焦到的测试方法。类似于 Python：在 2021.9 之前的版本中调试测试方法... |
| **Test: Debug Tests in Current File 测试：调试当前文件中的测试** | Debug tests in the file that is currently in focus on the editor. 调试当前在编辑器中聚焦的文件中的测试。 |
| **Test: Go to Next Test Failure 测试：转到下一个测试失败**   | If the error peek view is open, open and move to the peek view of the next test in the explorer that has failed. 如果错误预览视图已打开，请打开并移至资源管理器中下一个失败测试的预览视图。 |
| **Test: Go to Previous Test Failure 测试：转到上一个测试失败** | If the error peek view is open, open and move to the peek view of the previous test in the explorer that has failed. 如果错误预览视图已打开，请打开并移至资源管理器中上一个失败测试的预览视图。 |
| **Test: Peek Output 测试：预览输出**                         | Opens the error peek view for a test method that has failed. 为失败的测试方法打开错误预览视图。 |
| **Test: Refresh Tests 测试：刷新测试**                       | Perform test discovery and updates the Test Explorer to reflect any test changes, addition, or deletion. Similar to **Python: Discover Tests** on versions prior to 2021.9. 执行测试发现并更新测试资源管理器以反映任何测试更改、添加或删除。类似于 Python：在 2021.9 之前的版本上发现测试。 |
| **Test: Rerun Failed Tests 测试：重新运行失败的测试**        | Run tests that failed in the most recent test run. Similar to **Python: Run Failed Tests** on versions prior to 2021.9. 运行在最近一次测试运行中失败的测试。类似于 Python：在 2021.9 之前的版本上运行失败的测试。 |
| **Test: Rerun Last Run 测试：重新运行上次运行**              | Debug tests that were executed in the most recent test run. 调试在最近一次测试运行中执行的测试。 |
| **Test: Run All Tests 测试：运行所有测试**                   | Run all discovered tests. Equivalent to **Python: Run All Tests** on versions prior to 2021.9. 运行所有发现的测试。相当于 Python：在 2021.9 之前的版本上运行所有测试。 |
| **Test: Run Test at Cursor 测试：运行光标处的测试**          | Run the test method where you have your cursor focused on the editor. Similar to **Python: Run Test Method...** on versions prior to 2021.9. 运行您在编辑器中将光标聚焦到的测试方法。类似于 Python：在 2021.9 之前的版本上运行测试方法... |
| **Test: Run Test in Current File 测试：运行当前文件中的测试** | Run tests in the file that is currently in focus on the editor. Equivalent to **Python: Run Current Test File** on versions prior to 2021.9. 运行当前在编辑器中聚焦的文件中的测试。相当于 Python：在 2021.9 之前的版本上运行当前测试文件。 |
| **Test: Show Output 测试：显示输出**                         | Open the output with details of all the test runs. Similar to **Python: Show Test Output** on versions prior to 2021.9. 打开包含所有测试运行详细信息的输出。类似于 Python：在 2021.9 之前的版本上显示测试输出。 |
| **Testing: Focus on Test Explorer View 测试：聚焦于测试资源管理器视图** | Open the Test Explorer view. Similar to **Testing: Focus on Python View** on versions prior to 2021.9. 打开测试资源管理器视图。类似于测试：在 2021.9 之前的版本上关注 Python 视图。 |
| **Test: Stop Refreshing Tests 测试：停止刷新测试**           | Cancel test discovery. 取消测试发现。                        |

## [IntelliSense for pytest pytest 的 IntelliSense](https://code.visualstudio.com/docs/python/testing#_intellisense-for-pytest)

[Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance) offers IntelliSense features that can help you work more efficiently with [pytest fixtures](https://docs.pytest.org/en/6.2.x/fixture.html) and [parameterized tests](https://docs.pytest.org/en/6.2.x/parametrize.html).

&zeroWidthSpace;Pylance 提供 IntelliSense 功能，可以帮助您更有效地使用 pytest 夹具和参数化测试。

As you're typing the parameters for your test function, Pylance will offer you a list of [completions](https://code.visualstudio.com/docs/python/editing#_autocomplete-and-intellisense) that includes argument names from `@pytest.mark.parametrize` decorators, as well as existing pytest fixtures defined in your tests file or in `conftest.py`. [Code navigation](https://code.visualstudio.com/docs/python/editing#_navigation) features such as **Go to Definition** and **Find All References** and [rename symbol refactoring](https://code.visualstudio.com/docs/editor/refactoring#_rename-symbol) are also supported.

&zeroWidthSpace;在键入测试函数的参数时，Pylance 会为您提供一个完成列表，其中包括来自 `@pytest.mark.parametrize` 装饰器的参数名称，以及在测试文件中或 `conftest.py` 中定义的现有 pytest 夹具。还支持代码导航功能，例如转到定义和查找所有引用以及重命名符号重构。

![Auto completion suggestion when passing a parameter to a test function in a Python test file. The suggestion is a fixture defined in conftest.py.](https://code.visualstudio.com/assets/docs/python/testing/pytest-fixture-autocomplete.png)

When hovering over a fixture reference or a parameterized argument reference, Pylance will show the inferred type annotation, either based on the return values of the fixture, or based on the inferred types of the arguments passed to the parameterization decorator.

&zeroWidthSpace;将鼠标悬停在夹具引用或参数化参数引用上时，Pylance 将显示推断的类型注释，该注释基于夹具的返回值或基于传递给参数化装饰器的参数的推断类型。

![Pylance type inference based on the types of arguments passed to the parameterization decorator.](https://code.visualstudio.com/assets/docs/python/testing/pytest-inferred-parametrized-argument.png)

Pylance also offers [code actions](https://code.visualstudio.com/docs/editor/refactoring#_code-actions--quick-fixes-and-refactorings) to add type annotations to test functions that have fixture parameters. Inlay hints for inferred fixture parameter types can also be enabled by setting `python.analysis.inlayHints.pytestParameters` to `true` in your User settings.

&zeroWidthSpace;Pylance 还提供代码操作，以向具有夹具参数的测试函数添加类型注释。还可以通过在用户设置中将 `python.analysis.inlayHints.pytestParameters` 设置为 `true` 来启用推断的夹具参数类型的内联提示。

![Code action to add type annotation when hoving over a test function with a fixture parameter](https://code.visualstudio.com/assets/docs/python/testing/pytest-annotation-code-action.png)

## [Test configuration settings 测试配置设置](https://code.visualstudio.com/docs/python/testing#_test-configuration-settings)

The behavior of testing with Python is driven by general UI settings provided by VS Code, and settings that are specific to Python and to whichever framework you've enabled.

&zeroWidthSpace;使用 Python 进行测试的行为由 VS Code 提供的常规 UI 设置以及特定于 Python 和已启用框架的设置驱动。

### [General UI settings 常规 UI 设置](https://code.visualstudio.com/docs/python/testing#_general-ui-settings)

The settings that affect the UI of the testing features are provided by VS Code itself, and can be found in the [VS Code Settings editor](https://code.visualstudio.com/docs/getstarted/settings) when you search for "Testing".

&zeroWidthSpace;影响测试功能 UI 的设置由 VS Code 本身提供，可以在搜索“测试”时在 VS Code 设置编辑器中找到。

### [General Python settings 常规 Python 设置](https://code.visualstudio.com/docs/python/testing#_general-python-settings)

| Setting 设置 (python.testing.) | Default 默认 | Description 说明                                             |
| :----------------------------- | :----------- | :----------------------------------------------------------- |
| autoTestDiscoverOnSaveEnabled  | `true`       | Specifies whether to enable or disable auto run test discovery when saving a test file. You may need to reload the window after making changes to this setting for it to be applied. 指定在保存测试文件时启用还是禁用自动运行测试发现。您可能需要在对该设置进行更改后重新加载窗口才能应用该设置。 |
| cwd                            | null         | Specifies an optional working directory for tests. 指定测试的可选工作目录。 |
| debugPort                      | `3000`       | Port number used for debugging of unittest tests. 用于调试单元测试的端口号。 |
| promptToConfigure              | `true`       | Specifies whether VS Code prompts to configure a test framework if potential tests are discovered. 指定 VS Code 是否在发现潜在测试时提示配置测试框架。 |

### [unittest configuration settings unittest 配置设置](https://code.visualstudio.com/docs/python/testing#_unittest-configuration-settings)

| Unittest setting Unittest 设置 (python.testing.) | Default 默认                           | Description 说明                                             |
| :----------------------------------------------- | :------------------------------------- | :----------------------------------------------------------- |
| unittestEnabled                                  | `false`                                | Specifies whether unittest is enabled as the test framework. The equivalent setting for pytest should be disabled. 指定是否将 unittest 启用为测试框架。应禁用 pytest 的等效设置。 |
| unittestArgs                                     | `["-v", "-s", ".", "-p", "*test*.py"]` | Arguments to pass to unittest, where each element that's separated by a space is a separate item in the list. See below for a description of the defaults. 传递给 unittest 的参数，其中以空格分隔的每个元素都是列表中的一个单独项。有关默认值的说明，请参见下文。 |

The default arguments for unittest are as follows:

&zeroWidthSpace;unittest 的默认参数如下：

- `-v` sets default verbosity. Remove this argument for simpler output.
  `-v` 设置默认详细程度。删除此参数以获得更简单的输出。
- `-s .` specifies the starting directory for discovering tests. If you have tests in a "test" folder, change the argument to `-s test` (meaning `"-s", "test"` in the arguments array).
  `-s .` 指定用于发现测试的起始目录。如果在“test”文件夹中进行测试，请将参数更改为 `-s test` （表示参数数组中的 `"-s", "test"` ）。
- `-p *test*.py` is the discovery pattern used to look for tests. In this case, it's any `.py` file that includes the word "test". If you name test files differently, such as appending "_test" to every filename, then use a pattern like `*_test.py` in the appropriate argument of the array.
  `-p *test*.py` 是用于查找测试的发现模式。在这种情况下，它是包含单词“test”的任何 `.py` 文件。如果您对测试文件命名不同，例如在每个文件名后附加“_test”，则在数组的相应参数中使用类似 `*_test.py` 的模式。

To stop a test run on the first failure, add the fail fast option `"-f"` to the arguments array.

&zeroWidthSpace;要在第一次失败时停止测试运行，请将快速失败选项 `"-f"` 添加到参数数组。

See [unittest command-line interface](https://docs.python.org/3/library/unittest.html#command-line-interface) for the full set of available options.

&zeroWidthSpace;有关可用选项的完整列表，请参阅 unittest 命令行界面。

### [pytest configuration settings pytest 配置设置](https://code.visualstudio.com/docs/python/testing#_pytest-configuration-settings)

| pytest setting pytest 设置 (python.testing.) | Default 默认 | Description 说明                                             |
| :------------------------------------------- | :----------- | :----------------------------------------------------------- |
| pytestEnabled                                | `false`      | Specifies whether pytest is enabled as the test framework. The equivalent setting for unittest should be disabled. 指定是否将 pytest 启用为测试框架。应禁用 unittest 的等效设置。 |
| pytestPath                                   | `"pytest"`   | Path to pytest. Use a full path if pytest is located outside the current environment. 指向 pytest 的路径。如果 pytest 位于当前环境之外，请使用完整路径。 |
| pytestArgs                                   | `[]`         | Arguments to pass to pytest, where each element that's separated by a space is a separate item in the list. See [pytest command-line options](https://docs.pytest.org/en/latest/reference/reference.html#command-line-flags). 要传递给 pytest 的参数，其中每个以空格分隔的元素都是列表中的一个单独项。请参阅 pytest 命令行选项。 |

You can also configure pytest using a `pytest.ini` file as described on [pytest Configuration](https://docs.pytest.org/en/latest/reference/customize.html).

&zeroWidthSpace;您还可以按照 pytest 配置中所述使用 `pytest.ini` 文件配置 pytest。

> **Note** If you have the pytest-cov coverage module installed, VS Code doesn't stop at breakpoints while debugging because pytest-cov is using the same technique to access the source code being run. To prevent this behavior, include `--no-cov` in `pytestArgs` when debugging tests, for example by adding `"env": {"PYTEST_ADDOPTS": "--no-cov"}` to your debug configuration. (See [Debug Tests](https://code.visualstudio.com/docs/python/testing#_debug-tests) above about how to set up that launch configuration.) (For more information, see [Debuggers and PyCharm](https://pytest-cov.readthedocs.io/en/latest/debuggers.html) in the pytest-cov documentation.)
>
> &zeroWidthSpace;注意如果您安装了 pytest-cov 覆盖率模块，VS Code 在调试时不会在断点处停止，因为 pytest-cov 使用相同技术来访问正在运行的源代码。为防止出现此行为，请在调试测试时将 `--no-cov` 包含在 `pytestArgs` 中，例如通过将 `"env": {"PYTEST_ADDOPTS": "--no-cov"}` 添加到您的调试配置中。（请参阅上面的“调试测试”了解如何设置该启动配置。）（有关更多信息，请参阅 pytest-cov 文档中的“调试器和 PyCharm”。）

### [IntelliSense settings IntelliSense 设置](https://code.visualstudio.com/docs/python/testing#_intellisense-settings)

| IntelliSense setting IntelliSense 设置 (python.analysis.) | Default 默认 | Description 说明                                             |
| :-------------------------------------------------------- | :----------- | :----------------------------------------------------------- |
| inlayHints.pytestParameters                               | false        | Whether to display inlay hints for pytest fixture argument types. Accepted values are `true` or `false`. 是否为 pytest 固定参数类型显示内联提示。接受的值是 `true` 或 `false` 。 |

## [See also 另请参阅](https://code.visualstudio.com/docs/python/testing#_see-also)

- [Python environments](https://code.visualstudio.com/docs/python/environments) - Control which Python interpreter is used for editing and debugging.
  Python 环境 - 控制用于编辑和调试的 Python 解释器。
- [Settings reference](https://code.visualstudio.com/docs/python/settings-reference) - Explore the full range of Python-related settings in VS Code.
  设置参考 - 探索 VS Code 中与 Python 相关的全部设置。
