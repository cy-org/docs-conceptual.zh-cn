---
title: "在 macOS 上入门 .NET Core"
description: "本文档提供使用 Visual Studio Code 创建 .NET Core 解决方案的步骤和工作流概述。"
keywords: .NET, .NET Core, Mac, macOS, Visual Studio Code
author: bleroy
ms.author: mairaw
ms.date: 03/23/2017
ms.topic: get-started-article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 8ad82148-dac8-4b31-9128-b0e9610f4d9b
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 54a5078f71c68ce3d35c67b266dc198e123cdf88
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="getting-started-with-net-core-on-macos"></a>在 macOS 上入门 .NET Core

本文档提供为 macOS 创建 .NET Core 解决方案的步骤和工作流概述。 了解到如何通过 [NuGet](https://www.nuget.org/) 创建项目、单元测试、使用调试工具和合并第三方库。

> [!NOTE]
> 本文在 macOS 上使用 [Visual Studio Code](http://code.visualstudio.com)。

## <a name="prerequisites"></a>先决条件

获取 [.NET Core SDK](https://www.microsoft.com/net/core)。 .NET Core SDK 包括最新版本的 .NET Core 框架和运行时。

安装 [Visual Studio Code](http://code.visualstudio.com)。 在本文中，还将安装可提升 .NET Core 开发体验的 Visual Studio Code 扩展。

打开 Visual Studio Code，并按 <kbd>F1</kbd> 打开 Visual Studio Code 面板，从而安装 Visual Studio Code C# 扩展。 键入 ext install ，查看扩展列表。 选择 C# 扩展。 重启 Visual Studio Code 以激活扩展。 有关详细信息，请参阅 [Visual Basic Code C# 扩展文档](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md)。

## <a name="getting-started"></a>入门

在本教程中，将创建三个项目：库项目、对该库项目的测试和使用该库的控制台应用程序。 对于此主题，可以在 GitHub 的 dotnet/docs 存储库中[查看或下载源](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/golden)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

启动 Visual Studio Code。 按 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（反引号）或在菜单中依次选择“视图”>“集成终端”，在 Visual Studio Code 中打开嵌入式终端。 若要在 Visual Studio Code 外部执行操作，仍可以使用资源管理器的“通过命令提示符打开”（在 Mac 或 Linux 上，为“在终端中打开”）命令打开外部 shell。

首先创建一个解决方案文件，它将用作一个或多个 .NET Core 项目的容器。 在终端中，创建 golden 文件夹并将其打开。 此文件夹是解决方案的根目录。 运行 [`dotnet new`](../tools/dotnet-new.md) 命令，创建新的解决方案 golden.sln：

```console
dotnet new sln
```

在 golden 文件夹中，执行下列命令来创建库项目，它将在库文件夹中生成 library.csproj 和 Class1.cs 这两个文件：

```console
dotnet new classlib -o library
```

执行 [`dotnet sln`](../tools/dotnet-sln.md) 命令，将新创建的 library.csproj 添加到解决方案：

```console
dotnet sln add library/library.csproj
```

*library.csproj* 文件包含以下信息：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard1.4</TargetFramework>
  </PropertyGroup>

</Project>
```

库方法以 JSON 格式串行化和反序列化对象。 若要支持 JSON 序列化和反序列化，请添加对 `Newtonsoft.Json` NuGet 包的引用。 `dotnet add` 命令向项目添加新项。 若要添加对 NuGet 包的引用，请使用 [`dotnet add package`](../tools/dotnet-add-package.md) 命令并指定包的名称：

```console
dotnet add library package Newtonsoft.Json
```

这会将 `Newtonsoft.Json` 及其依赖项添加到库项目。 或者，可以手动编辑 library.csproj 文件，并添加以下节点：

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="10.0.1" />
</ItemGroup>
```

执行 [`dotnet restore`](../tools/dotnet-restore.md)，这将还原依赖项，并在库中创建 obj 文件夹，该文件夹中包含三个文件，其中一个是 project.assets.json 文件：

```console
dotnet restore
```

在库文件夹中，将文件 Class1.cs 重命名为 Thing.cs。 将代码替换为以下内容：

```csharp
using static Newtonsoft.Json.JsonConvert;

namespace Library
{
    public class Thing
    {
        public int Get(int left, int right) =>
            DeserializeObject<int>($"{left + right}");
    }
}
```

`Thing` 类包含一个公共方法 `Get`，它返回两个数字的总和，实现方法是将总和转换为字符串，然后反序列化为一个整数。 这将使用大量现代 C# 功能，如[`using static` 指令](../../csharp/language-reference/keywords/using-static.md)、[表达式体成员](../../csharp/whats-new/csharp-7.md#more-expression-bodied-members)和[内插字符串](../../csharp/language-reference/keywords/interpolated-strings.md)。

使用 [`dotnet build`](../tools/dotnet-build.md) 命令生成库。 这将在 golden/library/bin/Debug/netstandard1.4 下生成一个 library.dll 文件：

```console
dotnet build
```

## <a name="create-the-test-project"></a>创建测试项目

生成针对库的测试项目。 在 golden 文件夹中，创建一个新测试项目：

```console
dotnet new xunit -o test-library
```

向解决方案添加测试项目：

```console
dotnet sln add test-library/test-library.csproj
```

在上一节创建的库中添加项目引用，这样编译器就可以查找并使用该库项目。 使用 [`dotnet add reference`](../tools/dotnet-add-reference.md) 命令：

```console
dotnet add test-library/test-library.csproj reference library/library.csproj
```

或者，可以手动编辑 test-library.csproj 文件，并添加以下节点：

```xml
<ItemGroup>
  <ProjectReference Include="..\library\library.csproj" />
</ItemGroup>
```

现已正确配置依赖项，可以开始创建库的测试项目。 打开 *UnitTest1.cs*，用以下代码替代其内容：

```csharp
using Library;
using Xunit;

namespace TestApp
{
    public class LibraryTests
    {
        [Fact]
        public void TestThing() {
            Assert.NotEqual(42, new Thing().Get(19, 23));
        }
    }
}
```

请注意，在首次创建单元测试 (`Assert.NotEqual`) 时，已断言值 42 不等于 19+23（或 42），因此测试将失败。 生成单元测试的一个重要步骤是：使创建的测试最初失败一次，以便确认其逻辑正确无误。

在 golden 文件夹中，执行下列命令：

```console
dotnet restore
dotnet test test-library/test-library.csproj
```

这些命令将以递归形式查找所有项目，以还原依赖项、生成依赖性，并激活 xUnit 测试运行程序以运行测试。 该测试像预期那样失败。

编辑 UnitTest1.cs 文件，将断言从 `Assert.NotEqual` 更改为 `Assert.Equal`。 在 goldden  文件夹中执行下列命令，重新运行测试，此次测试通过：

```console
dotnet test test-library/test-library.csproj
```

## <a name="create-the-console-app"></a>创建控制台应用

通过以下步骤创建的控制台应用依赖于之前创建的库项目，并在运行时调用其库方法。 使用此开发模式，可了解如何创建多个项目的可重用库。

在 golden 文件夹中创建新的控制台应用程序：

```console
dotnet new console -o app
```

向解决方案添加控制台应用项目：

```console
dotnet sln add app/app.csproj
```

运行 `dotnet add reference` 命令，创建库的依赖项：

```console
dotnet add app/app.csproj reference library/library.csproj
```

运行 `dotnet restore`，在解决方案中还原三个对象的依赖项。 打开 program.cs，并使用下列行替换 `Main` 方法中的内容：

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

在 Program.cs 文件顶部添加两个 `using` 指令：

```csharp
using static System.Console;
using Library;
```

执行下列 `dotnet run` 命令，运行可执行文件，其中，`dotnet run` 后的 `-p` 选项用于指定主应用程序的项目。 应用会生成字符串“The answer is 42”。

```console
dotnet run -p app/app.csproj
```

## <a name="debug-the-application"></a>调试应用程序

在 `Main` 方法中的 `WriteLine` 语句处设置一个断点。 要实现此操作，可在光标位于 `WriteLine` 行之上时按 <kbd>F9</kbd> 键，也可在想要设置断点的行的左侧边缘中单击鼠标。 代码行旁边的边缘中将出现一个红色圆圈。 到达断点时，将在执行断点行前停止执行代码。

若要打开“调试器”选项卡，请在 Visual Studio Code 工具栏中选择“调试”图标，再从菜单栏中依次选择“视图”>“调试”，或使用键盘快捷方式 <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>D</kbd>：

![Visual Studio Code 调试程序](./media/using-on-macos/vscodedebugger.png)

按“开始”按钮，在调试器下启动应用程序。 应用开始执行，运行到断点处停止。 单步执行 `Get` 方法，确保已传入正确的参数。 确认答案是 42。

