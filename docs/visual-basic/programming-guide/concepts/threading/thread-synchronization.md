---
title: "线程同步 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 04f485d1-8333-4510-9e72-c334e7427e7e
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ec8fa89c8921eadee428a90971d9ae4ce305a109
ms.lasthandoff: 03/13/2017

---
# <a name="thread-synchronization-visual-basic"></a>线程同步 (Visual Basic)
以下各节描述了功能和可用于同步对多线程应用程序中的资源的访问的类。  
  
 在应用程序中使用多个线程的优势之一在于每个线程以异步方式执行。 对于 Windows 应用程序，这允许耗时的任务可以在应用程序窗口时后台执行，并且控件保持响应状态。 为服务器应用程序，多线程处理提供的功能来处理不同的线程与每个传入请求。 否则，直到上一个请求在完全满足将无法处理每个新请求。  
  
 但是，如文件句柄、 网络连接和内存资源的访问权限的线程表示的异步特性必须协调。 否则，两个或多个线程可能在同一时间，每个不知道对方的操作访问同一资源。 结果是不可预知的数据损坏。  
  
 对于整数数据类型的简单操作，同步线程可以通过实现<xref:System.Threading.Interlocked>类</xref:System.Threading.Interlocked>的成员 对于其他所有数据类型和非线程安全资源，多线程处理只能安全地执行本主题中使用的结构。  
  
 有关多线程编程的背景信息，请参阅︰  
  
-   [托管线程处理基本知识](http://msdn.microsoft.com/library/b2944911-0e8f-427d-a8bb-077550618935)  
  
-   [使用线程和线程处理](http://msdn.microsoft.com/library/9b5ec2cd-121b-4d49-b075-222cf26f2344)  
  
-   [托管线程处理最佳做法](http://msdn.microsoft.com/library/e51988e7-7f4b-4646-a06d-1416cee8d557)  
  
## <a name="the-lock-and-synclock-keywords"></a>Lock 和 SyncLock 关键字  
 Visual Basic`SyncLock`语句可用来确保代码块运行完成，无需中断由其他线程。 通过获取给定对象的互斥锁的代码块的持续时间内完成此操作。  
  
 一个`SyncLock`语句给定对象作为参数，并且后面跟着一次只能由一个线程要执行的代码块。 例如:   
  
```vb  
Public Class TestThreading  
    Dim lockThis As New Object  
  
    Public Sub Process()  
        SyncLock lockThis  
            ' Access thread-sensitive resources.  
        End SyncLock  
    End Sub  
End Class  
```  
  
 参数提供给`SyncLock`关键字必须是基于引用类型的对象，用于定义锁定的范围。 在上面的示例中，锁的范围被限制为此函数因为没有对该对象引用`lockThis`函数外不存在。 如果存在这样的引用一样，锁的范围会扩展到该对象。 严格地说，提供的对象是仅用于唯一标识要在多个线程之间共享，因此它可以是任意类实例的资源。 在实践中，但是，此对象通常表示为哪个线程同步是必不可少的资源。 例如，如果容器对象是由多个线程使用，然后传递容器要锁定，而后面锁的同步的代码块将访问该容器。 只要其他线程锁定在同一个包含然后才能访问它，然后对该对象的访问安全地同步。  
  
 通常情况下，最好避免锁定`public`类型，或在您的应用程序的控制之外的对象实例。 例如，`lockThis`由于受控制的代码可能会锁定对象也可能存在问题，如果该实例可以公开访问。 这可能导致死锁，其中两个或多个线程等待的同一个对象的版本。 出于同一原因，锁定对公共数据类型，而不是一个对象，可能导致问题。 锁定字符串是尤其危险，因为字符串被*暂留*由公共语言运行时 (CLR)。 这意味着没有文字整个程序的任何给定的字符串的一个实例，即完全相同的对象表示在所有文字在所有线程上运行应用程序域。 结果是，锁放置在具有相同的内容的字符串任意位置在应用程序进程锁定应用程序中该字符串的所有实例。 因此，最好锁定不暂留的私有或受保护成员。 某些类提供专门用于锁定的成员。 的<xref:System.Array>类型，例如，提供了<xref:System.Array.SyncRoot%2A>。</xref:System.Array.SyncRoot%2A> </xref:System.Array> 提供了许多集合类型`SyncRoot`以及成员。  
  
 有关详细信息`SyncLock`语句中，请参阅下列主题︰  
  
-   [SyncLock 语句](../../../../visual-basic/language-reference/statements/synclock-statement.md)  
  
-   @System.Threading.Monitor  
  
## <a name="monitors"></a>监视器  
 如`SyncLock`关键字，监视器防止多个线程同时执行代码块。 <xref:System.Threading.Monitor.Enter%2A>方法允许一个且只有一个线程继续执行下面的语句; 所有其他线程被阻塞，直到执行的线程调用<xref:System.Threading.Monitor.Exit%2A>。</xref:System.Threading.Monitor.Exit%2A> </xref:System.Threading.Monitor.Enter%2A> 这就类似于使用`SyncLock`关键字。 例如：  
  
```vb  
SyncLock x  
    DoSomething()  
End SyncLock  
```  
  
 这等效于︰  
  
```vb  
Dim obj As Object = CType(x, Object)  
System.Threading.Monitor.Enter(obj)  
Try  
    DoSomething()  
Finally  
    System.Threading.Monitor.Exit(obj)  
End Try  
```  
  
 使用`SyncLock`关键字优于通常使用<xref:System.Threading.Monitor>类直接，同时由于`SyncLock`更为简洁，而且因为`SyncLock`可确保发布后的基础的监视器，即使受保护的代码将引发异常。</xref:System.Threading.Monitor> 完成此操作`Finally`关键字，它都执行关联的代码块而不考虑是否会引发异常。  
  
## <a name="synchronization-events-and-wait-handles"></a>同步事件和等待句柄  
 使用锁或监视器可用于预防同时执行的线程敏感代码块，但这些构造不允许一个线程通信到另一个事件。 这要求*同步事件*，哪些是具有两种状态之一的对象终止和非终止，可用来激活和挂起的线程。 线程可以通过所进行的同步事件为非终止状态，等待挂起，并且可以通过将事件状态为终止状态更改激活。 如果线程尝试等待已终止的事件，该线程将继续执行而不会延迟。  
  
 有两种类型的同步事件︰ <xref:System.Threading.AutoResetEvent>，和<xref:System.Threading.ManualResetEvent>。</xref:System.Threading.ManualResetEvent> </xref:System.Threading.AutoResetEvent> 它们的差异仅在于<xref:System.Threading.AutoResetEvent>从终止变为非终止自动无论何时激活线程。</xref:System.Threading.AutoResetEvent> 相反，<xref:System.Threading.ManualResetEvent>允许任意数量的线程将激活其终止状态的并且将仅恢复到非终止时，状态其<xref:System.Threading.EventWaitHandle.Reset%2A>调用方法。</xref:System.Threading.EventWaitHandle.Reset%2A> </xref:System.Threading.ManualResetEvent>  
  
 线程会等待事件通过调用等待方法之一来如<xref:System.Threading.WaitHandle.WaitOne%2A>， <xref:System.Threading.WaitHandle.WaitAny%2A>，或<xref:System.Threading.WaitHandle.WaitAll%2A>.</xref:System.Threading.WaitHandle.WaitAll%2A> </xref:System.Threading.WaitHandle.WaitAny%2A> </xref:System.Threading.WaitHandle.WaitOne%2A> <xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=fullName>导致线程等待，直到一个事件将被发送信号，<xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName>阻止线程，直到一个或多个指示的事件发送信号，和<xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName>阻止线程，直到所有指示的事件发送信号。</xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName> </xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName></xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=fullName> 事件将被发送信号时其<xref:System.Threading.EventWaitHandle.Set%2A>调用方法。</xref:System.Threading.EventWaitHandle.Set%2A>  
  
 在下面的示例中，创建和启动线程`Main`函数。 新线程等待事件使用<xref:System.Threading.WaitHandle.WaitOne%2A>方法。</xref:System.Threading.WaitHandle.WaitOne%2A> 挂起线程，直到该事件终止正在执行的主线程`Main`函数。 一旦该事件将被发送信号，辅助线程将返回。 在这种情况下，因为该事件仅用于实现一个线程的激活，或者<xref:System.Threading.AutoResetEvent>或<xref:System.Threading.ManualResetEvent>无法使用类。</xref:System.Threading.ManualResetEvent> </xref:System.Threading.AutoResetEvent>  
  
```vb  
Imports System.Threading  
  
Module Module1  
    Dim autoEvent As AutoResetEvent  
  
    Sub DoWork()  
        Console.WriteLine("   worker thread started, now waiting on event...")  
        autoEvent.WaitOne()  
        Console.WriteLine("   worker thread reactivated, now exiting...")  
    End Sub  
  
    Sub Main()  
        autoEvent = New AutoResetEvent(False)  
  
        Console.WriteLine("main thread starting worker thread...")  
        Dim t As New Thread(AddressOf DoWork)  
        t.Start()  
  
        Console.WriteLine("main thread sleeping for 1 second...")  
        Thread.Sleep(1000)  
  
        Console.WriteLine("main thread signaling worker thread...")  
        autoEvent.Set()  
    End Sub  
End Module  
```  
  
## <a name="mutex-object"></a>Mutex 对象  
 一个*互斥体*类似于监视器; 它会阻止的代码块的同时执行多个线程一次。 事实上，名称"互斥体"是"互相排斥。"一词的缩写形式 与不同的监视器，但是，互斥锁可在进程间同步线程。 由<xref:System.Threading.Mutex>类</xref:System.Threading.Mutex>表示一个 mutex  
  
 当用于进程间同步，mutex 称为*已命名互斥体*因为它是在另一个应用程序中使用，因此它不能通过全局或静态变量共享。 必须为其提供一个名称，以便两个应用程序能够访问同一个 mutex 对象。  
  
 虽然互斥体可用于进程内的线程同步，但是使用<xref:System.Threading.Monitor>是通常首选，因为监视器专门为.NET Framework 设计，因此作出更好地利用资源。</xref:System.Threading.Monitor> 与此相反，<xref:System.Threading.Mutex>类是 Win32 构造的包装。</xref:System.Threading.Mutex> 尽管它是一个监视器，它比功能更强大，互斥体，就需要更占用计算资源比所需的<xref:System.Threading.Monitor>类</xref:System.Threading.Monitor>的互操作转换 有关使用互斥体的示例，请参阅[互斥锁](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2)。  
  
## <a name="interlocked-class"></a>Interlocked 的类  
 您可以使用的方法<xref:System.Threading.Interlocked>类来避免在多个线程尝试同时更新或相同的值进行比较时可能发生的问题。</xref:System.Threading.Interlocked> 此类方法可以安全地递增、 递减、 交换，并比较值从任意线程。  
  
## <a name="readerwriter-locks"></a>ReaderWriter 锁  
 在某些情况下，您可能希望仅在写入数据时锁定资源，并允许多个客户端同时读取数据时不更新数据。 <xref:System.Threading.ReaderWriterLock>类强制执行对资源的独占访问，而在线程修改该资源，但在读取资源时，它允许非独占访问。</xref:System.Threading.ReaderWriterLock> ReaderWriter 锁是排他锁，这会使其他线程等待，即使当这些线程不需要更新数据的有用替代方法。  
  
## <a name="deadlocks"></a>死锁  
 线程同步是在多线程应用程序中非常有用，但始终是创建的危险`deadlock`，其中多个线程正在等待对方，而该应用程序就会停顿。 死锁的情况，汽车停止在四路停止，而每个用户正在等待另一个以转到相当。 避免死锁很重要;关键是仔细规划。 图表多线程应用程序，在开始编码之前，通常可以预测死锁情况。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Thread></xref:System.Threading.Thread>   
 <xref:System.Threading.WaitHandle.WaitOne%2A></xref:System.Threading.WaitHandle.WaitOne%2A>   
 <xref:System.Threading.WaitHandle.WaitAny%2A></xref:System.Threading.WaitHandle.WaitAny%2A>   
 <xref:System.Threading.WaitHandle.WaitAll%2A></xref:System.Threading.WaitHandle.WaitAll%2A>   
 <xref:System.Threading.Thread.Join%2A></xref:System.Threading.Thread.Join%2A>   
 <xref:System.Threading.Thread.Start%2A></xref:System.Threading.Thread.Start%2A>   
 <xref:System.Threading.Thread.Sleep%2A></xref:System.Threading.Thread.Sleep%2A>   
 <xref:System.Threading.Monitor></xref:System.Threading.Monitor>   
 <xref:System.Threading.Mutex></xref:System.Threading.Mutex>   
 <xref:System.Threading.AutoResetEvent></xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent></xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.Interlocked></xref:System.Threading.Interlocked>   
 <xref:System.Threading.WaitHandle></xref:System.Threading.WaitHandle>   
 <xref:System.Threading.EventWaitHandle></xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading></xref:System.Threading>   
 <xref:System.Threading.EventWaitHandle.Set%2A></xref:System.Threading.EventWaitHandle.Set%2A>   
 [多线程应用程序 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [SyncLock 语句](../../../../visual-basic/language-reference/statements/synclock-statement.md)   
 [互斥锁](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2)   
 @System.Threading.Monitor   
 [互锁的操作](http://msdn.microsoft.com/library/cbda7114-c752-4f3e-ada1-b1e8dd262f2b)   
 [AutoResetEvent](http://msdn.microsoft.com/library/6d39c48d-6b37-4a9b-8631-f2924cfd9c18)   
 [同步数据的多线程处理](http://msdn.microsoft.com/library/b980eb4c-71d5-4860-864a-6dfe3692430a)
