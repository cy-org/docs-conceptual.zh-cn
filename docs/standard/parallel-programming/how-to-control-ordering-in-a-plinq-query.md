---
title: "How to: Control Ordering in a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to control ordering"
ms.assetid: c67eccc7-004d-4b2f-987e-919cbbd62ef7
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Control Ordering in a PLINQ Query
这些示例演示如何使用 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 扩展方法在 PLINQ 查询中控制排序。  
  
> [!WARNING]
>  这些示例主要旨在演示用法，运行速度可能比也可能不如等效的顺序 LINQ to Objects 查询快。  
  
## 示例  
 下面的示例保留源序列的排序。  有时这是必要的；例如，某些查询运算符需要经过排序的源序列才能生成正确的结果。  
  
 [!code-csharp[PLINQ#12](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#12)]
 [!code-vb[PLINQ#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#12)]  
  
## 示例  
 下面的示例演示一些可能需要对其源序列进行排序的查询运算符。  这些运算符将适用于未排序的序列，但可能会产生意外的结果。  
  
 [!code-csharp[PLINQ#14](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#14)]
 [!code-vb[PLINQ#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#14)]  
  
 若要运行此方法，请将其粘贴到 [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md)项目的 PLINQDataSample 类中，然后按 F5。  
  
## 示例  
 下面的示例演示如何保留查询第一部分的排序，然后移除排序以提高 join 子句的性能，接着将排序重新应用于最终结果序列。  
  
 [!code-csharp[PLINQ#15](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#15)]
 [!code-vb[PLINQ#15](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#15)]  
  
 若要运行此方法，请将其粘贴到 [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md)项目的 PLINQDataSample 类中，然后按 F5。  
  
## 请参阅  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)