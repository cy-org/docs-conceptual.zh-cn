---
title: "线程同步 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: e42b1be6-c93c-479f-a148-be0759f1a4e1
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: df4093d4bf777f904aa8ce376cd164ed822350a0
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="thread-synchronization-c"></a>线程同步 (C#)
以下各节中描述的功能和类可用于同步访问多线程应用程序中的资源。  
  
 在应用程序中使用多线程的好处之一是每个线程都可以异步方式执行。 对于 Windows 应用程序，这允许在后台执行耗时的任务，同时应用程序窗口和控件保持响应状态。 对于服务器应用程序，多线程处理提供了用不同线程处理每个传入请求的能力。 否则，在满足上一个请求之前，将无法处理任何新请求。  
  
 然而，线程的异步性质意味着必须协调对文件句柄、网络连接和内存等资源的访问。 否则，两个或多个线程可能在同一时间访问同一资源，且不能感知对方的操作。 结果是不可预知的数据损坏。  
  
 对于针对整数数据类型的简单操作，可以通过 <xref:System.Threading.Interlocked> 类的成员完成同步处理线程。 对于其他所有数据类型和非线程安全资源，只有使用本主题中的构造才能安全地执行多线程处理。  
  
 有关多线程编程中的背景信息，请参阅：  
  
-   [托管线程处理基本知识](../../../../standard/threading/managed-threading-basics.md)  
  
-   [使用线程和线程处理](../../../../standard/threading/using-threads-and-threading.md)  
  
-   [托管线程处理的最佳做法](../../../../standard/threading/managed-threading-best-practices.md)  
  
## <a name="the-lock-keyword"></a>lock 关键字  
 C# `lock` 语句可用于确保代码块运行完成，且不会被其他线程中断。 这是通过在代码块的持续时间内获得给定对象的互斥锁来实现的。  
  
 `lock` 语句被作为参数赋予对象，而且后面跟随的是一次只能由一个线程运行的代码块。 例如：  
  
```csharp  
public class TestThreading  
{  
    private System.Object lockThis = new System.Object();  
  
    public void Process()  
    {  
  
        lock (lockThis)  
        {  
            // Access thread-sensitive resources.  
        }  
    }  
  
}  
```  
  
 提供给 `lock` 关键字的参数必须是基于引用类型的对象，并且用于定义锁的范围。 在上例中，锁定范围仅限于此函数，因为函数外不存在 `lockThis` 对象的任何引用。 如果存在此类引用，锁定范围将扩展到该对象。 严格地说，所提供的对象仅用于唯一标识在多个线程之间共享的资源，因此它可以是任意类实例。 但实际上，该对象通常表示需要线程同步的资源。 例如，如果某个容器对象要被多个线程使用，则可以将该容器传递给锁，而锁后面的同步代码块可访问该容器。 只要其他线程在访问该容器前先锁定该容器，对该对象的访问就是安全同步的。  
  
 通常情况下，最好避免锁定 `public` 类型，或者锁定超出应用程序控制的对象实例。 例如，如果可以公开访问实例，则 `lock(this)` 可能会有问题，因为超出控制范围的代码也可能锁定对象。 这可能会导致死锁情况，即两个或多个线程等待同一对象的释放。 出于相同原因，锁定与对象相对的公共数据类型也可能会导致问题。 锁定文本字符串尤其危险，因为文本字符串被公共语言运行时 (CLR) *暂存*。 这意味着对于整个程序，任何给定字符串文本都只有一个实例，就是这同一个对象表示了所有运行的应用程序域的所有线程中的该文本。 因此，在应用程序进程中任何位置锁定具有相同内容的字符串都会锁定应用程序中该字符串的所有实例。 因此，最好锁定未被暂存的私有或受保护的成员。 某些类提供专用于锁定的成员。 例如，<xref:System.Array> 类型提供 <xref:System.Array.SyncRoot%2A>。 许多集合类型也提供了 `SyncRoot` 成员。  
  
 有关 `lock` 语句的详细信息，请参阅下列主题：  
  
-   [lock 语句](../../../../csharp/language-reference/keywords/lock-statement.md)  
  
-   @System.Threading.Monitor  
  
## <a name="monitors"></a>监视器  
 与 `lock` 关键字类似，监视器可防止多个线程同时执行代码块。 <xref:System.Threading.Monitor.Enter%2A> 方法允许有且只有一个线程继续执行下面的语句；执行线程调用 <xref:System.Threading.Monitor.Exit%2A> 之前，将阻止其他所有线程。 这与使用 `lock` 关键字类似。 例如:   
  
```csharp  
lock (x)  
{  
    DoSomething();  
}  
```  
  
 这等效于：  
  
```csharp  
System.Object obj = (System.Object)x;  
System.Threading.Monitor.Enter(obj);  
try  
{  
    DoSomething();  
}  
finally  
{  
    System.Threading.Monitor.Exit(obj);  
}  
```  
  
 使用 `lock` 关键字通常优先于直接使用 <xref:System.Threading.Monitor> 类，因为 `lock` 更简洁，而且即使在受保护的代码引发异常时，`lock` 也可确保基础监视器被释放。 这通过由 `finally` 关键字完成，该关键字执行其关联的代码块，不会受是否引发异常的影响。  
  
## <a name="synchronization-events-and-wait-handles"></a>同步事件和等待句柄  
 使用锁或监视器有助于防止同时执行线程敏感的代码块，但这些构造不允许在线程之间传达事件。 这就需要“同步事件”，它们是具有两种状态之一（发出信号和未发出信号）的对象，可用于激活和挂起线程。 线程可以通过等待未发出信号的同步事件来挂起，并且可以通过将事件状态改变为发出信号来激活。 如果某个线程尝试等待已经发出信号的事件，则该线程将继续执行且无延迟。  
  
 存在两种类型的同步事件：<xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.ManualResetEvent>。 它们唯一的差别在于：<xref:System.Threading.AutoResetEvent> 会在启动线程时自动从发出信号的状态更改为未发出信号的状态。 相反，<xref:System.Threading.ManualResetEvent> 允许其信号状态激活任意数量的线程，且在调用其 <xref:System.Threading.EventWaitHandle.Reset%2A> 方法后，将仅还原到非信号状态。  
  
 可通过调用某个 wait 方法（例如 <xref:System.Threading.WaitHandle.WaitOne%2A>、<xref:System.Threading.WaitHandle.WaitAny%2A> 或 <xref:System.Threading.WaitHandle.WaitAll%2A>）让线程等待事件。 <xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=fullName> 将导致线程等待，直到单个事件进入信号状态，<xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName> 将阻止线程，直到一个或多个指示的事件进入信号状态，<xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName> 将阻止线程，直到所有指示的事件进入信号状态。 调用某一事件的 <xref:System.Threading.EventWaitHandle.Set%2A> 方法时，该事件会进入信号状态。  
  
 在下例中，线程由 `Main` 函数创建和启动。 新线程使用 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法等待事件。 该线程将被挂起，直到由执行 `Main` 函数的主线程对事件发出信号。 事件发出信号后，辅助线程返回。 在这种情况下，因为该事件仅用于激活一个线程，因此可使用 <xref:System.Threading.AutoResetEvent> 或 <xref:System.Threading.ManualResetEvent> 类。  
  
```csharp  
using System;  
using System.Threading;  
  
class ThreadingExample  
{  
    static AutoResetEvent autoEvent;  
  
    static void DoWork()  
    {  
        Console.WriteLine("   worker thread started, now waiting on event...");  
        autoEvent.WaitOne();  
        Console.WriteLine("   worker thread reactivated, now exiting...");  
    }  
  
    static void Main()  
    {  
        autoEvent = new AutoResetEvent(false);  
  
        Console.WriteLine("main thread starting worker thread...");  
        Thread t = new Thread(DoWork);  
        t.Start();  
  
        Console.WriteLine("main thread sleeping for 1 second...");  
        Thread.Sleep(1000);  
  
        Console.WriteLine("main thread signaling worker thread...");  
        autoEvent.Set();  
    }  
}  
```  
  
## <a name="mutex-object"></a>Mutex 对象  
 *mutex* 与监视器相似；它防止多个线程在某一时间同时执行某个代码块。 事实上，名称“mutex”是术语“互相排斥 (mutually exclusive)”的缩写形式。 但是，与监视器不同，mutex 可用于进程间的同步线程。 mutex 由 <xref:System.Threading.Mutex> 类表示。  
  
 当用于进程间同步时，mutex 称为“命名 mutex”，因为它将在另一个应用程序中使用，因此它不能通过全局变量或静态变量共享。 必须为其提供一个名称，以便两个应用程序能够访问同一个 mutex 对象。  
  
 虽然 mutex 可用于进程内线程同步，但通常首选使用 <xref:System.Threading.Monitor>，因为监视器是为 .NET Framework 专门设计的，因此可以更好地利用资源。 与此相反，<xref:System.Threading.Mutex> 类是 Win32 构造的包装器。 虽然它比监视器更强大，但 mutex 需要互操作过渡，其计算成本比 <xref:System.Threading.Monitor> 类所需的成本更多。 有关使用 mutex 的示例，请参阅 [Mutexes](../../../../standard/threading/mutexes.md)。  
  
## <a name="interlocked-class"></a>Interlocked 类  
 可以使用 <xref:System.Threading.Interlocked> 类的方法来防止多个线程尝试同时更新或比较相同值时可能发生的问题。 该类的方法可从任何线程安全地递增、递减、交换和比较值。  
  
## <a name="readerwriter-locks"></a>ReaderWriter 锁  
 在某些情况下，建议仅在写入数据时锁定资源，并允许多个客户端在数据未更新时同时读取数据。 当线程正在修改资源时，<xref:System.Threading.ReaderWriterLock> 类强制执行对资源的独占访问，但在读取资源时允许非独占访问。 ReaderWriter 锁可用于代替排它锁。使用排它锁时，即使其他线程不需要更新数据，也会导致其他线程等待。  
  
## <a name="deadlocks"></a>死锁  
 线程同步在多线程应用程序中非常有用，但是产生 `deadlock` 总是十分危险。一旦产生了死锁，将有多个线程互相等待，从而导致应用程序暂停。 死锁类似于汽车停在十字路口一样，每个人都在等待别人先出发。 因此，避免死锁很重要；关键是要仔细规划。 开始编码之前，通常可以通过绘制多线程应用程序来预测死锁情况。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Thread>   
 <xref:System.Threading.WaitHandle.WaitOne%2A>   
 <xref:System.Threading.WaitHandle.WaitAny%2A>   
 <xref:System.Threading.WaitHandle.WaitAll%2A>   
 <xref:System.Threading.Thread.Join%2A>   
 <xref:System.Threading.Thread.Start%2A>   
 <xref:System.Threading.Thread.Sleep%2A>   
 <xref:System.Threading.Monitor>   
 <xref:System.Threading.Mutex>   
 <xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.Interlocked>   
 <xref:System.Threading.WaitHandle>   
 <xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading>   
 <xref:System.Threading.EventWaitHandle.Set%2A>   
 [多线程应用程序 (C#)](../../../../csharp/programming-guide/concepts/threading/multithreaded-applications.md)   
 [lock 语句](../../../../csharp/language-reference/keywords/lock-statement.md)   
 [Mutexes](../../../../standard/threading/mutexes.md)   
 @System.Threading.Monitor   
 [互锁操作](../../../../standard/threading/interlocked-operations.md)   
 [AutoResetEvent](../../../../standard/threading/autoresetevent.md)   
 [为多线程处理同步数据](../../../../standard/threading/synchronizing-data-for-multithreading.md)

