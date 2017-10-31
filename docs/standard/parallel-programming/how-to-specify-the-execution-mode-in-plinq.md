---
title: "How to: Specify the Execution Mode in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, how to use execution mode"
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Specify the Execution Mode in PLINQ
本示例演示如何强制 PLINQ 绕过其默认试探法并在不考虑查询形状的情况下并行化查询。  
  
> [!WARNING]
>  本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。  有关加速的更多信息，请参见[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 示例  
 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 PLINQ 旨在利用并行化的机会。  但是，并非所有查询都受益于并行执行。  例如，如果查询包含很少执行工作的单个用户委托，查询通常将以更快的速度按顺序运行。  这是因为在启用并行化执行中，所涉及的开销比速度提高所涉及的开销大。  因此，PLINQ 不会自动并行化每个查询。  它首先检查查询的形状和构成它的各种运算符。  基于此分析，默认执行模式下的 PLINQ 可能决定按顺序执行部分或全部查询。  然而，在某些情况下，您对查询的了解可能比 PLINQ 能够从其分析中确定的多。  例如，您可能知道委托非常昂贵，查询将一定受益于并行化。  在这样的情况下，可使用 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> 方法，并指定 <xref:System.Linq.ParallelExecutionMode> 值，以指示 PLINQ 始终以并行方式运行查询。  
  
## 编译代码  
 将此代码剪切并粘贴到 [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md) 中，并从 `Main` 调用该方法。  
  
## 请参阅  
 <xref:System.Linq.ParallelEnumerable.AsSequential%2A>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)