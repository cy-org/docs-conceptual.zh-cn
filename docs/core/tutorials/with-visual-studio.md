---
title: "使用 Visual Studio 2017 生成 .NET Core C# Hello World 应用程序"
description: "了解如何使用 Visual Studio 2017 生成简单的 C# .NET Core 控制台应用程序。"
keywords: ".NET Core, .NET Core 控制台应用程序, Visual Studio 2017"
author: BillWagner
ms.author: wiwagn
ms.date: 09/13/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 97aa50bf-bdf8-416d-a56c-ac77504c14ea
ms.translationtype: HT
ms.sourcegitcommit: b041fbec3ff22157d00af2447e76a7ce242007fc
ms.openlocfilehash: 86c772bd98978fe06f648eec9ca750b86ab2bfec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/14/2017

---

# <a name="build-a-c-hello-world-application-with-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序

本主题分步介绍了如何使用 Visual Studio 2017 生成、调试和发布简单的 C# .NET Core 控制台应用程序。 Visual Studio 2017 提供了功能全面的开发环境，可用于生成 .NET Core 应用程序。 只要应用程序没有平台专属依赖项，应用程序就可以在 .NET Core 的任何目标平台上和安装了 .NET Core 的任何系统上运行。

## <a name="prerequisites"></a>先决条件

安装了“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/downloads/)。 可以使用 .NET Core 1.1 或 .NET Core 2.0 开发应用程序。

有关详细信息，请参阅 [Windows 上 .NET Core 的先决条件](../../core/windows-prerequisites.md)主题。

## <a name="a-simple-hello-world-application"></a>简单的“Hello World”应用程序

首先创建简单的“Hello World”控制台应用程序。 请执行这些步骤：

1. 启动 Visual Studio 2017。 从菜单栏中选择“文件” > “新建” > “项目”。 在“新项目”*对话框中，依次选择“Visual C#”和“.NET Core”节点。 然后，选择“控制台应用程序(.NET Core)”项目模板。 在“名称”文本框中，键入“HelloWorld”。 选择“确定”按钮。

   ![选择了“控制台应用”的“新建项目”对话框](./media/with-visual-studio/newproject.png)
   
1. Visual Studio 使用模板创建项目。 C# .NET Core 控制台应用程序模板会自动定义类 `Program` 和一个需要将 <xref:System.String> 数组用作自变量的方法 `Main`。 `Main` 是应用程序入口点，同时也是在应用程序启动时由运行时自动调用的方法。 *args* 数组中包含在应用程序启动时提供的所有命令行自变量。

   ![Visual Studio 和新建的 HelloWorld 项目](./media/with-visual-studio/devenv.png)

   用于创建简单的“Hello World”应用程序的模板。 它通过调用 <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> 方法在控制台窗口中 显示文本字符串“Hello World!”。 现在，选择工具栏上含绿色箭头的“HelloWorld”按钮，可以在调试模式下运行程序。 如果这样操作，控制台窗口只在较短的时间内可见，然后就会关闭。 这是因为在执行 `Main` 方法中的单个语句后，`Main` 方法和应用程序将立即终止。

1. 若要在应用程序关闭控制台窗口前将其暂停，请在调用 <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> 方法后立即添加下列代码：

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```
   此代码会提示用户按任意键，然后在用户按键前暂停程序。

1. 在菜单栏中，选择“生成” > “生成解决方案”。 这会将程序编译成一种中间语言 (IL)，然后由实时 (JIT) 编译器转换成二进制代码。

1. 选择工具栏上含绿色箭头的“HelloWorld”按钮，从而运行程序。

   ![控制台窗口，其中显示 Hello World Press any key to continue](./media/with-visual-studio/helloworld1.png)

1. 按任意键关闭控制台窗口。

## <a name="enhancing-the-hello-world-application"></a>改进“Hello World”应用程序

改进应用程序，提示用户输入名字，并将其与日期和时间一同显示。 若要修改和测试程序，请执行以下操作：

1. 在代码窗口中，在 `static void Main(string[] args)` 代码行后面的左括号和第一个右括号之间，输入以下 C# 代码：

   [!code-csharp[GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   此代码替换现有的 <xref:System.Console.WriteLine%2A?displayProperty=fullName>、<xref:System.Console.Write%2A?displayProperty=fullName> 和 <xref:System.Console.ReadKey%2A?displayProperty=fullName> 语句。

   ![Visual Studio Program c-sharp 文件，含更新后 Main 方法](./media/with-visual-studio/codewindow.png)

   此代码在控制台中显示“What is your name?”， 然后等待用户输入字符串并按 Enter 键。 它将此字符串存储到名为 `name` 的变量中。 它还会检索 <xref:System.DateTime.Now?displayProperty=fullName> 属性的值（其中包含当前的本地时间），并将此值赋给 `date` 变量。 最后，使用[内插字符串](../../csharp/language-reference/keywords/interpolated-strings.md)在控制台窗口中显示这些值。

1. 依次选择**“生成”** > **“生成解决方案”**，编译此程序。

1. 选择工具栏上的绿色箭头、按 F5 或选择“调试” > “启动调试”菜单项，在 Visual Studio 的调试模式下运行程序。 出现提示时，输入名称并按 Enter 键。

   ![控制台窗口，含已修改程序的输出](./media/with-visual-studio/helloworld2.png)

1. 按任意键关闭控制台窗口。

现已创建并运行应用程序。 若要开发专业应用程序，仍需要执行一些其他步骤，才可发布应用程序：

- 有关调试应用程序的信息，请参阅[使用 Visual Studio 2017 调试 C# Hello World 应用程序](debugging-with-visual-studio.md)。

- 若要了解如何开发和发布可发行版应用程序，请参阅[使用 Visual Studio 2017 发布 C# Hello World 应用程序](publishing-with-visual-studio.md)。

## <a name="related-topics"></a>相关主题

还可以使用 Visual Studio 2017 生成 .NET Core 类库，而不是控制台应用程序。 有关分步说明，请参阅[使用 Visual Studio 2017 生成 C# .NET Core 类库](library-with-visual-studio.md)。

还可以使用 [Visual Studio Code](https://code.visualstudio.com/)（可供下载的代码编辑器）开发在 Mac、Linux 和 Windows 上运行的 .NET Core 控制台应用。 有关分步教程，请参阅 [Visual Studio Code 入门](with-visual-studio-code.md)。

