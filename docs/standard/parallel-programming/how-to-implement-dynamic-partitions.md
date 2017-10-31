---
title: "How to: Implement Dynamic Partitions | Microsoft Docs"
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
  - "tasks, how to create a dynamic partitioner"
ms.assetid: c875ad12-a161-43e6-ad1c-3d6927c536a7
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# How to: Implement Dynamic Partitions
下面的示例演示如何实现一个实现动态分区并可从某些重载 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 和 PLINQ 中使用的 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName>。  
  
## 示例  
 每次分区对枚举器调用 <xref:System.Collections.IEnumerator.MoveNext%2A> 时，枚举器都会提供包含一个列表元素的分区。  对于 PLINQ 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A>，分区是一个 <xref:System.Threading.Tasks.Task> 实例。  由于请求同时在多个线程上发生，因此对当前索引的访问是同步的。  
  
 [!code-csharp[TPL_Partitioners#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#04)]
 [!code-vb[TPL_Partitioners#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/dynamicpartitioner.vb#04)]  
  
 这是按区块分区的示例，其中每个区块都由一个元素组成。  通过一次提供多个元素，您可以减少锁争用，并在理论上实现更快的性能。  但是，有时较大的区块可能需要额外的负载平衡逻辑才能使所有线程在工作完成之前保持忙碌。  
  
## 请参阅  
 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)   
 [How to: Implement a Partitioner for Static Partitioning](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)