---
title: "Hello World -- 您的第一个程序（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: get-started-article
f1_keywords:
- cs.program
- vs.csharp.startpage.firstapplication
dev_langs:
- CSharp
helpviewer_keywords:
- examples [C#], Hello World
- Hello World example [C#]
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
caps.latest.revision: 39
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: b7cb84362c96dac50ae5136334138b55ed1ce00b
ms.openlocfilehash: 03891f83885cf41ab157ebd78ef7e72767b4b163
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="hello-world----your-first-program-c-programming-guide"></a>Hello World -- 您的第一个程序（C# 编程指南）
以下过程创建传统“Hello World!”程序的 C# 版本。 该程序显示字符串 `Hello World!`  
  
 有关介绍性概念的更多示例，请参阅 [Visual C# 和 Visual Basic 入门](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-and-run-a-console-application"></a>创建并运行控制台应用程序  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” 、“新建” 、“项目” 。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  依次展开“已安装”、“模板”、“Visual C#”，然后选择“控制台应用程序”。  
  
4.  在“名称”框中，指定项目名称，然后选择“确定”按钮。  
  
     新项目将出现在“解决方案资源管理器”中。  
  
5.  如果 Program.cs 未在“代码编辑器”中打开，则在“解决方案资源管理器”中打开“Program.cs”的快捷菜单，然后选择“查看代码”。  
  
6.  将 Program.cs 的内容替换为以下代码。  
  
     [!code-cs[csProgGuide#21](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_1.cs)]  
  
7.  选择 F5 键运行该项目。 将显示包含行 `Hello World!` 的命令提示符窗口  
  
 接下来，将检查此程序的重要部分。  
  
## <a name="comments"></a>注释  
 第一行包含一条注释。 字符 `//` 将该行的其余内容转换为一条注释。  
  
 [!code-cs[csProgGuide#32](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_2.cs)]  
  
 还可以通过将文本块置于 `/*` 和 `*/` 字符之间，禁止对其的注释。 这在下面的示例中显示。  
  
 [!code-cs[csProgGuide#33](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_3.cs)]  
  
## <a name="main-method"></a>Main 方法  
 C# 控制台应用程序必须包含 `Main` 方法，控件在其中开始和结束。 在 `Main` 方法中，可以创建对象并执行其他方法。  
  
 `Main` 方法是驻留在类或结构中的[静态](../../../csharp/language-reference/keywords/static.md)方法。 在上一个“Hello World!” 示例中，该方法驻留在名为 `Hello` 的类中。 可以通过以下方式之一来声明 `Main` 方法：  
  
-   它可返回 `void`。  
  
     [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_4.cs)]  
  
-   还可以返回一个整数。  
  
     [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_5.cs)]  
  
-   无论使用哪种返回类型，它都可以带有参数。  
  
     [!code-cs[csProgGuideMain#19](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_6.cs)]  
  
     - 或 -  
  
     [!code-cs[csProgGuideMain#18](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_7.cs)]  
  
 `Main` 方法中定义的参数 `args` 是一个 `string` 类型的数组，该数组包含用于调用该程序的命令行自变量。 与 C++ 不同的是该数组不包括可执行 (exe) 文件的名称。  
  
 若要深入了解如何使用命令行参数，请参阅 [Main() 和命令行参数](../../../csharp/programming-guide/main-and-command-args/index.md)与[如何：使用命令行创建和使用程序集](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)中的示例。  
  
 在调试模式下运行程序时，对 `Main` 方法末尾处 <xref:System.Console.ReadKey%2A> 的调用可以防止在有可能读取输出内容之前控制台窗口关闭，具体方法是按 F5 键。  
  
## <a name="input-and-output"></a>输入和输出  
 C# 程序通常使用由 .NET Framework 的运行时库提供的输入/输出服务。 语句 `System.Console.WriteLine("Hello World!");` 使用 <xref:System.Console.WriteLine%2A> 方法。 这是运行时库中 <xref:System.Console> 类的输出方法之一。 该方法将在标准输出流中显示其字符串参数，后接新行。 其他 <xref:System.Console> 方法可用于不同的输入和输出操作。 如果程序开头包含 `using System;` 指令，则可以直接使用 <xref:System> 类和方法，而不必进行完全限定。 例如，可以调用 `Console.WriteLine`，而非 `System.Console.WriteLine`：  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_8.cs)]  
  
 [!code-cs[csProgGuide#23](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_9.cs)]  
  
 有关输入/输出方法的详细信息，请参阅 <xref:System.IO>。  
  
## <a name="command-line-compilation-and-execution"></a>命令行编译和执行  
 通过使用命令行 而非 Visual Studio 集成开发环境 (IDE)，可以编译“Hello World!”程序。  
  
#### <a name="to-compile-and-run-from-a-command-prompt"></a>从命令提示符中编译并运行  
  
1.  将上一过程的代码粘贴到任何文本编辑器中，然后将该文件保存为文本文件。 为 `Hello.cs` 文件命名。 C# 源代码文件使用 `.cs` 扩展。  
  
2.  执行以下任一步骤以打开命令提示符窗口：  
  
    -   在 Windows 10 的“开始”菜单上，搜索 `Developer Command Prompt`，然后点击或选择“VS 2017 开发人员命令提示”。  
  
         将出现“开发人员命令提示”窗口。  
  
    -   在 Windows 7 中，打开“启动”菜单，展开当前版本的 Visual Studio 的文件夹，打开“Visual Studio Tools”快捷菜单，然后选择“VS 2017 开发人员命令提示”。  
  
         将出现“开发人员命令提示”窗口。  
  
    -   从标准命令提示符窗口启用命令行生成。  
  
         请参阅[如何：为 Visual Studio 命令行设置环境变量](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。  
  
3.  在命令提示窗口中，导航到包含 `Hello.cs` 文件的文件夹。  
  
4.  输入以下命令以编译 `Hello.cs`。  
  
     `csc Hello.cs`  
  
     如果程序不存在编译错误，系统将创建名为 `Hello.exe` 的可执行文件。  
  
5.  在命令提示窗口中，输入以下命令以运行该程序：  
  
     `Hello`  
  
 有关 C# 编译器及其选项的详细信息，请参阅 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)。
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [在 C# 程序内部](../../../csharp/programming-guide/inside-a-program/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [\<paveover>C# 示例应用程序](http://msdn.microsoft.com/en-us/9a9d7aaa-51d3-4224-b564-95409b0f3e15)   
 [C# 参考](../../../csharp/language-reference/index.md)   
 [Main() 和命令行自变量](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Visual C# 和 Visual Basic 入门](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)

