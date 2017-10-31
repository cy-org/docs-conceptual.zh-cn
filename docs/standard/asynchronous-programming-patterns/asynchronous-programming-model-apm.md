---
title: "Asynchronous Programming Model (APM) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ending asynchronous operations"
  - "starting asynchronous operations"
  - "beginning asynchronous operations"
  - "asynchronous programming, ending operations"
  - "asynchronous programming"
  - "stopping asynchronous operations"
  - "asynchronous programming, beginning operations"
ms.assetid: c9b3501e-6bc6-40f9-8efd-4b6d9e39ccf0
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Asynchronous Programming Model (APM)
使用 <xref:System.IAsyncResult> 设计模式的异步操作是通过名为 **Begin** *OperationName* 和 **End** *OperationName* 的两个方法来实现的，这两个方法分别开始和结束异步操作 *OperationName*。 例如，<xref:System.IO.FileStream> 类提供 <xref:System.IO.FileStream.BeginRead%2A> 和 <xref:System.IO.FileStream.EndRead%2A> 方法来从文件异步读取字节。 这两个方法实现了 <xref:System.IO.FileStream.Read%2A> 方法的异步版本。  
  
> [!NOTE]
>  从 .NET Framework 4 开始，任务并行库为异步和并行编程提供了一种新模型。 有关详细信息，请参阅[Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)和[Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)。  
  
 在调用 **Begin** *OperationName* 后，应用程序可以继续在调用线程上执行指令，同时异步操作在另一个线程上执行。 每次调用 **Begin** *OperationName* 时，应用程序还应调用 **End** *OperationName* 来获取操作的结果。  
  
## 开始异步操作  
 **Begin** *OperationName* 方法开始异步操作 *OperationName*，并返回实现 <xref:System.IAsyncResult> 接口的对象。<xref:System.IAsyncResult> 对象存储有关异步操作的信息。 下表显示有关异步操作的信息。  
  
|成员|描述|  
|--------|--------|  
|<xref:System.IAsyncResult.AsyncState%2A>|一个特定于应用程序的可选对象，其中包含有关异步操作的信息。|  
|<xref:System.IAsyncResult.AsyncWaitHandle%2A>|一个 <xref:System.Threading.WaitHandle>，可用来在异步操作完成之前阻止应用程序执行。|  
|<xref:System.IAsyncResult.CompletedSynchronously%2A>|一个值，指示异步操作是否是在用于调用 **Begin** *OperationName* 的线程上完成，而不是在单独的 <xref:System.Threading.ThreadPool> 线程上完成。|  
|<xref:System.IAsyncResult.IsCompleted%2A>|一个值，指示异步操作是否已完成。|  
  
 **Begin** *OperationName* 方法采用该方法的同步版本的签名中声明的任何参数（由值传递或由引用传递）。**Begin** *OperationName* 方法签名中不包含任何输出参数。**Begin** *OperationName* 方法签名另外还包括两个其他参数。 第一个参数定义一个 <xref:System.AsyncCallback> 委托，此委托引用在异步操作完成时调用的方法。 如果调用方不希望在操作完成后调用方法，它可以指定 `null`（在 Visual Basic 中为 `Nothing`）。 第二个参数是一个用户定义的对象。 此对象可用来向异步操作完成时调用的方法传递应用程序特定的状态信息。 如果 **Begin** *OperationName* 方法还采用其他一些操作特定的参数（例如，一个用于存储从文件读取的字节的字节数组），则 <xref:System.AsyncCallback> 和应用程序状态对象将是 **Begin** *OperationName* 方法签名中的最后两个参数。  
  
 **Begin** *OperationName* 立即返回对调用线程的控制。 如果 **Begin** *OperationName* 方法引发异常，则会在开始异步操作之前引发异常。 如果 **Begin** *OperationName* 方法引发异常，则意味着没有调用回调方法。  
  
## 结束异步操作  
 **End** *OperationName* 方法可结束异步操作 *OperationName*。**End** *OperationName* 方法的返回值与其同步对应方法的返回值类型相同，并且是特定于异步操作的。 例如，<xref:System.IO.FileStream.EndRead%2A> 方法返回从 <xref:System.IO.FileStream> 读取的字节数，<xref:System.Net.Dns.EndGetHostByName%2A> 方法返回包含有关主机的信息的 <xref:System.Net.IPHostEntry> 对象。**End** *OperationName* 方法采用该方法同步版本的签名中声明的所有输出参数或引用参数。 除了来自同步方法的参数外，**End** *OperationName* 方法还包括 <xref:System.IAsyncResult> 参数。 调用方必须将对应调用返回的实例传递给 **Begin** *OperationName*。  
  
 如果调用 **End** *OperationName* 时 <xref:System.IAsyncResult> 对象表示的异步操作尚未完成，则 **End** *OperationName* 将在异步操作完成之前阻止调用线程。 异步操作引发的异常是从 **End** *OperationName* 方法引发的。 未定义多次使用同一 <xref:System.IAsyncResult> 调用 **End** *OperationName* 方法的效果。 同样，也未定义使用不是相关 Begin 方法返回的 <xref:System.IAsyncResult> 调用 **End** *OperationName* 方法的效果。  
  
> [!NOTE]
>  对于这两种未定义的情况，实施者应考虑引发 <xref:System.InvalidOperationException>。  
  
> [!NOTE]
>  此设计模式的实施者应通知调用方异步操作已通过以下步骤完成：将 <xref:System.IAsyncResult.IsCompleted%2A> 设置为 true，调用异步回调方法（如果已指定一个回调方法），然后发送 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 信号。  
  
 对于访问异步操作的结果，应用程序开发人员有若干种设计选择。 正确的选择取决于应用程序是否有可以在操作完成时执行的指令。 如果应用程序在接收到异步操作结果之前不能进行任何其他工作，则必须在获得这些结果之前先阻止该应用程序进行其他工作。 若要在异步操作完成之前阻止应用程序，可以使用下列方法之一：  
  
-   从应用程序的主线程调用 **End** *OperationName*，阻止应用程序执行，直到操作完成。 有关演示此方法的示例，请参阅[Blocking Application Execution by Ending an Async Operation](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-by-ending-an-async-operation.md)。  
  
-   使用 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 来阻止应用程序执行，直到一个或多个操作完成。 有关演示此方法的示例，请参阅[Blocking Application Execution Using an AsyncWaitHandle](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md)。  
  
 在异步操作完成时不需要阻止的应用程序可使用下列方法之一：  
  
-   按以下方式轮询操作完成状态：定期检查 <xref:System.IAsyncResult.IsCompleted%2A> 属性，并在操作完成后调用 **End** *OperationName*。 有关演示此方法的示例，请参阅[Polling for the Status of an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md)。  
  
-   使用 <xref:System.AsyncCallback> 委托来指定要在操作完成时调用的方法。 有关演示此方法的示例，请参阅[Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。  
  
## 请参阅  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)   
 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)