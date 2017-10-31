---
title: "Polling for the Status of an Asynchronous Operation | Microsoft Docs"
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
  - "asynchronous programming, status polling"
  - "polling asynchronous operation status"
  - "status information [.NET Framework], asynchronous operations"
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Polling for the Status of an Asynchronous Operation
在等待异步操作结果的同时可以进行其他工作的应用程序不应在操作完成之前阻止等待。  可以使用下列方法之一来在等待异步操作完成的同时继续执行指令。  
  
-   可使用异步操作的 "Begin" *操作名称OperationName 方法返回的*<xref:System.IAsyncResult> 的 <xref:System.IAsyncResult.IsCompleted%2A> 属性来确定该操作是否已完成。  此方法叫做轮询；本主题中将演示轮询。  
  
-   可使用 <xref:System.AsyncCallback> 委托来处理另一个线程中的异步操作的结果。  有关演示此方法的示例，请参见 [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Net.Dns> 类中的异步方法来检索用户指定的计算机的域名系统信息。  此示例开始异步操作，然后在控制台输出句点（“.”），直到操作完成。  请注意，示例中为 <xref:System.Net.Dns.BeginGetHostByName%2A> <xref:System.AsyncCallback> 和 <xref:System.Object> 参数传递了 **null**（在 Visual Basic 中为 **Nothing**），因为在使用此方法时不需要这两个参数。  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## 请参阅  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)