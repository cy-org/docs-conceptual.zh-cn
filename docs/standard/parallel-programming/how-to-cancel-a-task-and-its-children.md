---
title: "How to: Cancel a Task and Its Children | Microsoft Docs"
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
  - "tasks, how to cancel"
ms.assetid: 08574301-8331-4719-ad50-9cf7f6ff3048
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Cancel a Task and Its Children
这些示例演示如何执行以下任务：  
  
1.  创建和启动可取消的任务。  
  
2.  将取消标记传递到您的用户委托，并可选择传递到任务实例。  
  
3.  在用户委托中发出取消请求通知并对这些请求做出响应。  
  
4.  （可选）在调用线程上发出有关任务已取消的通知。  
  
 调用线程不会强制结束任务；它只会发出有关已请求取消的通知。  如果任务已经在运行，则由用户委托负责通知请求并相应做出响应。  如果在任务运行之前请求了取消，则用户委托从不会运行，并且任务对象将转换为 Canceled 状态。  
  
## 示例  
 此示例演示如何终止 <xref:System.Threading.Tasks.Task> 及其子级以响应取消请求。  它还演示，当用户通过引发 <xref:System.Threading.Tasks.TaskCanceledException>委托终止时，调用线程可以选择使用 <xref:System.Threading.Tasks.Task.Wait%2A> 方法或 <xref:System.Threading.Tasks.Task.WaitAll%2A> 方法来等待任务完成。  在这种情况下，你必须使用`try/catch`块来处理调用线程上的异常。  
  
 [!code-csharp[TPL_Cancellation#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/cancel1.cs#04)]
 [!code-vb[TPL_Cancellation#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/cancel1.vb#04)]  
  
 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 类与基于 <xref:System.Threading.CancellationTokenSource?displayProperty=fullName> 和 <xref:System.Threading.CancellationToken?displayProperty=fullName> 类型的取消模型完全集成。  有关更多信息，请参见[Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)和[Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md)。  
  
## 请参阅  
 <xref:System.Threading.CancellationTokenSource?displayProperty=fullName>   
 <xref:System.Threading.CancellationToken?displayProperty=fullName>   
 <xref:System.Threading.Tasks.Task?displayProperty=fullName>   
 <xref:System.Threading.Tasks.Task%601?displayProperty=fullName>   
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)   
 [Attached and Detached Child Tasks](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)