---
title: "How to: Listen for Cancellation Requests by Polling | Microsoft Docs"
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
  - "cancellation, how to poll for requests"
ms.assetid: c7f2f022-d08e-4e00-b4eb-ae84844cb1bc
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Listen for Cancellation Requests by Polling
下面的示例演示一种方法，通过该方法用户代码可以定期轮询取消标记以查看是否已从调用线程请求取消。  此示例使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 类型，但是相同的模式适用于由 <xref:System.Threading.ThreadPool?displayProperty=fullName> 类型或 <xref:System.Threading.Thread?displayProperty=fullName> 类型直接创建的异步操作。  
  
## 示例  
 轮询需要某种循环或递归代码，该代码可以定期读取布尔 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 属性的值。  如果您使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 类型且等待任务在调用线程中完成，则可以使用 <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> 方法检查属性和引发异常。  通过使用此方法，可以确保为响应请求而引发相应的异常。  如果使用 <xref:System.Threading.Tasks.Task>，则调用此方法优于手动引发 <xref:System.OperationCanceledException>。  如果您不必引发异常，则只需检查属性并从方法返回（如果属性为 `true`）。  
  
 [!code-csharp[Cancellation#11](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex11.cs#11)]
 [!code-vb[Cancellation#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex11.vb#11)]  
  
 调用 <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> 非常快，不会在循环中显著增加系统开销。  
  
 如果调用 <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A>，且除了引发异常之外还要执行其他操作来响应取消，则只需显式检查 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 属性即可。  在此示例中，可以发现代码实际上访问该属性两次：一次是在显式访问中，另一次是在 <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> 方法中。  但是，由于读取 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 属性的操作针对每次访问只包含一条可变读取指令，两次访问不会对性能有太大影响。  调用该方法仍优于手动引发 <xref:System.OperationCanceledException>。  
  
## 请参阅  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)