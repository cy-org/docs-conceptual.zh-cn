---
title: "使用 Visual Studio 2017 调用 .NET Core 类库"
description: "了解如何使用 Visual Studio 2017 调用类库中的成员。"
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.translationtype: HT
ms.sourcegitcommit: 1b028e5880f9e57e87c16eabeb442e0a46a369da
ms.openlocfilehash: 38e6c7d8797285abc4eb2e87602cc0bbf46ba590
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---

# <a name="consuming-a-class-library-with-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 调用 .NET Core 类库

如果已按照[使用 Visual Studio 2017 生成 C# .NET Core 类库](./library-with-visual-studio.md)或[使用 Visual Studio 2017 生成 Visual Basic .NET Core 类库](vb-library-with-visual-studio.md)以及[使用 Visual Studio 2017 测试 .NET Core 类库](testing-library-with-visual-studio.md)中的步骤创建并测试类库，并且已生成库的发布版本，下一步就是使其可供调用方使用。 可以通过以下两种方式执行此操作：

* 如果库将供一个解决方案使用（例如，如果它是一个大型应用程序中的组件），可以将其以项目的形式添加到解决方案中。

* 如果类库将供更多调用方使用，可以 NuGet 包的形式分发它。

## <a name="including-a-library-as-a-project-in-a-solution"></a>将类库以项目的形式添加到解决方案中

就像将单元测试和类库添加到同一解决方案中一样，可以将应用程序添加到同一解决方案中。 例如，可在控制台应用程序中使用类库，此应用程序将提示用户输入字符串，并报告第一个字符是否为大写：

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 打开在[使用 Visual Studio 2017 生成 C# .NET Core 类库](./library-with-visual-studio.md)主题中创建的 `ClassLibraryProjects` 解决方案。 在“解决方案资源管理器”中，右键单击“ClassLibraryProjects”解决方案，然后从上下文菜单依次选择“添加” > “新项目”。

1. 在“添加新项目”对话框中，展开“Visual C#”节点，再依次选择“.NET Core”节点和“控制台应用程序(.NET Core)”项目模板。 在“名称”文本框中，键入“ShowCase”，然后选择“确定”按钮。

   ![“添加新项目”对话框](./media/consuming-library-with-visual-studio/addnewproject.png)

1. 在“解决方案资源管理器”****中，右键单击“ShowCase”****项目，在上下文菜单中选择“设为启动项目”。 

   ![ShowCase 上下文菜单](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. 项目一开始无权访问类库。 若要允许项目调用类库中的方法，可以创建对该类库的引用。 在“解决方案资源管理器”中，右键单击 `ShowCase` 项目的“依赖项”节点，并选择“添加引用”。

   ![ShowCase 依赖项上下文菜单](./media/consuming-library-with-visual-studio/addreference.png)

1. 在“引用管理器”对话框中，选择类库项目“StringLibrary”，然后选择“确定”按钮。

   ![引用管理器](./media/consuming-library-with-visual-studio/referencemanager.png)

1. 在“Program.cs”文件的代码窗口中，将所有代码替换为以下代码：

   [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs)]

   此代码使用 [Console.WindowHeight](xref:System.Console.WindowHeight) 属性来确定控制台窗口中的行数。 只要 [Console.CursorTop](xref:System.Console.CursorTop) 属性大于或等于控制台窗口中的行数，此代码就会清除控制台窗口，然后向用户显示消息。

   该程序会提示用户输入字符串。 它会指明字符串是否以大写字符开头。 如果用户没有输入字符串就按 Enter 键，应用程序会终止且控制台窗口会关闭。

1. 必要时，将工具栏更改为编译 `ShowCase` 项目的“调试”版本。 选择“ShowCase”按钮上的绿色箭头，编译并运行程序。

   ![Image](./media/consuming-library-with-visual-studio/toolbar.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 打开在[使用 Visual Studio 2017 生成 Visual Basic .NET Core 类库](vb-library-with-visual-studio.md)主题中创建的 `ClassLibraryProjects` 解决方案。 在“解决方案资源管理器”中，右键单击“ClassLibraryProjects”解决方案，然后从上下文菜单依次选择“添加” > “新项目”。

1. 在“添加新项目”对话框中，展开“Visual Basic”节点，再依次选择“.NET Core”节点和“控制台应用程序(.NET Core)”项目模板。 在“名称”文本框中，键入“ShowCase”，然后选择“确定”按钮。

   ![“添加新项目”对话框](./media/consuming-library-with-visual-studio/vb-addnewproject.png)

1. 在“解决方案资源管理器”****中，右键单击“ShowCase”****项目，在上下文菜单中选择“设为启动项目”。 

   ![ShowCase 上下文菜单](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. 项目一开始无权访问类库。 若要允许项目调用类库中的方法，可以创建对该类库的引用。 在“解决方案资源管理器”中，右键单击 `ShowCase` 项目的“依赖项”节点，并选择“添加引用”。

   ![ShowCase 依赖项上下文菜单](./media/consuming-library-with-visual-studio/addreference.png)

1. 在“引用管理器”对话框中，选择类库项目“StringLibrary”，然后选择“确定”按钮。

   ![引用管理器](./media/consuming-library-with-visual-studio/referencemanager.png)

1. 在“Program.vb”文件的代码窗口中，将所有代码替换为以下代码：

    [!CODE-vb[UsingClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/showcase.vb)]

   此代码使用 [Console.WindowHeight](xref:System.Console.WindowHeight) 属性来确定控制台窗口中的行数。 只要 [Console.CursorTop](xref:System.Console.CursorTop) 属性大于或等于控制台窗口中的行数，此代码就会清除控制台窗口，然后向用户显示消息。

   该程序会提示用户输入字符串。 它会指明字符串是否以大写字符开头。 如果用户没有输入字符串就按 Enter 键，应用程序会终止且控制台窗口会关闭。

1. 必要时，将工具栏更改为编译 `ShowCase` 项目的“调试”版本。 选择“ShowCase”按钮上的绿色箭头，编译并运行程序。

   ![Image](./media/consuming-library-with-visual-studio/toolbar.png)
---

可以按照[使用 Visual Studio 2017 调试 Hello World 应用程序](debugging-with-visual-studio.md)和[使用 Visual Studio 2017 发布 Hello World 应用程序](publishing-with-visual-studio.md)中的步骤操作，调试并发布使用此库的应用程序。

## <a name="distributing-the-library-in-a-nuget-package"></a>以 NuGet 包的形式分发类库

可采用 NuGet 包的形式发布类库，让类库可供更多调用方使用。 Visual Studio 不支持创建 NuGet 包。 若要创建 NuGet 包，请使用 [`dotnet` 命令行实用工具](../../core/tools/dotnet.md)：

1. 打开控制台窗口。 例如，在 Windows 任务栏的“有问题尽管问我”文本框中，输入 `Command Prompt`（或缩写 `cmd`），然后选择“命令提示符”桌面应用或按 Enter（如果已在搜索结果中选中控制台窗口），打开控制台窗口。

1. 转到类库的项目目录。 除非重新配置了典型文件位置，否则文件通常位于 Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary 目录中。 此目录包含源代码和项目文件 StringLibrary.csproj。

1. 发出命令 `dotnet pack --no-build`。 此时，`dotnet` 实用工具会生成一个扩展名为 .nupkg 的包。

   > [!TIP]
   > 如果路径中没有包含 dotnet.exe 的目录，可以通过在控制台窗口中输入 `where dotnet.exe` 来找到它的位置。

若要详细了解如何创建 NuGet 包，请参阅[如何使用跨平台工具创建 NuGet 包](../../core/deploying/creating-nuget-packages.md)。

