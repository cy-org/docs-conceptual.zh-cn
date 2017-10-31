---
title: "How to: Write a Custom PLINQ Aggregate Function | Microsoft Docs"
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
  - "PLINQ queries, how to create aggregate function"
ms.assetid: 5a70dd49-ab2a-4798-b551-196ee7042b1a
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Write a Custom PLINQ Aggregate Function
此示例演示如何使用 <xref:System.Linq.ParallelEnumerable.Aggregate%2A> 方法将自定义聚合函数应用于源序列。  
  
> [!WARNING]
>  本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。  有关加速的更多信息，请参见[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 示例  
 下面的示例计算一个整数序列的标准偏差。  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 此示例使用 Aggregate 标准查询运算符的重载，该运算符是 PLINQ 所独有的。  此重载采用额外的 <xref:System.Func%603?displayProperty=fullName> 作为第三个输入参数。  此委托在其对聚合的结果执行最终计算之前合并来自所有线程的结果。  在此示例中，我们将所有线程的和加总。  
  
 请注意，当 lambda 表达式体中只有一个表达式时，<xref:System.Func%602?displayProperty=fullName> 委托的返回值为该表达式的值。  
  
## 请参阅  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)