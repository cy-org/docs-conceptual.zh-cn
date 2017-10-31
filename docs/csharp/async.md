---
title: "异步编程"
description: "了解 .NET Core 提供的 C# 语言级别异步编程模式。"
keywords: .NET, .NET Core
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b878c34c-a78f-419e-a594-a2b44fa521a4
ms.translationtype: HT
ms.sourcegitcommit: 019461964ba63d874ce86511474aa37b4342bbc4
ms.openlocfilehash: b4a95438fe8b7490337de10299b824c5796bb4d1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---

# <a name="asynchronous-programming"></a>异步编程

如果需要 I/O 绑定（例如从网络请求数据或访问数据库），则需要利用异步编程。  还可以使用 CPU 绑定代码（例如执行成本高昂的计算），对编写异步代码而言，这是一个不错的方案。

C# 拥有语言级别的异步编程模型，它使你能轻松编写异步代码，而无需应付回叫或符合支持异步的库。 它遵循[基于任务的异步模式 (TAP)](https://msdn.microsoft.com/library/hh873175.aspx)。

## <a name="basic-overview-of-the-asynchronous-model"></a>异步模型的基本概述

异步编程的核心是 `Task` 和 `Task<T>` 对象，这两个对象对异步操作建模。  它们受关键字 `async` 和 `await` 的支持。  在大多数情况下模型十分简单： 

对于 I/O 绑定代码，当你 `await` 一个操作，它将返回 `async` 方法中的一个 `Task` 或 `Task<T>`。

对于 CPU 绑定代码，当你 `await` 一个操作，它将在后台线程通过 `Task.Run` 方法启动。

`await` 关键字有这奇妙的作用。 它控制执行 `await` 的方法的调用方，且它最终允许 UI 具有响应性或服务具有灵活性。

除上方链接的 TAP 文章中介绍的 `async` 和 `await` 之外，还有其他处理异步代码的方法，但本文档将在下文中重点介绍语言级别的构造。

### <a name="io-bound-example-downloading-data-from-a-web-service"></a>I/O 绑定示例：从 Web 服务下载数据

你可能需要在按下按钮时从 Web 服务下载某些数据，但不希望阻止 UI 线程。 只需执行如下操作即可轻松实现：

```csharp
private readonly HttpClient _httpClient = new HttpClient();

downloadButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI as the request
    // from the web service is happening.
    //
    // The UI thread is now free to perform other work.
    var stringData = await _httpClient.GetStringAsync(URL);
    DoSomethingWithData(stringData);
};
```

就是这么简单！ 代码表示目的（异步下载某些数据），而不会在与任务对象的交互中停滞。

### <a name="cpu-bound-example-performing-a-calculation-for-a-game"></a>CPU 绑定示例：为游戏执行计算

假设你正在编写一个移动游戏，在该游戏中，按下某个按钮将会对屏幕中的许多敌人造成伤害。  执行伤害计算的开销可能极大，而且在 UI 线程中执行计算有可能使游戏在计算执行过程中暂停！

此问题的最佳解决方法是启动一个后台线程，它使用 `Task.Run` 执行工作，并 `await` 其结果。  这可确保在执行工作时 UI 能流畅运行。

```csharp
private DamageResult CalculateDamageDone()
{
    // Code omitted:
    //
    // Does an expensive calculation and returns
    // the result of that calculation.
}


calculateButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI while CalculateDamageDone()
    // performs its work.  The UI thread is free to perform other work.
    var damageResult = await Task.Run(() => CalculateDamageDone());
    DisplayDamage(damageResult);
};
```

就是这么简单！  此代码清楚地表达了按钮的单击事件的目的，它无需手动管理后台线程，而是通过非阻止性的方式来实现。

### <a name="what-happens-under-the-covers"></a>内部原理

异步操作涉及许多移动部分。  若要了解 `Task` 和 `Task<T>` 的内部原理，请参阅[深入了解异步](../standard/async-in-depth.md)，以获取详细信息。

在 C# 方面，编译器将代码转换为状态机，它将跟踪类似以下内容：到达 `await` 时暂停执行以及后台作业完成时继续执行。

从理论上讲，这是[异步的承诺模型](https://en.wikipedia.org/wiki/Futures_and_promises)的实现。

## <a name="key-pieces-to-understand"></a>需了解的要点

*   异步代码可用于 I/O 绑定和 CPU 绑定代码，但在每个方案中有所不同。
*   异步代码使用 `Task<T>` 和 `Task`，它们是对后台所完成的工作进行建模的构造。
* `async` 关键字将方法转换为异步方法，这使你能在其正文中使用 `await` 关键字。
*   应用 `await` 关键字后，它将挂起调用方法，并将控制权返还给调用方，直到等待的任务完成。
*   仅允许在异步方法中使用 `await`。

## <a name="recognize-cpu-bound-and-io-bound-work"></a>识别 CPU 绑定和 I/O 绑定工作

本指南的前两个示例演示如何将 `async` 和 `await` 用于 I/O 绑定和 CPU 绑定工作。  确定所需执行的操作是 I/O 绑定或 CPU 绑定是关键，因为这会极大影响代码性能，并可能导致某些构造的误用。

以下是编写代码前应考虑的两个问题：

1. 你的代码是否会“等待”某些内容，例如数据库中的数据？

    如果答案为“是”，则你的工作是 **I/O 绑定**。

2. 你的代码是否要执行开销巨大的计算？

    如果答案为“是”，则你的工作是 **CPU 绑定**。
    
如果你的工作为 **I/O 绑定**，请使用 `async` 和 `await`（而不使用 `Task.Run`）。  不应使用任务并行库。  相关原因在[深入了解异步的文章](../standard/async-in-depth.md)中说明。

如果你的工作为 **CPU 绑定**，并且你重视响应能力，请使用 `async` 和 `await`，并在另一个线程上使用 `Task.Run` 生成工作。  如果该工作同时适用于并发和并行，则应考虑使用任务并行库。

此外，应始终对代码的执行进行测量。  例如，你可能会遇到这样的情况：多线程处理时，上下文切换的开销高于 CPU 绑定工作的开销。  每种选择都有折衷，应根据自身情况选择正确的折衷方案。

## <a name="more-examples"></a>更多示例

下列示例演示了多种使用 C# 编写异步代码的方法。  它们涉及你可能会遇到的一些不同方案。

### <a name="extracting-data-from-a-network"></a>从网络提取数据

此代码片段从 www.dotnetfoundation.org 下载 HTML，并对 HTML 中出现字符串“.NET”的次数计数。  它使用 ASP.NET MVC 定义执行此任务的 Web 控制器方法，以便返回数字。

> [!NOTE]
> 如果打算在生产代码中进行 HTML 分析，则不要使用正则表达式。 改为使用分析库。

```csharp
private readonly HttpClient _httpClient = new HttpClient();

[HttpGet]
[Route("DotNetCount")]
public async Task<int> GetDotNetCountAsync()
{
    // Suspends GetDotNetCountAsync() to allow the caller (the web server)
    // to accept another request, rather than blocking on this one.
    var html = await _httpClient.DownloadStringAsync("http://dotnetfoundation.org");

    return Regex.Matches(html, ".NET").Count;
}
```

以下是为通用 Windows 应用编写的相同方案，当按下按钮时，它将执行相同的任务：

```csharp
private readonly HttpClient _httpClient = new HttpClient();

private async void SeeTheDotNets_Click(object sender, RoutedEventArgs e)
{
    // Capture the task handle here so we can await the background task later.
    var getDotNetFoundationHtmlTask = _httpClient.GetStringAsync("http://www.dotnetfoundation.org");

    // Any other work on the UI thread can be done here, such as enabling a Progress Bar.
    // This is important to do here, before the "await" call, so that the user
    // sees the progress bar before execution of this method is yielded.
    NetworkProgressBar.IsEnabled = true;
    NetworkProgressBar.Visibility = Visibility.Visible;

    // The await operator suspends SeeTheDotNets_Click, returning control to its caller.
    // This is what allows the app to be responsive and not hang on the UI thread.
    var html = await getDotNetFoundationHtmlTask;
    int count = Regex.Matches(html, ".NET").Count;

    DotNetCountLabel.Text = $"Number of .NETs on dotnetfoundation.org: {count}";

    NetworkProgressBar.IsEnabled = false;
    NetworkProgressBar.Visbility = Visibility.Collapsed;
}
```

### <a name="waiting-for-multiple-tasks-to-complete"></a>等待多个任务完成

你可能发现自己处于需要并行检索多个数据部分的情况。  `Task` API 包含两种方法（即 `Task.WhenAll` 和 `Task.WhenAny`），这些方法允许你编写在多个后台作业中执行非阻止等待的异步代码。

此示例演示如何为一组 `User` 捕捉 `userId` 数据。

```csharp
public async Task<User> GetUser(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static Task<IEnumerable<User>> GetUsers(IEnumerable<int> userIds)
{
    var getUserTasks = new List<Task<User>>();
    
    foreach (int userId in userIds)
    {
        getUserTasks.Add(GetUser(id));
    }
    
    return await Task.WhenAll(getUserTasks);
}
```

以下是使用 LINQ 进行更简洁编写的另一种方法：

```csharp
public async Task<User> GetUser(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static async Task<User[]> GetUsers(IEnumerable<int> userIds)
{
    var getUserTasks = userIds.Select(id => GetUser(id));
    return await Task.WhenAll(getUserTasks);
}
```
尽管它的代码较少，但在混合 LINQ 和异步代码时需要谨慎操作。  因为 LINQ 使用延迟的执行，因此异步调用将不会像在 `foreach()` 循环中那样立刻发生，除非强制所生成的序列通过对 `.ToList()` 或 `.ToArray()` 的调用循环访问。

## <a name="important-info-and-advice"></a>重要信息和建议

尽管异步编程相对简单，但应记住一些可避免意外行为的要点。

*  `async` **方法需在其主体中具有** `await` **关键字，否则它们将永不暂停！**

这一点需牢记在心。  如果 `await` 未用在 `async` 方法的主体中，C# 编译器将生成一个警告，但此代码将会以类似普通方法的方式进行编译和运行。  请注意这会导致效率低下，因为由 C# 编译器为异步方法生成的状态机将不会完成任何任务。

*   应将“Async”作为后缀添加到所编写的每个异步方法名称中。

这是 .NET 中的惯例，以便更轻松区分同步和异步方法。 请注意，未由代码显式调用的某些方法（如事件处理程序或 Web 控制器方法）并不一定适用。 由于它们未由代码显式调用，因此对其显式命名并不重要。

*   `async void` **应仅用于事件处理程序。**

`async void` 是允许异步事件处理程序工作的唯一方法，因为事件不具有返回类型（因此无法利用 `Task` 和 `Task<T>`）。 其他任何对 `async void` 的使用都不遵循 TAP 模型，且可能存在一定使用难度，例如：

  *   `async void` 方法中引发的异常无法在该方法外部被捕获。
  *   十分难以测试 `async void` 方法。
  *   如果调用方不希望 `async void` 方法是异步方法，则这些方法可能会产生不好的副作用。

*   **在 LINQ 表达式中使用异步 lambda 时请谨慎**

LINQ 中的 Lambda 表达式使用延迟执行，这意味着代码可能在你并不希望结束的时候停止执行。 如果编写不正确，将阻塞任务引入其中时可能很容易导致死锁。 此外，此类异步代码嵌套可能会对推断代码的执行带来更多困难。 Async 和 LINQ 的功能都十分强大，但在结合使用两者时应尽可能小心。

*   **采用非阻止方式编写等待任务的代码**

将阻止当前线程作为等待任务完成的方法可能导致死锁和已阻止的上下文线程，且可能需要更复杂的错误处理。 下表提供了关于如何以非阻止方式处理等待任务的指南：

| 使用以下方式... | 而不是… | 若要执行此操作 |
| --- | --- | --- |
| `await` | `Task.Wait` 或 `Task.Result` | 检索后台任务的结果 |
| `await Task.WhenAny` | `Task.WaitAny` | 等待任何任务完成 |
| `await Task.WhenAll` | `Task.WaitAll` | 等待所有任务完成 |
| `await Task.Delay` | `Thread.Sleep` | 等待一段时间 |

*   **编写状态欠缺的代码**

请勿依赖全局对象的状态或某些方法的执行。 请仅依赖方法的返回值。 为什么？

  *   这样更容易推断代码。
  *   这样更容易测试代码。
  *   混合异步和同步代码更简单。
  *   通常可完全避免争用条件。
  *   通过依赖返回值，协调异步代码可变得简单。
  *   （好处）它非常适用于依赖关系注入。

建议的目标是实现代码中完整或接近完整的[引用透明度](https://en.wikipedia.org/wiki/Referential_transparency_%28computer_science%29)。 这么做能获得高度可预测、可测试和可维护的基本代码。

## <a name="other-resources"></a>其他资源

* [深入了解异步](../standard/async-in-depth.md)提供了关于任务如何工作的详细信息。
* 由 Lucian Wischik 所著的 [Six Essential Tips for Async](https://channel9.msdn.com/Series/Three-Essential-Tips-for-Async)（关于异步的六个要点）是有关异步编程的绝佳资源

