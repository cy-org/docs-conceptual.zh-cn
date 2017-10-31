---
title: "How to: Measure PLINQ Query Performance | Microsoft Docs"
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
  - "PLINQ queries, how to measure performance"
ms.assetid: 491ba43b-2c10-473d-9aab-e2cb96446711
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Measure PLINQ Query Performance
此示例演示如何使用 <xref:System.Diagnostics.Stopwatch> 类来衡量 PLINQ 查询执行所花费的时间。  
  
## 示例  
 此示例使用空的 `foreach` 循环（Visual Basic 中为 `For Each`）来衡量查询执行所花费的时间。  在实际代码中，该循环通常包含额外的处理步骤，这些步骤会增加查询总执行时间。  请注意，秒表会恰好在循环开始之前启动，因为此时查询开始执行。  如果需要更精细的度量，您可以使用 `ElapsedTicks` 属性，而不是 `ElapsedMilliseconds`。  
  
 [!code-csharp[PLINQ#19](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/measure2.cs#19)]
 [!code-vb[PLINQ#19](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/measure2.vb#19)]  
  
 当您在体验查询实现时，总执行时间是一项非常有用的指标，但它并不总是能说明一切。  为了更深入细致地了解查询线程相互之间的交互以及与其他正在运行的进程的交互，请使用并发可视化工具。  有关更多信息，请参见[并发可视化工具](../Topic/Concurrency%20Visualizer.md)。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)