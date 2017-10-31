---
title: "How to: Listen for Multiple Cancellation Requests | Microsoft Docs"
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
  - "cancellation tokens, joining"
  - "LinkedTokenSource, how to"
ms.assetid: 6f4f3804-2ed7-41b4-a97a-6e32b93f6e05
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Listen for Multiple Cancellation Requests
此示例演示如何同时侦听两个取消标记，以便您可以取消操作（如果任一标记请求取消）。  
  
> [!NOTE]
>  当启用“仅我的代码”时，在某些情况下，Visual Studio 将在引发异常的行上中断运行，并显示错误消息“异常未由用户代码处理”。此错误是良性的。  可以按 F5 从中断处继续运行，并查看在以下示例中演示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在**“工具”\-\>“选项”\-\>“调试”\-\>“常规”**下取消选中“仅我的代码”复选框即可。  
  
## 示例  
 在下面的示例中，使用 <xref:System.Threading.CancellationTokenSource.CreateLinkedTokenSource%2A> 方法将两个标记连接成一个标记。  这使得可以将标记传递给只采用一个取消标记作为参数的方法。  此示例演示一种常见情形，即方法必须检查从类外传入的标记和在类中生成的标记。  
  
 [!code-csharp[Cancellation#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex13.cs#13)]
 [!code-vb[Cancellation#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex13.vb#13)]  
  
 当链接的标记引发 <xref:System.OperationCanceledException> 时，传递给此异常的标记为该链接的标记，而不是任何一个前置标记。  若要确定取消哪些标记，请直接检查前置标记的状态。  
  
 在此示例中，应从不引发 <xref:System.AggregateException>，但在此处捕获它是因为在现实情况中，从任务委托引发的除 <xref:System.OperationCanceledException> 外的任何其他异常均包装在 <xref:System.OperationCanceledException> 中。  
  
## 请参阅  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)