---
title: "使用 Visual Studio for Mac 在 macOS 上构建完整的 .NET Core 解决方案"
description: "本主题演示了构建包含可重用的库和单元测试的 .NET Core 解决方案。"
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 06/12/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 6945bedf-5bf3-4955-8588-83fb87511b79
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 60179fb0435803c3235b75ba012e588c6f1b35d3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="building-a-complete-net-core-solution-on-macos-using-visual-studio-for-mac"></a>使用 Visual Studio for Mac 在 macOS 上构建完整的 .NET Core 解决方案

Visual Studio for Mac 提供用于开发 .NET Core 应用程序的功能全面的集成开发环境 (IDE)。 本主题演示了构建包含可重用的库和单元测试的 .NET Core 解决方案。

本教程介绍了如何创建接受来自用户的搜索词和文本字符串、使用类库中的方法计算字符串中出现的搜索词的次数，并将结果返回给用户的应用程序。 该解决方案还包括针对类库的单元测试作为测试驱动开发 (TDD) 概念的介绍。 如果希望使用完整的示例学习该教程，请下载[示例解决方案](https://github.com/dotnet/docs/blob/master/samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

> [!NOTE]
> 你的反馈非常有价值。 有两种方法可以向开发团队提供有关 Visual Studio for Mac 的反馈：
> * 在 Visual Studio for Mac 中，从菜单选择“帮助” > “报告问题”，或从欢迎屏幕中选择“报告问题”，将打开一个窗口，以供填写 bug 报告。 可在[开发人员社区](https://developercommunity.visualstudio.com/spaces/41/index.html)门户中跟踪自己的反馈。
> * 若要提出建议，从菜单中选择“帮助” > “提供建议”，或从欢迎屏幕中选择“提供建议”，转到 [Visual Studio for Mac UserVoice 网页](https://visualstudio.uservoice.com/forums/563332-visual-studio-for-mac)。

## <a name="prerequisites"></a>先决条件

- OpenSSL（如果运行 .NET Core 1.1）：请参阅 [Mac 上 .NET Core 的先决条件](../macos-prerequisites.md)主题。
- [.NET Core SDK 1.1 或更高版本](https://www.microsoft.com/net/core#macos)
- [Visual Studio 2017 for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

有关先决条件的详细信息，请参阅 [Mac 上的 .NET Core 的先决条件](../../core/macos-prerequisites.md)。 有关 Visual Studio 2017 for Mac 完整系统要求的信息，请参阅 [Visual Studio 2017 for Mac 产品系列系统要求](https://www.visualstudio.com/productinfo/vs2017-system-requirements-mac)。

## <a name="building-a-library"></a>生成库

1. 在欢迎屏幕上，选择“新建项目”。 在“多平台”节点下的“新建项目”对话框中，选择“.NET 标准库”模板。 选择“下一步”。

   ![“新建项目”对话框](./media/using-on-mac-vs-full-solution/vsmacfull01.png)

1. 将项目命名为“TextUtils”（“Text Utilities”的短名称），将解决方案命名为“WordCounter”。 使“在解决方案目录中创建项目目录”保持选中状态。 选择“创建”。

   ![“新建项目”对话框](./media/using-on-mac-vs-full-solution/vsmacfull02.png)

1. 在“解决方案”边栏中，展开 `TextUtils` 节点以显示模板提供的类文件 *Class1.cs*。 右键单击该文件，从上下文菜单中选择“重命名”，然后将该文件重命名为 *WordCount.cs*。 打开文件并将内容替换为以下代码：

   [!code-csharp[Main](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/TextUtils/WordCount.cs)]

1. 通过使用以下三种不同的方法之一保存文件：使用键盘快捷方式 <kbd>&#8984;</kbd>+<kbd>s</kbd>，从菜单中选择“文件” > “保存”，或右键单击文件的选项卡，并从上下文菜单中选择“保存”。 下图显示 IDE 窗口：

   ![IDE 窗口显示 TextUtils 类库、WordCount 类文件、静态类 WordCount 和 GetWordCount 方法](./media/using-on-mac-vs-full-solution/vsmacfull03.png)

1. 在 IDE 窗口底部边距处选择“错误”，打开“错误”面板。 选择“生成输出”按钮。

   ![IDE 的底部边距处显示错误按钮](./media/using-on-mac-vs-full-solution/vsmacfull03b.png)

1. 从菜单中选择“生成” > “生成所有”。

   生成解决方案。 生成输出面板显示生成成功。

   ![错误面板的生成输出面板显示生成成功消息](./media/using-on-mac-vs-full-solution/vsmacfull04.png)

## <a name="creating-a-test-project"></a>创建测试项目

单元测试在开发和发布期间提供自动化的软件测试。 本教程中使用的测试框架是 [xUnit（版本 2.2.0 或更高版本）](https://xunit.github.io/)，使用下列步骤将 xUnit 测试项目添加到解决方案时将自动安装此框架：

1. 在“解决方案”边栏中，右键单击 `WordCounter` 解决方案并选择“添加” > “添加新项目”。

1. 在“新建项目”对话框中，从“.NET Core”节点中选择“测试”。 在“下一步”后，选择“xUnit 测试项目”。

   ![创建 xUnit 测试项目的“新建项目”对话框](./media/using-on-mac-vs-full-solution/vsmacfull05.png)

1. 将新项目命名为"TestLibrary"，然后选择“创建”。

   ![提供项目名称的“新建项目”对话框](./media/using-on-mac-vs-full-solution/vsmacfull06.png)

1. 若要使测试库使用 `WordCount` 类，请将引用添加到 `TextUtils` 项目中。 在“解决方案”边栏中，右键单击“TestLibrary”下的“依赖项”。 从上下文菜单中选择“编辑引用”。

1. 在“编辑引用”对话框中，选择“项目”选项卡上的“TextUtils”项目。 选择“确定”。

   ![编辑引用对话框](./media/using-on-mac-vs-full-solution/vsmacfull07.png)

1. 在 **TestLibrary** 项目中，将 *UnitTest1.cs* 文件重命名为 *TextUtilsTests.cs*。

1. 打开该文件，并将代码替换为以下内容：

   ```csharp
   using Xunit;
   using TextUtils;
   using System.Diagnostics;

   namespace TestLibrary
   {
       public class TextUtils_GetWordCountShould
       {
           [Fact]
           public void IgnoreCasing()
           {
               var wordCount = WordCount.GetWordCount("Jack", "Jack jack");
   
               Assert.NotEqual(2, wordCount);
           }
       }
   }
   ```

   下图显示了就地使用单元测试代码的 IDE。 请注意 `Assert.NotEqual` 语句。

   ![在 IDE 主窗口中检查 GetWordCount 的初始单元测试](./media/using-on-mac-vs-full-solution/vsmacfull08.png)

   使用 TDD 时，请务必使新的测试失败一次，以确定其测试逻辑正确无误。 该方法使用“Jack”和“jack”（大写和小写）传递名称“Jack”（大写）和字符串。 如果 `GetWordCount` 方法运行正常，则返回搜索词的两个实例的计数。 为了有意进行失败测试，首先实现测试断言，即搜索词“Jack”的两个实例不是由 `GetWordCount` 方法返回的。 继续执行下一步骤，有意使测试失败。

1. 打开屏幕右侧的“单元测试”面板。

![“单元测试”面板](./media/using-on-mac-vs-full-solution/vsmacfull_UnitTestPanel.png)

1. 单击“停靠”图标使此面板保持打开状态。

![“单元测试”面板“停靠”图标](./media/using-on-mac-vs-full-solution/vsmacfull_UnitTestPanelDockIcon.png)

1. 单击“全部运行”按钮。
   
   测试失败，这是正确的结果。 测试方法断言不会从提供给 `GetWordCount` 的方法的字符串“Jack jack”中返回 `inputString`“Jack”的两个实例。 因为已在 `GetWordCount` 方法中对单词的大小写进行了分解，所以返回了两个实例。 2  *不等于*  2 的断言失败。 这是正确的结果，且测试的逻辑良好。

   ![测试失败](./media/using-on-mac-vs-full-solution/vsmacfull09.png)

1. 通过将 `Assert.NotEqual` 更改为 `Assert.Equal` 来修改 `IgnoreCasing` 测试方法。 使用键盘快捷方式 <kbd>&#8984;</kbd>+<kbd>s</kbd> 保存该文件，从菜单选择“文件” > “保存”，或右键单击文件的选项卡，并从上下文菜单中选择“保存”。

   `searchWord`Jack”应返回两个实例，并且 `inputString`“Jack jack”传递到 `GetWordCount`。 通过单击“单元测试”面板中的“运行测试”按钮或屏幕底部的“测试结果”面板中的“重新运行测试”按钮重新运行测试。 测试通过。 在字符串"Jack jack"（忽略大小写）中有“Jack”的两个实例，且测试断言为 `true`。

   ![测试通过](./media/using-on-mac-vs-full-solution/vsmacfull10.png)

1. 使用 `Fact` 测试单个返回值仅仅是借助单元测试可以实现的功能的开始。 另一个功能强大的技术是允许你使用 `Theory` 立即测试多个值。 将以下方法添加到你的 `TextUtils_GetWordCountShould` 类。 添加该方法后，在类中有两个方法：

   ```csharp
   [Theory]
   [InlineData(0, "Ting", "Does not appear in the string.")]
   [InlineData(1, "Ting", "Ting appears once.")]
   [InlineData(2, "Ting", "Ting appears twice with Ting.")]
   public void CountInstancesCorrectly(int count, 
                                       string searchWord, 
                                       string inputString)
   {
       Assert.NotEqual(count, WordCount.GetWordCount(searchWord,
                                                  inputString));
   }
   ```

   `CountInstancesCorrectly` 检查 `GetWordCount` 方法计数是否正确。 `InlineData` 提供计数、搜索词和要检查的输入字符串。 测试方法为数据的每行运行一次。 请再次注意，使用 `Assert.NotEqual` 首先声明失败，即使知道数据中的计数是正确的，且这些值与 `GetWordCount` 方法所返回的计数相匹配。 有意执行测试失败的步骤起初看起来像是浪费时间，但是首先通过失败测试检查测试的逻辑对于测试逻辑而言，是一项重要检查。 如果在预期失败时找到一种可通过的测试方法，则你已在测试逻辑中找到 bug。 每次创建测试方法时，都值得采取此步骤。
   
1. 保存文件并重新运行测试。 大小写测试通过，但三个计数测试失败。 这与我们预期的结果完全一致。

   ![测试失败](./media/using-on-mac-vs-full-solution/vsmacfull11.png)

1. 通过将 `Assert.NotEqual` 更改为 `Assert.Equal` 来修改 `CountInstancesCorrectly` 测试方法。 保存该文件。 重新运行测试。 所有测试通过。

   ![测试通过](./media/using-on-mac-vs-full-solution/vsmacfull12.png)

## <a name="adding-a-console-app"></a>添加控制台应用

1. 在“解决方案”边栏中，右键单击 `WordCounter` 解决方案。 通过从“.NET Core” > “应用” 模板中选择模板来添加新的**控制台应用程序**项目。 选择“下一步”。 将项目命名为 **WordCounterApp**。 选择“创建”以在解决方案中创建项目。

1. 在“解决方案”边栏中，右键单击新 **WordCounterApp** 项目的“依赖项”。 在“编辑引用”对话框中，选中“TextUtils”，然后选择“确定”。

1. 打开 *Program.cs* 文件。 将代码替换为以下内容：

   [!code-csharp[Main](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/WordCounterApp/Program.cs)]

1. 如要在控制台窗口而不是在 IDE 中运行应用，右键单击 `WordCounterApp` 项目，选择“选项”，然后打开“配置”下的“默认”节点。 选中“在外部控制台上运行”框。 使“暂停控制台输出”选项保持选中状态。 此设置使应用在控制台窗口中生成，以便可以为 `Console.ReadLine` 语句键入输入。 如果使应用在 IDE 中持续运行，则仅能看到 `Console.WriteLine` 语句的输出。 `Console.ReadLine` 语句无法在 IDE 的“应用程序输出”面板中运行。

   ![项目选项窗口](./media/using-on-mac-vs-full-solution/vsmacfull13.png)

1. 由于 Visual Studio for Mac 的当前版本无法在解决方案运行时运行测试，因此，可以直接运行控制台应用。 右键单击 `WordCounterApp` 项目，并从上下文菜单中选择“运行项目”。 如果尝试使用播放按钮运行应用，测试运行程序和应用将无法运行。 有关此问题的运行状态的详细信息，请参阅 [xunit/xamarinstudio.xunit (#60)](https://github.com/xunit/xamarinstudio.xunit/issues/60)。 运行应用时，在控制台窗口中的提示符处提供搜索词和输入字符串的值。 应用指示搜索词在字符串中出现的次数。

   ![控制台窗口显示字符串中搜索的词 olives，“Iro ate olives by the lake, and the olives were wonderful.” 应用作出响应：“搜索词 olives 出现 2 次。”](./media/using-on-mac-vs-full-solution/vsmacfull14.png)

1. 要探索的最后一个功能是使用 Visual Studio for Mac 进行调试。 在 `Console.WriteLine` 语句上设置断点：在第 23 行的左边距处选择，可以看到代码行旁边出现红色的圆圈。 或者，在代码行上的任意位置进行选择，然后从菜单中选择“运行” > “切换断点”。

   ![在第 23 行 Console.WriteLine 语句处设置断点](./media/using-on-mac-vs-full-solution/vsmacfull15.png)

1. 右键单击 `WordCounterApp` 项目。 从上下文菜单中选择“开始调试项目”。 应用运行时，输入搜索词“cat”和“The dog chased the cat, but the cat escaped.” 以供字符串进行搜索。 到达 `Console.WriteLine` 语句时，将在执行该语句前暂停执行程序。 在“本地”选项卡中，可以看到 `searchWord`、`inputString`、`wordCount` 和 `pluralChar` 值。

   ![在 Console.WriteLine 语句处停止执行程序，且本地窗口将在执行 Console.WriteLine 语句前立即显示值。](./media/using-on-mac-vs-full-solution/vsmacfull16.png)

1. 在“即时”面板中，键入“wordCount = 999;”，然后按 Enter 键。 该操作将无意义的值 999 分配到 `wordCount` 变量，显示可以在调试时替换变量值。

   ![命中端点。 wordCount 在“即时”窗口中更改为值 999](./media/using-on-mac-vs-full-solution/vsmacfull17.png)

1. 在工具栏中，单击“继续”。 查看控制台窗口中的输出。 它报告调试应用时所设置的不正确的值 999。

   ![工具栏中的继续按钮](./media/using-on-mac-vs-full-solution/vsmacfull18.png)

   ![搜索词计数在应用的输出中更改为值 999](./media/using-on-mac-vs-full-solution/vsmacfull19.png)

## <a name="see-also"></a>请参阅

[Visual Studio 2017 for Mac 发行说明](https://www.visualstudio.com/news/releasenotes/vs2017-mac-relnotes)

