---
title: "How to: Implement a Partitioner for Static Partitioning | Microsoft Docs"
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
  - "tasks, how to create a static partitioner"
ms.assetid: f4410508-cac6-4ba7-bef1-c5e68b2794f3
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Implement a Partitioner for Static Partitioning
下面的示例演示了一种为执行静态分区的 PLINQ 实现简单的自定义分区程序的方式。  由于分区程序不支持动态分区，因此无法从 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 中使用该分区程序。  对于每个元素都需要增加处理时间的数据源而言，此特定分区程序的速度可能比默认按范围分区程序快。  
  
## 示例  
 [!code-csharp[TPL_Partitioners#05](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#05)]  
  
 此示例中的分区假定每个元素的处理时间线程递增。  在实际情况中，可能很难采用这种方式预测处理时间。  如果要将静态分区程序用于特定数据源，您可以针对该数据源优化分区规则、添加负载平衡逻辑，或使用[How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)中演示的按区块分区方法。  
  
## 请参阅  
 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)