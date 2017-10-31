---
title: "使用 Visual Studio 2017 调试 C# Hello World 应用程序"
description: "了解如何使用 Visual Studio 2017 调试用 C# 编写的 Hello World 应用程序。"
keywords: ".NET Core, .NET Core 控制台应用程序, .NET Core 调试"
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: cb213625-cc60-438b-9b9e-49aed0e4a974
ms.translationtype: HT
ms.sourcegitcommit: e0271ba3392ce8861dc916714af8c16d4581ce4f
ms.openlocfilehash: 19744773d18f6ea43e4b4a7518405b60e6b53acf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---

# <a name="debug-your-hello-world-application-with-visual-studio-2017"></a>使用 Visual Studio 2017 调试 Hello World 应用程序

至此，已按照[使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序](.\with-visual-studio.md)或[使用 Visual Studio 2017 生成 Visual Basic .NET Core Hello World 用用程序](vb-with-visual-studio.md)中的步骤操作，创建和运行简单的控制台应用程序。 编写和编译应用程序后，可以开始进行测试。 Visual Studio 提供一整套调试工具，方便你在测试和排除应用程序故障时使用。

## <a name="debugging-in-debug-mode"></a>在调试模式下调试

“调试”和“发布”是 Visual Studio 的两种默认生成配置。 当前的生成配置显示在工具栏上。 下面的工具栏图像显示 Visual Studio 配置为在“调试”模式下编译应用程序。

   ![Visual Studio 工具栏](./media/debugging-with-visual-studio/toolbar1.png)

一开始应始终在调试模式下测试程序。 调试模式会禁用大多数编译器优化，并在生成过程中提供更丰富的信息。

## <a name="setting-a-breakpoint"></a>设置断点

在调试模式下运行程序，并尝试一些调试功能：

1. 断点会在执行包含断点的代码行之前暂时中断执行应用程序。 

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
   若要在 `Console.WriteLine($"\nHello, {name}, on {date:d} at {date:t}!");` 一行上设置断点，可单击该行上代码窗口的左侧边缘，或选中该行，选择“调试” > “切换断点”菜单项。 如下图所示，Visual Studio 通过突出显示此代码行，并在其左侧边缘显示红色圆圈来指明这行设置了断点。

   ![设置断点后的 Visual Studio 程序窗口](./media/debugging-with-visual-studio/setbreakpoint.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
   若要在 `Console.WriteLine(vbCrLf + $"Hello, {name}, on {currentDate:d} at {currentDate:t}!")` 一行上设置断点，可单击该行上代码窗口的左侧边缘，或选中该行，选择“调试” > “切换断点”菜单项。 如下图所示，Visual Studio 通过突出显示此代码行，并在其左侧边缘显示红色圆圈来指明这行设置了断点。

   <a name="visual-studio-program-window-with-breakpoint-setmediadebugging-with-visual-studiovb-setbreakpointpng"></a>![设置断点后的 Visual Studio 程序窗口](./media/debugging-with-visual-studio/vb-setbreakpoint.png)
---

1. 选择工具栏上含绿色箭头的“HelloWorld”按钮、按 F5 或选择“调试” > “启动调试”，在调试模式下运行程序。

1. 当程序提示输入名称时，在控制台窗口中输入字符串，然后按 Enter 键。

1. 到达断点时，程序停止执行，然后执行 `Console.WriteLine` 方法。 “自动”窗口显示当前代码行周围使用的变量值。 “局部变量”窗口（可以通过单击“局部变量”选项卡查看）显示当前正在执行的方法中定义的变量值。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
   ![Visual Studio 应用程序窗口](./media/debugging-with-visual-studio/break.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
   <a name="visual-studio-application-windowmediadebugging-with-visual-studiovb-breakpng"></a>![Visual Studio 应用程序窗口](./media/debugging-with-visual-studio/vb-break.png)
---

1. 可更改变量值，查看这样会对程序产生哪些影响。 如果“即时窗口”不可见，请选择“调试” > “Windows” > “即时”菜单项来显示它。 在“即时窗口”中，可以与正在调试的应用程序进行交互。

1. 可以交互方式更改变量的值。 在“即时窗口”中输入 `name = "Gracie"`，然后按 Enter 键。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 在“即时窗口”中输入 `date = new DateTime(2016,11,01,11,59,00)`，然后按 Enter 键。

   “即时窗口”窗口显示字符串变量的值和 @System.DateTime 值的属性。 此外，**“自动”**和**“局部变量”**窗口中也会更新变量值。

   ![自动窗口和即时窗口](./media/debugging-with-visual-studio/autosimmediate.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 在“即时窗口”中输入 `currentDate = new DateTime(2016,11,01,11,59,00)`，然后按 Enter 键。

<!-- The **Immediate Window** displays the value of the string variable and the properties of the @System.DateTime value. In addition, the value of the variables is updated in the **Autos** and **Locals** windows.

   ![Autos window and Immediate Window](./media/debugging-with-visual-studio/vb-autosimmediate.png)
-->
---

1. 选择工具栏中的“继续”按钮，或选择“调试” > “继续”菜单项，继续执行程序。 控制台窗口中显示的值对应于在“即时窗口”中所做的更改。

   ![控制台窗口，在“What is your name?”提示下显示键入的值 Jack，后跟“Hello Gracie on 11/1/2016 at 11:59am”](./media/debugging-with-visual-studio/changed.png)

1. 按任意键，退出应用程序并结束调试模式。

## <a name="setting-a-conditional-breakpoint"></a>设置条件断点

程序显示用户输入的字符串。 如果用户没有输入任何内容，情况又如何呢？ 可使用实用的调试功能“条件断点”来测试这种情况，该功能可在满足一个或多个条件时中断程序执行。

若要设置条件断点，并测试用户无法输入字符串时的情况如何，请执行以下操作：

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 右键单击表示断点的红点。 在上下文菜单中，选择“条件”，打开“断点设置”对话框。 选中“条件”对应的框。

   ![断点设置面板](./media/debugging-with-visual-studio/breakpointsettings.png)

1. 对于“条件表达式”，将“e.g. x == 5”替换为以下内容：

   ```csharp
   String.IsNullOrEmpty(name)
   ```
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 右键单击表示断点的红点。 在上下文菜单中，选择“条件”，打开“断点设置”对话框。 选中“条件”对应的框。

   ![断点设置面板](./media/debugging-with-visual-studio/vb-breakpointsettings.png)

1. 对于“条件表达式”，将“e.g. x = 5”替换为以下内容：

   ```vb
   String.IsNullOrEmpty(name)
   ```
---

   要测试的代码条件是 `String.IsNullOrEmpty(name)` 方法调用是否为 `true`，因为 name 尚未分配有值或值为空字符串 ("")。 还可以指定命中次数，这样程序就会在语句的执行次数达到指定值时中断执行；也可以指定筛选条件，这样就可以根据诸如线程标识符、进程名称或线程名称之类的属性来中断程序执行。

1. 选择“关闭”按钮，关闭此对话框。

1. 在调试模式下运行程序。

1. 在控制台窗口中，在看到输入名称的提示时按 Enter 键。

1. 由于符合我们指定的条件（`name` 为 `null` 或 <xref:System.String.Empty?displayProperty=fullName>），因此程序在到达断点时以及在 `Console.WriteLine` 方法执行前停止执行。

1. 选择“局部变量”窗口，其中显示当前正在执行的方法（在此程序中为 `Main` 方法）的局部变量值。 请注意，`name` 变量的值为 `""` 或 <xref:System.String.Empty?displayProperty=fullName>。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 在“即时窗口”中输入下面的语句，确认值为空字符串。 结果为 `true`。

   ```csharp
   ? name == String.Empty
   ```

   ![即时窗口，执行语句后返回值 true](./media/debugging-with-visual-studio/emptystring.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 在“即时窗口”中输入下面的语句，确认值为空字符串。 结果为 `true`。

   ```vb
   ? String.IsNullOrEmpty(name)
   ```
  ![即时窗口，执行语句后返回值 true](./media/debugging-with-visual-studio/vb-emptystring.png)
---

1. 选择工具栏上的“继续”按钮，继续执行程序。

1. 按任意键，关闭控制台窗口并退出调试模式。

1. 单击代码窗口左侧边缘上的点，或选中该行，选择“调试”>“切换断点”菜单项，从而清除断点。

---
## <a name="stepping-through-a-program"></a>单步执行程序

使用 Visual Studio，还可以单步执行程序，并监视其执行情况。 通常可以设置断点，并使用此功能单步执行程序流，尽管是一小部分程序代码。 因为程序很小，因此可以通过执行以下操作来单步执行整个程序：

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 在菜单栏上，选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 会在要执行的下一行旁边突出显示一个箭头。

   ![Visual Studio 窗口](./media/debugging-with-visual-studio/stepinto1.png)

   此时，“自动”窗口显示程序只定义了一个变量，即 `args`。 由于尚未向程序传递任何命令行自变量，因此它的值是一个空字符串数组。 此外，Visual Studio 还打开了一个空白控制台窗口。

1. 选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 现在突出显示要执行的下一行。 如图所示，从上一语句执行到这行代码花费了不到 1 毫秒的时间。 `args` 仍然是唯一声明的变量，控制台窗口仍为空白。

   ![Visual Studio 窗口](./media/debugging-with-visual-studio/stepinto2.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 在菜单栏上，选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 会在要执行的下一行旁边突出显示一个箭头。

   ![Visual Studio 窗口](./media/debugging-with-visual-studio/vb-stepinto1.png)

   此时，由于还没有向程序传递任何命令行参数，因此“自动”窗口显示 `args` 变量的值是一组空字符串。 此外，Visual Studio 还打开了一个空白控制台窗口。

1. 选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 现在突出显示要执行的下一行。 如图所示，从上一语句执行到这行代码花费了不到 1 毫秒的时间。 `args` 仍然是唯一声明的变量，控制台窗口仍为空白。

   ![Visual Studio 窗口](./media/debugging-with-visual-studio/vb-stepinto2.png)
---

1. 选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 突出显示包含 `name` 变量赋值的语句。 “自动”窗口显示 `name` 为 `null`（在 C# 中）或 `Nothing`（在 Visual Basic 中），控制台窗口显示字符串“What is your name?”。

1. 在控制台窗口中输入字符串，然后按 Enter，从而响应提示。 控制台无响应，输入的字符串未显示在控制台窗口中，但 <xref:System.Console.ReadLine%2A?displayProperty=fullName> 方法将捕获输入。

1. 选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 突出显示包含 `date`（在 C# 中）或 `currentDate`（在 Visual Basic 中）变量赋值的语句。 “自动”窗口显示 <xref:System.DateTime.Now?displayProperty=fullName> 属性值以及 <xref:System.Console.ReadLine%2A?displayProperty=fullName> 方法调用返回的值。 控制台窗口还显示你在看到控制台输入提示后输入的字符串。

1. 选择“调试” > “单步执行”，或按 F11 键。 “自动”窗口显示通过 <xref:System.DateTime.Now?displayProperty=fullName> 属性赋值后的 `date` 变量值。 控制台窗口保持不变。

1. 选择“调试” > “单步执行”，或按 F11 键。 Visual Studio 调用 <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=fullName> 方法。 “自动”窗口显示 `date`（或 `currentDate`）和 `name` 变量的值，控制台窗口显示格式化字符串。

1. 选择“调试” > “跳出”，或按 Shift 和 F11 键。 这将停止单步执行。 控制台窗口会显示一条消息，并等待用户按任意键。

1. 按任意键，关闭控制台窗口并退出调试模式。

## <a name="building-a-release-version"></a>生成发布版本

测试应用程序的调试版本后，还应该编译并测试发布版本。 发布版本包含编译器优化，有时可能会对应用程序的行为产生不良影响。 例如，旨在提升性能的编译器优化可能会在异步或多线程应用程序中创建争用条件。

若要生成和测试控制台应用程序的发布版本，请将工具栏上的生成配置从“调试”更改为“发布”。

![Image](./media/debugging-with-visual-studio/toolbar2.png)

按 F5 或选择“生成”菜单中的“生成解决方案”后，Visual Studio 会编译控制台应用程序的发布版本。 可像测试应用程序的调试版本一样测试发布版本。

调试完应用程序后，下一步是发布应用程序的可部署版本。 若要了解如何执行此操作，请参阅[使用 Visual Studio 2017 发布 Hello World 应用程序](./publishing-with-visual-studio.md)。

