---
title: "How to: Listen for Cancellation Requests That Have Wait Handles | Microsoft Docs"
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
  - "cancellation, waiting with wait handles"
ms.assetid: 6e2aa49b-fc84-4bcf-962b-17db98b7edcb
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Listen for Cancellation Requests That Have Wait Handles
如果方法在等待事件接收信号时被阻塞，它将无法检查取消标记的值，也无法及时响应。  第一个示例演示如何在您处理本质上不支持统一取消框架的事件（如 <xref:System.Threading.ManualResetEvent?displayProperty=fullName>）时解决此问题。  第二个示例演示一个更简单的方法，即使用支持统一取消的 <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>。  
  
> [!NOTE]
>  当启用“仅我的代码”时，在某些情况下，Visual Studio 将在引发异常的行上中断运行，并显示错误消息“异常未由用户代码处理”。此错误是良性的。  可以按 F5 从中断处继续运行，并查看在以下示例中演示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在**“工具”\-\>“选项”\-\>“调试”\-\>“常规”**下取消选中“仅我的代码”复选框即可。  
  
## 示例  
 下面的示例使用 <xref:System.Threading.ManualResetEvent> 来演示如何取消阻塞不支持统一取消的等待句柄。  
  
 [!code-csharp[Cancellation#9](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex9.cs#9)]
 [!code-vb[Cancellation#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex9.vb#9)]  
  
## 示例  
 下面的示例使用 <xref:System.Threading.ManualResetEventSlim> 来演示如何取消阻塞不支持统一取消的坐标基元。  可以对其他轻型坐标基元（例如 <xref:System.Threading.Semaphore>`Slim` 和 <xref:System.Threading.CountdownEvent>）使用相同的方法。  
  
 [!code-csharp[Cancellation#10](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex10.cs#10)]
 [!code-vb[Cancellation#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex10.vb#10)]  
  
## 请参阅  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)