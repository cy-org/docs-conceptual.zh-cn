---
title: "Canceling Threads Cooperatively | Microsoft Docs"
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
  - "threads, cancellation"
ms.assetid: d2d6d5fd-e263-4fa0-847b-2fc3e0d82337
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Canceling Threads Cooperatively
在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 之前，.NET Framework 不提供内置方法在线程启动以后以协作方式取消线程。 但是，在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，可以使用取消标记来取消线程，就像使用它们来取消 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象或 PLINQ 查询一样。 虽然 <xref:System.Threading.Thread?displayProperty=fullName> 类不提供对取消标记的内置支持，但可以使用采用 <xref:System.Threading.ParameterizedThreadStart> 委托的 <xref:System.Threading.Thread> 构造函数将一个标记传递给一个线程过程。 下面的示例演示如何执行此操作。  
  
 [!code-csharp[Cancellation#14](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/CooperativeThreads.cs#14)]
 [!code-vb[Cancellation#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/CooperativeThreads.vb#14)]  
  
## 请参阅  
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)