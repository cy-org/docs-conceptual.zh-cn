---
title: "How to: Implement a Producer-Consumer Dataflow Pattern | Microsoft Docs"
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
  - "TPL dataflow library, implementing producer-consumer pattern"
  - "Task Parallel Library, dataflows"
  - "producer-consumer patterns, implementing [TPL]"
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Implement a Producer-Consumer Dataflow Pattern
本文档描述如何使用TPL 数据流库实现生产者\-消费者模式。  在此模式中，制造者向消息块发送消息，使用者从该块中读取消息。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 示例  
 下面的示例演示使用数据流的基本生产者 \- 消费者模式。  `Produce` 方法编写包含随机的字节数据到 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=fullName> 对象，`Consume` 同时方法从 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=fullName> 对象中读取的字节数据。  通过对 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 和 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 接口的操作，而不是它们的派生类型，可以编写各种流数据块类型可以操作的可重用的代码。  此示例使用了 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 类。  由于 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 类既充当源块又充当目标块、制造者和使用者可以使用共享对象对数据进行传输。  
  
 在一次轮询中，`Produce` 方法调<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法向目标块同步读写数据 。  在 `Produce` 方法编写所有数据到目标块之后，它会调用 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> 方法以表明块将不会有可用的附加数据。  `Consume` 方法使用 [async](../Topic/async%20\(C%23%20Reference\).md)和 [await](../Topic/await%20\(C%23%20Reference\).md) 操作\( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中为 [Async](../Topic/Async%20\(Visual%20Basic\).md) 和[Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md)） 异步计算从 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 对象接收的总字节数。  异步操作， 当源块有可用的数据，或当源块将不再有可用的附加数据时`Consume` 方法调用<xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> 方法接收通知，。  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DataflowProducerConsumer.cs` \(`DataflowProducerConsumer.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.vb**  
  
## 可靠编程  
 此示例使用一消费者者处理源数据。  如果应用程序中有多个消费者，如下面的示例所示，使用 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法读取源块的数据。  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]  
  
 当没有数据可用时<xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法返回`False` 。  当多个消费者必须同时访问源块时，此机制保证数据在调用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A>调用后仍有效。  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)