---
title: "控制台应用程序"
description: "此教程将介绍 .NET Core 和 C# 语言的许多功能。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 883cd93d-50ce-4144-b7c9-2df28d9c11a0
ms.translationtype: Human Translation
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 360e93af03e00547116d1af1816c2b9b29524881
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="console-application"></a>控制台应用程序

## <a name="introduction"></a>介绍
此教程将介绍 .NET Core 和 C# 语言的许多功能。 你将了解：
*   .NET Core 命令行接口 (CLI) 的基础知识
*   C# 控制台应用程序的结构
*   控制台 I/O
*   .NET Core 中文件 I/O API 的基础知识
*   .NET Core 中任务异步编程模型的基础知识

你将生成一个应用程序，用于读取文本文件，然后将文本文件的内容回显到控制台。 将按配速大声朗读控制台输出。 可以按“<”或“>”键加速或减速显示。

此教程将介绍许多功能。 我们将逐个生成这些功能。 
## <a name="prerequisites"></a>先决条件
必须将计算机设置为运行 .Net Core。 有关安装说明，请访问 [.NET Core](https://www.microsoft.com/net/core) 页。 可以在 Windows、Linux、macOS 或 Docker 容器中运行此应用程序。 必须安装常用的代码编辑器。 
## <a name="create-the-application"></a>创建应用程序
第一步是新建应用程序。 打开命令提示符，然后新建应用程序的目录。 将新建的目录设为当前目录。 在命令提示符处，键入命令 `dotnet new console`。 这将为基本的“Hello World”应用程序创建起始文件。

在开始进行修改之前，我们先来逐步了解一下如何运行简单的 Hello World 应用程序。 创建应用程序之后，在命令提示符处键入 `dotnet restore`。 此命令将运行 NuGet 包还原进程。 NuGet 是 .NET 程序包管理器。 此命令会下载项目缺少的所有依赖项。 由于这是一个新项目，尚无任何依赖项，因此首次运行只会下载 .NET Core 框架。 执行这一初始步骤后，只需运行 `dotnet restore`，即可添加新的依赖项包，或更新任意依赖项的版本。 此进程还会在项目目录中创建项目锁定文件 (project.lock.json)。 此文件有助于管理项目依赖项。 其中包含所有项目依赖项的本地位置。 无需将文件置于源控件中；它将在 `dotnet restore` 运行时生成。 

还原包后，运行 `dotnet build`。 这将运行生成引擎，并创建应用程序可执行文件。 最后，执行 `dotnet run` 来运行应用程序。  

简单的 Hello World 应用程序代码全都在 Program.cs 中。 使用常用文本编辑器打开此文件。 我们将执行首轮更改。
在此文件的最上面，你会看到 using 语句：

```csharp
using System;
```

此语句指示编译器，`System` 命名空间中的任何类型都在范围内。 与你可能用过的其他面向对象的语言一样，C# 也使用命名空间来整理类型。 此 hello world 程序也一样。 你可以看到，此程序封闭在 `ConsoleApplication` 命名空间内。 这不是很具描述性的名称，因此将其更改为 `TeleprompterConsole`：

```csharp
namespace TeleprompterConsole
```

## <a name="reading-and-echoing-the-file"></a>读取和回显文件
要添加的第一项功能是读取文本文件，然后在控制台中显示全部文本。 首先，让我们来添加文本文件。 将此[示例](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/console-teleprompter)的 GitHub 存储库中的 [sampleQuotes.txt](https://raw.githubusercontent.com/dotnet/docs/master/samples/csharp/getting-started/console-teleprompter/sampleQuotes.txt) 文件复制到项目目录中。 这将用作应用程序脚本。 如果需要有关如何下载本主题示例应用的信息，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)主题中的说明。

接下来，在 Program 类中添加以下方法（就在 `Main` 方法的下方）：

```csharp
static IEnumerable<string> ReadFrom(string file)
{
    string line;
    using (var reader = File.OpenText(file))
    {
        while ((line = reader.ReadLine()) != null)
        {
            yield return line;
        }
    }
}
```

此方法使用两个新命名空间中的类型。 为了让编译能够顺利进行，需要在文件的最上面添加以下两行代码：

```csharp
using System.Collections.Generic;
using System.IO;
```

`IEnumerable<T>` 接口是在 `System.Collections.Generic` 命名空间中进行定义。 @System.IO.File 类是在 `System.IO` 命名空间中进行定义。

这是一种称为*枚举器方法*的特殊类型 C# 方法。 枚举器方法返回延迟计算的序列。 也就是说，序列中的每一项是在使用序列的代码提出请求时生成。 枚举器方法包含一个或多个 `yield return` 语句。 `ReadFrom` 方法返回的对象包含用于生成序列中所有项的代码。 在此示例中，这涉及读取源文件中的下一行文本，然后返回相应的字符串。 每当调用代码请求生成序列中的下一项时，代码就会读取并返回文件中的下一行文本。 读取完整个文件时，序列会指示没有其他项了。

还有两个 C# 语法元素你可能是刚开始接触。 此方法中的 `using` 语句用于管理资源清除。 `using` 语句中初始化的变量（在此示例中，为 `reader`）必须实现 `IDisposable` 接口。 @System.IDisposable 接口定义了一个方法 `Dispose`，应在释放资源时调用此方法。 当快执行到 `using` 语句的右大括号时，编译器会生成此调用。 编译器生成的代码可确保资源得到释放，即使代码块中用 using 语句定义的代码抛出异常，也不例外。

`reader` 变量是使用 `var` 关键字进行定义。 `var` 定义的是*隐式类型局部变量*。 也就是说，变量的类型是由分配给变量的对象的编译时类型决定的。 此处，即为 @System.IO.StreamReader 对象 @System.IO.File.OpenText 的返回值。
 
现在，让我们在 `Main` 方法中填充用于读取文件的代码： 

```csharp
var lines = ReadFrom("sampleQuotes.txt");
foreach (var line in lines)
{
    Console.WriteLine(line); 
}
```

使用 `dotnet run` 运行程序，可以看到控制台中打印输出所有文本行。  

## <a name="adding-delays-and-formatting-output"></a>添加延迟和设置输出格式
现在的问题是，输出显示过快，无法大声朗读。 此时，需要为输出添加延迟。 首先，将生成一些可实现异步处理的核心代码。 不过，在执行这些初始步骤时，将遵循一些反面模式。 反面模式会在你添加代码时在注释中指出，代码将在后面的步骤中进行更新。

这部分包含两步操作。 首先，将迭代器方法更新为返回单个字词，而不是整行文本。 为此，执行下面这些修改。 用以下代码替换 `yield return line;` 语句：

```csharp
var words = line.Split(' ');
foreach (var word in words)
{
    yield return word + " ";
}
yield return Environment.NewLine;
```

接下来，需要修改对文件行的使用方式，并在写入每个字词后添加延迟。 用以下代码块替换 `Main` 方法中的 `Console.WriteLine(line)` 的语句：

```csharp
Console.Write(line);
if (!string.IsNullOrWhiteSpace(line))
{
    var pause = Task.Delay(200);
    // Synchronously waiting on a task is an
    // anti-pattern. This will get fixed in later
    // steps.
    pause.Wait();
}
```

由于 `Task` 类位于 `System.Threading.Tasks` 命名空间中，因此需要在文件的最上面添加 `using` 语句：

```csharp
using System.Threading.Tasks;
```

运行此示例并检查输出。 现在，每打印输出一个字词后，就会有 200 毫秒的延迟。 不过，显示的输出反映出一些问题，因为源文本文件有好几行都超过 80 个字符，且没有换行符。 很难滚动读取这些文本。 此问题很容易解决。 只需跟踪每行长度，然后在行长度达到特定阈值时生成新的一行即可。 在 `words` 声明后声明一个局部变量，用于保存行长度：

```csharp
var lineLength = 0;
```
 
然后，在 `yield return word + " ";` 语句后（在右大括号前）添加以下代码：

```csharp
lineLength += word.Length + 1;
if (lineLength > 70)
{
    yield return Environment.NewLine;
    lineLength = 0;
}
```
 
运行此示例，将能够按预配速大声朗读文本。

## <a name="async-tasks"></a>异步任务
最后一步将是添加代码，以便在一个任务中异步编写输出，同时运行另一任务来读取用户输入（如果用户想要加速或减速文本显示的话）。 此过程分为几步操作，最后将完成所需的全部更新。
第一步是创建异步 @System.Threading.Tasks.Task 返回方法，用于表示已创建的用于读取和显示文件的代码。

将以下方法（截取自 `Main` 方法主体）添加到 `Program` 类中：

```csharp
private static async Task ShowTeleprompter()
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var line in words)
    {
        Console.Write(line);
        if (!string.IsNullOrWhiteSpace(line))
        {
            await Task.Delay(200);
        }
    }
}
```

你会注意到两处更改。 首先，此版本在方法主体中使用 `await` 关键字，而不是调用 @System.Threading.Tasks.Task.Wait 同步等待任务完成。 为此，需要将 `async` 修饰符添加到方法签名中。 此方法返回 `Task`。 请注意，没有用于返回 `Task` 对象的返回语句。 相反，`Task` 对象由编译器在你使用 `await` 运算符时生成的代码进行创建。 可以想象，此方法在到达 `await` 时返回。 返回的 `Task` 指示工作未完成。
在等待的任务完成时，此方法继续执行。 执行完后，返回的 `Task` 会指示已完成。
调用代码可以通过监视返回的 `Task` 来确定完成时间。

可以在 `Main` 方法中调用以下新方法：

```csharp
ShowTeleprompter().Wait();
```

此时，在 `Main` 中，代码确实是同步等待。 应尽可能使用 `await` 运算符，而不是采用同步等待的方式。 不过，在控制台应用程序的 `Main` 方法中，不能使用 `await` 运算符。 这会导致应用程序在所有任务完成前退出。

接下来，需要编写第二个异步方法，从控制台读取键，并监视“<”和“>”键。 下面是为此任务添加的方法：

```csharp
private static async Task GetInput()
{
    var delay = 200;
    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
            {
                delay -= 10;
            }
            else if (key.KeyChar == '<')
            {
                delay += 10;
            }
        } while (true);
    };
    await Task.Run(work);
}
```

这创建了一个表示 @System.Action 委托的 lambda 表达式，用于在用户按“<”或“>”键时，从控制台读取键，并修改表示延迟的局部变量。 此方法使用 @System.Console.ReadKey 来阻止并等待用户按键。

若要完成这项功能，需要新建 `async Task` 返回方法，用于启动这两项任务（`GetInput` 和 `ShowTeleprompter`），并管理这两项任务之间共享的数据。
 
是时候创建一个类来处理这两项任务之间共享的数据了。 此类包含两个公共属性，即延迟和指示已读取完整个文件的标志：

```csharp
namespace TeleprompterConsole
{
    internal class TelePrompterConfig
    {
        private object lockHandle = new object();
        public int DelayInMilliseconds { get; private set; } = 200;

        public void UpdateDelay(int increment) // negative to speed up
        {
            var newDelay = Min(DelayInMilliseconds + increment, 1000);
            newDelay = Max(newDelay, 20);
            lock (lockHandle)
            {
                DelayInMilliseconds = newDelay;
            }
        }
    }
}
```

将此类放入新文件，并将此类封闭在 `TeleprompterConsole` 命名空间中，如上所示。 还需要添加 `using static` 语句，以便可以引用 `Min` 和 `Max` 方法，而无需使用封闭类或命名空间名称。 `using static` 语句从一个类导入方法。 这与一直使用的 `using` 语句相反，后者导入命名空间中的所有类。

```csharp
using static System.Math;
```

新增的另外一项语言功能是 `lock` 语句。 此语句可确保相应代码在任何给定时间都只有一个线程。 如果一个线程处于锁定分区，那么其他线程必须等待第一个线程退出锁定分区。 `lock` 语句使用可监视锁定分区的对象。 此类遵循在类中锁定私有对象的标准惯用做法。

接下来，需要将 `ShowTeleprompter` 和 `GetInput` 方法更新为使用新的 `config` 对象。 编写最后一个 `Task` 返回 `async` 方法，用于启动这两项任务，并在第一项任务完成时退出：

```csharp
private static async Task RunTeleprompter()
{
    var config = new TelePrompterConfig();
    var displayTask = ShowTeleprompter(config);

    var speedTask = GetInput(config);
    await Task.WhenAny(displayTask, speedTask);
}
```

上面引入的一种新方法是 @System.Threading.Tasks.Task.WhenAny(System.Threading.Tasks.Task[]) 调用。 这会创建 `Task`，只要自变量列表中的任意一项任务完成，它就会完成。

接下来，需要同时将 `ShowTeleprompter` 和 `GetInput` 方法更新为对延迟使用 `config` 对象：

```csharp
private static async Task ShowTeleprompter(TelePrompterConfig config)
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var line in words)
    {
        Console.Write(line);
        if (!string.IsNullOrWhiteSpace(line))
        {
            await Task.Delay(config.DelayInMilliseconds);
        }
    }
    config.SetDone();
}

private static async Task GetInput(TelePrompterConfig config)
{

    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
                config.UpdateDelay(-10);
            else if (key.KeyChar == '<')
                config.UpdateDelay(10);
        } while (!config.Done);
    };
    await Task.Run(work);
}
```

这个新版 `ShowTeleprompter` 在 `TeleprompterConfig` 类中调用新方法。 现在，需要将 `Main` 更新为调用 `RunTeleprompter`（而不是 `ShowTeleprompter`）：

```csharp
RunTeleprompter().Wait();
```

若要完成，需要添加 `SetDone` 方法，并将 `Done` 属性添加到 `TelePrompterConfig` 类中：

```csharp
public bool Done => done;

private bool done;

public void SetDone()
{
    done = true;    
}
```

## <a name="conclusion"></a>结束语
此教程介绍了与处理控制台应用程序相关的许多 C# 语言和 .NET Core 库功能。
可以在此教程的基础上进一步探索语言和本文介绍的类。 你已了解文件和控制台 I/O 的基础知识、基于任务的异步编程模型的阻止性和非阻止性用途、C# 语言介绍、C# 程序的组织结构，以及 .NET Core 命令行接口和工具。
 

