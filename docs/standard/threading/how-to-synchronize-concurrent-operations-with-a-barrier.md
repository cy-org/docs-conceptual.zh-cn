---
title: "How to: Synchronize Concurrent Operations with a Barrier | Microsoft Docs"
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
  - "Barrier, how to use"
ms.assetid: e1a253ff-e0fb-4df8-95ff-d01a90d4cb19
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Synchronize Concurrent Operations with a Barrier
下面的示例演示如何使用 <xref:System.Threading.Barrier> 同步并发任务。  
  
## 示例  
 以下程序旨在通过使用一种随机化算法将一个短语的单词打乱排列，从而计算两个线程需要多少迭代（或阶段）才能各自找出自己的解答。  在每个线程排列好单词之后，关卡后期阶段操作将比较两个结果，查看完整句子是否以正确的单词顺序呈现。  
  
 [!code-csharp[CDS_Barrier#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#01)]
 [!code-vb[CDS_Barrier#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#01)]  
  
 <xref:System.Threading.Barrier> 是一个对象，它可以在并行操作中的所有任务都达到相应的关卡之前，阻止各个任务继续执行。  如果并行操作是分阶段执行的，并且每一阶段要求各任务之间进行同步，则可以使用该对象。  在本示例中，操作共分为两个阶段。  在第一阶段，每一项任务将使用数据填充其缓冲区部分。  每项任务在填写完各自的部分之后，均会向关卡发出自己已准备好继续的信号，然后进行等待。  在所有任务都已向关卡发出信号之后，将取消阻塞这些任务，并开始第二阶段。  由于第二阶段要求每项任务都必须具有对此时已生成的所有数据的访问权，因此关卡是必需的。  如果没有关卡，那么，先期完成的任务可能会尝试从尚未由其他任务填充的缓冲区中进行读取。  通过这种方式，可以对任意数量的阶段进行同步。  
  
## 请参阅  
 [Data Structures for Parallel Programming](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)