---
title: "Using an AsyncCallback Delegate to End an Asynchronous Operation | Microsoft Docs"
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
  - "asynchronous programming, ending operations"
  - "AsyncCallback delegate"
  - "stopping asynchronous operations"
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Using an AsyncCallback Delegate to End an Asynchronous Operation
在等待异步操作结果的同时可以进行其他工作的应用程序不应在操作完成之前阻止等待。  可以使用下列方法之一来在等待异步操作完成的同时继续执行指令。  
  
-   可使用 <xref:System.AsyncCallback> 委托来处理另一个线程中的异步操作的结果。  本主题中演示了此方法。  
  
-   可使用异步操作的 "Begin" *操作名称OperationName 方法返回的*<xref:System.IAsyncResult> 的 <xref:System.IAsyncResult.IsCompleted%2A> 属性来确定该操作是否已完成。  有关演示此方法的示例，请参见 [Polling for the Status of an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md)。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Net.Dns> 类中的异步方法来检索用户指定的计算机的域名系统 \(DNS\) 信息。  此示例创建一个引用 `ProcessDnsInformation` 方法的 <xref:System.AsyncCallback> 委托。  对各个针对 DNS 信息发出的异步请求，将分别调用一次此方法。  
  
 请注意，用户指定的主机被传递给了 <xref:System.Net.Dns.BeginGetHostByName%2A> <xref:System.Object> 参数。  有关演示如何定义和使用更复杂的状态对象的示例，请参见 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)。  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## 请参阅  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [Calling Asynchronous Methods Using IAsyncResult](../../../docs/standard/asynchronous-programming-patterns/calling-asynchronous-methods-using-iasyncresult.md)   
 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)