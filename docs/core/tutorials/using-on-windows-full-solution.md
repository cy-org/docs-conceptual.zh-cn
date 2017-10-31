---
title: "在 Windows 上，使用 Visual Studio 2017 生成完整的 .NET Core 解决方案"
description: "了解如何在 Windows 上的 Visual Studio 2017 中生成完整的 .NET Core 解决方案。"
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ba7e082c-a7c8-431e-a342-f67734b660f6
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6b164198f5fbbae5ebc6164fc281dd7de8172b70
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="building-a-complete-net-core-solution-on-windows-using-visual-studio-2017"></a>在 Windows 上，使用 Visual Studio 2017 生成完整的 .NET Core 解决方案

Visual Studio 2017 提供用于开发 .NET Core 应用程序的功能全面的开发环境。 本文档中的过程介绍了构建典型的 .NET Core 解决方案所需的步骤，包含可重用库、测试以及使用第三方库。 

## <a name="prerequisites"></a>先决条件

请按照[先决条件页](../windows-prerequisites.md)上的说明更新环境。

## <a name="a-solution-using-only-net-core-projects"></a>仅使用 .NET Core 项目的解决方案

### <a name="writing-the-library"></a>编写库

1. 在 Visual Studio 中，依次选择“文件”、“新建”、“项目”。 在“新建项目”对话框中，展开“Visual C#”节点并选择“.NET Core”节点，然后选择“类库 (.NET Standard)”。 

2. 将项目命名为“Library”，将解决方案命名为“Golden”。 保持选中“为解决方案创建目录”。 单击“确定”。

3. 在“解决方案资源管理器”中，打开“依赖项”节点的上下文菜单，并选择“管理 NuGet 包”。

4. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 浏找到 **Newtonsoft.Json**。 单击“安装”，然后接受许可协议。 现在，包应该在“依赖项/NuGet”下显示并自动还原。

5. 将 `Class1.cs` 文件重命名为 `Thing.cs`。 接受类的重命名。 添加方法：`public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. 在 **“生成”** 菜单上，选择 **“生成解决方案”**。

   应可以准确无误地生成解决方案。

### <a name="writing-the-test-project"></a>编写测试项目

1. 在“解决方案资源管理器”中，打开“解决方案”节点的上下文菜单，然后依次选择“添加”、“新建项目”。 在“新建项目”对话框中的“Visual C#/.NET Core”下选择“单元测试项目 (.NET Core)”。 将它命名为“TestLibrary”，然后单击“确定”。 

2. 在“TestLibrary”项目中，打开“依赖项”节点的上下文菜单，选择“添加引用”。 单击“项目”，然后勾选库项目并单击“确定”。 这会将测试项目中的引用添加到库中。

3. 将 `UnitTest1.cs` 文件重命名为 `LibraryTests.cs` 并接受类重命名。 将 `using Library;` 添加到文件顶部，并将`TestMethod1` 方法替换为以下代码：
    ```csharp
    [TestMethod]
    public void ThingGetsObjectValFromNumber()
    {
        Assert.AreEqual(42, new Thing().Get(42));
    }
    ```

   现在，应该可以生成解决方案了。 
   
4. 在“测试”菜单上，依次选择“Windows”和“测试资源管理器”，将测试资源管理器窗口植入工作区。 几秒钟后，`ThingGetsObjectValFromNumber` 测试应在测试资源管理器中显示。 选择 **“全部运行”**。
   
   测试应该会通过。

### <a name="writing-the-console-app"></a>编写控制台应用

1. 在“解决方案资源管理器”中，打开解决方案的上下文菜单，添加新的**控制台应用 (.NET Core)** 项目。 将其命名为“App”。

2. 在 **App** 项目中，打开“依赖项”节点的上下文菜单，依次选择“添加”**和**“引用”。 

3. 在“引用管理器”对话框中，选中“项目”、“解决方案”节点下的“库”，然后单击“确定”

6. 打开 **App** 节点的上下文菜单，选择“设置为启动项目”。 这确保了按住 F5 或 Ctrl+F5 时可启动控制台应用。

7. 打开 `Program.cs` 文件，将 `using Library;` 指令添加到文件顶部，然后将 `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` 添加到 `Main` 方法。

8. 在刚添加的行后设置一个断点。

9. 按 F5 运行该应用程序。

   应用程序应正确生成并命中断点。 应该也可检查应用程序输出“The answer is 42.”。

