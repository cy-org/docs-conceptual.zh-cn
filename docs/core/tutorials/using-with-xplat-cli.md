---
title: "使用 CLI 实现 .NET Core 入门"
description: "一个分步教程，演示如何使用 .NET Core 命令行接口 (CLI) 开始在 Windows、Linux 或 macOS 上使用 .NET Core。"
keywords: .NET Core, CLI
author: cartermp
ms.author: mairaw
ms.date: 03/08/2017
ms.topic: get-started-article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 41632e63-d5c6-4427-a09e-51dc1116d45f
ms.translationtype: HT
ms.sourcegitcommit: 2762cdc983465979a530192716c33de7044dd1ed
ms.openlocfilehash: 53894b7548b7bedfe3a980efd53a076c0e4efc7f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/04/2017

---

# <a name="getting-started-with-net-core-on-windowslinuxmacos-using-the-command-line"></a>使用命令行在 Windows/Linux/macOS 上入门 .NET Core

本主题将演示如何使用 .NET Core CLI 工具开始在计算机上开发跨平台应用。

如果熟悉 .NET Core CLI 工具集，请阅读 [.NET Core SDK 概述](../tools/index.md)。

## <a name="prerequisites"></a>先决条件

- [.NET Core SDK 1.0](https://www.microsoft.com/net/download/core)。
- 按需选择的文本编辑器或代码编辑器。

## <a name="hello-console-app"></a>Hello，控制台应用！

可在 dotnet/docs GitHub 存储库[查看或下载示例代码](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/HelloMsBuild)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

打开命令提示符，创建一个名为“Hello”的文件夹。 导航到创建的文件夹，键入下列内容：

```
$ dotnet new console
$ dotnet restore
$ dotnet run
```

让我们进行快速演练：

1. `$ dotnet new console`

   [`dotnet new`](../tools/dotnet-new.md) 会创建一个最新的 `Hello.csproj` 项目文件，其中包含生成控制台应用所必需的依赖项。  它还将创建 `Program.cs`，这是包含应用程序的入口点的基本文件。
   
   `Hello.csproj`：

   [!code[Hello.csproj](../../../samples/core/console-apps/HelloMsBuild/Hello.csproj)]   

   项目文件指定还原依赖项和生成程序所需的一切。

   * `OutputType` 标记指定我们要生成的可执行文件，即控制台应用程序。
   * `TargetFramework` 标记指定要定位的 .NET 实现代码。 在高级方案中，可以指定多个目标框架，并在单个操作中生成所有目标框架。 在本教程中，我们将仅针对 .NET Core 1.0 进行生成。

   `Program.cs`：

   [!code-csharp[Program.cs](../../../samples/core/console-apps/HelloMsBuild/Program.cs)]   

   该程序从 `using System` 开始，这意味着“将 `System` 命名空间中的所有内容都纳入此文件的作用域”。 `System` 命名空间包括基本结构，如 `string` 或数值类型。

   接着定义一个名为 `Hello` 的命名空间。 你可以将其更改为任何你喜欢的名称。 在该命名空间中定义了一个名为 `Program` 的类，其中 `Main` 方法将字符串数组作为其参数。 此数组包含在调用编译的程序时所传递的参数列表。 按照这样，不使用此数组：程序所进行的全部操作就是编写“Hello World!” “Hello World!”。 稍后将对使用此参数的代码进行更改。

2. `$ dotnet restore`

   [`dotnet restore`](../tools/dotnet-restore.md) 调用到 [NuGet](https://www.nuget.org/)（.NET 包管理器）以还原依赖项树。 NuGet 分析 *Hello.csproj* 文件、下载文件中所述的依赖项（或从计算机缓存中获取）并编写 *obj/project.assets.json* 文件。  需要 *project.assets.json* 文件才可进行编译和运行。
   
   *project.assets.json* 文件是 NuGet 依赖项和其他描述应用的信息的持久化完整图片集。  此文件由其他工具（如 [](../tools/dotnet-build.md)[ 和 `dotnet build``dotnet run`](../tools/dotnet-run.md)）读取，让它们可以使用正确的 NuGet 依赖项和绑定解决方法集处理源代码。
   
3. `$ dotnet run`

   [`dotnet run`](../tools/dotnet-run.md) 调用 [`dotnet build`](../tools/dotnet-build.md) 来确保已生成要生成的目标，然后调用 `dotnet <assembly.dll>` 运行目标应用程序。
   
    ```
    $ dotnet run
    Hello World!
    ```

    或者，还可以执行 [`dotnet build`](../tools/dotnet-build.md) 来编译代码，无需运行已生成的控制台应用程序。 这使得编译的应用程序（作为 DLL 文件）可以在 Windows 上使用 `dotnet bin\Debug\netcoreapp1.0\Hello.dll` 运行（将 `/` 用于非 Windows 系统）。 还可以对应用程序指定参数，相关操作将在本主题稍后部分进行介绍。

    ```
    $ dotnet bin\Debug\netcoreapp1.0\Hello.dll
    Hello World!
    ```

    在高级方案中，可以将应用程序作为独立的特定于平台的文件集生成，该应用程序可以在未安装 .NET Core 的计算机上部署或运行。 请参阅 [.NET Core 应用程序部署](../deploying/index.md)了解详细信息。

### <a name="augmenting-the-program"></a>扩充程序

让我们稍微更改一下程序。 Fibonacci 数字很有意思，那么除了使用参数，让我们也来添加 Fibonacci 数字，让运行应用的用户开心一下。

1. 将 *Program.cs* 文件的内容替换为以下代码：

   [!code-csharp[Fibonacci](../../../samples/core/console-apps/fibonacci-msbuild/Program.cs)]   

2. 执行 [`dotnet build`](../tools/dotnet-build.md) 以编译更改。

3. 运行向应用传递参数的程序：

   ```
   $ dotnet run -- John
   Hello John!
   Fibonacci Numbers 1-15:
   1: 0
   2: 1
   3: 1
   4: 2
   5: 3
   6: 5
   7: 8
   8: 13
   9: 21
   10: 34
   11: 55
   12: 89
   13: 144
   14: 233
   15: 377
   ```

就是这么简单！  可以按任意喜欢的方式扩充 `Program.cs`。

## <a name="working-with-multiple-files"></a>使用多个文件

对于简单的一次性程序，使用单个文件即可，但如果要生成更复杂的应用，则项目上可能需要多个源文件。让我们通过缓存一些 Fibonacci 值，基于之前的 Fibonacci 示例来生成这类应用，并添加一些递归特性。 

1. 使用以下代码将新文件添加到名为 *FibonacciGenerator.cs* 的 *Hello* 目录：

   [!code-csharp[Fibonacci 生成器](../../../samples/core/console-apps/FibonacciBetterMsBuild/FibonacciGenerator.cs)]   

2. 更改 *Program.cs* 文件中的 `Main` 方法，以实例化新的类并调用其方法，如下例所示：

   [!code-csharp[新的 Program.cs](../../../samples/core/console-apps/FibonacciBetterMsBuild/Program.cs)]

3. 执行 [`dotnet build`](../tools/dotnet-build.md) 以编译更改。

4. 通过执行 [`dotnet run`](../tools/dotnet-run.md) 来运行应用。 以下是程序输出：

   ```
   0
   1
   1
   2
   3
   5
   8
   13
   21
   34
   55
   89
   144
   233
   377
   ```

就是这么简单！ 现在，可以开始使用此处学到的基本概念来创建自己的程序了。

请注意，本教程中用来运行应用程序的命令和步骤仅用于开发过程。 准备好部署应用后，需要查看适用于 .NET Core 应用的不同[部署策略](../deploying/index.md)和 [`dotnet publish`](../tools/dotnet-publish.md) 命令。

## <a name="see-also"></a>另请参阅

[使用 .NET Core CLI 工具组织和测试项目](testing-with-cli.md)

