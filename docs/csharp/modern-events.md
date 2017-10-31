---
title: "更新的 .NET Core 事件模式"
description: "了解 .NET Core 事件模式如何通过向后兼容性实现灵活性，以及如何通过异步订阅服务器实现安全事件处理。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 9aa627c3-3222-4094-9ca8-7e88e1071e06
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: cf69cbe0a7adbd274d1cb9e9544dda77d9fa1740
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="the-updated-net-core-event-pattern"></a>更新的 .NET Core 事件模式

[上一篇文章](event-pattern.md)

上一篇文章讨论了最常见的事件模式。 .NET Core 的模式较为宽松。 在此版本中，`EventHandler<TEventArgs>` 定义不再要求 `TEventArgs` 必须是派生自 `System.EventArgs` 的类。

这就提高了灵活性，并且还具有后向兼容性。 首先讨论灵活性。 类 System.EventArgs 引入了一个方法 `MemberwiseClone()`，该方法可创建对象的浅表副本。
对于任何派生自 `EventArgs` 的类，该方法必须使用反射才能实现其功能。 该功能在特定的派生类中更容易创建。 实际上，这意味着派生自 System.EventArgs 的类会限制你的设计，且不会为你提供任何附加好处。
其实，你可以更改 `FileFoundArgs` 和 `SearchDirectoryArgs` 的定义，使它们不从 `EventArgs` 派生。
该程序的工作原理相同。

如果还要进行一处更改，还可将 `SearchDirectoryArgs` 更改为结构：

```csharp  
internal struct SearchDirectoryArgs  
{  
    internal string CurrentSearchDirectory { get; }  
    internal int TotalDirs { get; }  
    internal int CompletedDirs { get; }  
    
    internal SearchDirectoryArgs(string dir, int totalDirs, 
        int completedDirs) : this()  
    {  
        CurrentSearchDirectory = dir;  
        TotalDirs = totalDirs;  
        CompletedDirs = completedDirs;  
    }  
}  
```   

这一额外更改就是在进入初始化所有字段的构造函数之前调用默认构造函数。 若没有此添加，C# 规则将报告先访问属性再分配属性。

不应将 `FileFoundArgs` 从类（引用类型）更改为结构（值类型）。 这是因为处理取消的协议要求通过引用传递事件参数。 如果进行了相同的更改，文件搜索类将永远不会观察到任何事件订阅者所做的任何更改。 结构的新副本将用于每个订阅者，并且该副本将与文件搜索对象所看到的不同。

接下来，让我们考虑这种更改如何具有后向兼容性。
删除约束不会影响任何现有代码。 任何现有的事件参数类型仍然派生自 `System.EventArgs`。
它们将继续从 `System.EventArgs` 派生，其中一个主要原因就是后向兼容性。 任何现有的事件订阅者都是遵循经典模式的事件的订阅者。

遵循类似的逻辑，现在创建的任何事件参数类型在任何现有代码库中都不会有任何订阅者。 只有从 `System.EventArgs` 派生的新事件类型才会破坏这些代码库。

## <a name="events-with-async-subscribers"></a>异步事件订阅者

你还需了解最后一个模式：如何正确编写调用异步代码的事件订阅者。 该问题详见 [async 和 await](async.md) 一文。 异步方法可具有一个 void 返回类型，但强烈建议不要使用它。 事件订阅者代码调用异步方法时，只能创建 `async void` 方法。 事件处理程序签名需要该方法。

你需要协调此对立指南。 不管怎样，必须创建安全的 `async void` 方法。 需要实现的模式的基础知识如下：

```csharp
worker.StartWorking += async (sender, eventArgs) =>
{
    try 
    {
        await DoWorkAsync();
    }
    catch (Exception e)
    {
        //Some form of logging.
        Console.WriteLine($"Async task failure: {e.ToString()}");
        // Consider gracefully, and quickly exiting.
    }
};
```

首先请注意，处理程序已被标记为异步处理程序。 因为它将被分配给一个事件处理程序委托类型，所以它将有一个 void 返回类型。 这意味着必须遵循处理程序中显示的模式，并且不允许在异步处理程序上下文之外引发异常。 因为它不返回任务，所以没有任何可通过进入故障状态报告错误的任务。 因为方法是异步的，所以不能简单地引发异常。 （调用方法已继续执行，因为它是 `async`。）对于不同的环境，实际的运行时行为将有不同的定义。 它可能会终止线程或程序，或可能使程序处于未确定状态。 这些都不是好的结果。

这就是为什么你应该在自己的 try 块中包装异步任务的 await 语句。 如果它的确导致任务出错，则可以记录该错误。 如果它是应用程序无法从中恢复的错误，则可以迅速优雅地退出此程序。

这些就是 .NET 事件模式的主要更新。 你将在所使用的库中看到许多早期版本的示例。 但是，你也应了解最新的模式是什么。

本系列的下一篇文章将有助于你区分在设计中使用 `delegates` 和 `events`。 它们是类似的概念，该文章将帮助你为程序做出最好的决定。

[下一篇](distinguish-delegates-events.md)

