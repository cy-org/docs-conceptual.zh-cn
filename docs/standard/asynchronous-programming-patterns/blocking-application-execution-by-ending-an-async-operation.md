---
title: "Blocking Application Execution by Ending an Async Operation | Microsoft Docs"
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
  - "blocks, asynchronous operations"
  - "AsyncWaitHandle property"
  - "asynchronous programming, blocking applications"
  - "blocking application execution"
ms.assetid: cc5e2834-a65b-4df8-b750-7bdb79997fee
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Blocking Application Execution by Ending an Async Operation
如果应用程序在等待异步操作结果时不能继续执行其他工作，则在操作完成之前，必须阻止执行其他工作。  可以使用下列方法之一来在等待异步操作完成时阻止应用程序的主线程。  
  
-   调用异步操作的 "End"*操作名称OperationName* 方法。  本主题中演示了此方法。  
  
-   使用异步操作的 "Begin"*操作名称OperationName* 方法返回的 <xref:System.IAsyncResult> 的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 属性。  有关演示此方法的示例，请参见 [Blocking Application Execution Using an AsyncWaitHandle](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md)。  
  
 在异步操作完成之前使用 "End" *操作名称OperationName* 方法进行阻止的应用程序通常会调用 "Begin"*操作名称OperationName* 方法，执行任何不需要等待操作结果也可以执行的工作，然后调用 "End"*OperationName*。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Net.Dns> 类中的异步方法来检索用户指定的计算机的域名系统信息。  请注意，示例中为 <xref:System.Net.Dns.BeginGetHostByName%2A> `requestCallback` 和 `stateObject` 参数传递了 `null`（在 Visual Basic 中为 `Nothing`），因为在使用此方法时不需要这两个参数。  
  
 [!code-csharp[AsyncDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlock.cs#1)]
 [!code-vb[AsyncDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlock.vb#1)]  
  
## 请参阅  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)