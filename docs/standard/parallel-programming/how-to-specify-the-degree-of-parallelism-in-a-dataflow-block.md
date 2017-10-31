---
title: "How to: Specify the Degree of Parallelism in a Dataflow Block | Microsoft Docs"
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
  - "dataflow block, specifying parallelism in TPL"
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, specifying parallelism"
ms.assetid: e4088541-ee05-40db-95f5-147cfe62fde7
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Specify the Degree of Parallelism in a Dataflow Block
本文档介绍如何设置 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A?displayProperty=fullName> 属性使执行数据流块一次处理多条消息。  当数据流块需要执行长时间运行的计算并且可从并行处理消息中获益时，这种做法很有用。  此示例使用 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=fullName> 类并发执行多个数据流操作；但是，您可以对 TPL 数据流库提供的任何预定义的执行块类型（<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>、<xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=fullName>）指定最大并行度。  
  
> [!TIP]
>  TPL 数据流库（<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间）不随 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 一起分配。  若要安装 <xref:System.Threading.Tasks.Dataflow> 命名空间，请打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] 中的项目，从“项目”菜单选择**管理 NuGet 包**，然后在线搜索 `Microsoft.Tpl.Dataflow` 包。  
  
## 示例  
 下面的示例执行两个数据流计算并输出每个计算所需的运行时间。  第一个计算指定最大并行度为 1，这是默认值。  最大并行度 1 会使数据流块按顺序处理消息。  第二个计算与第一个类似，但指定的最大并行度与可用处理器的数量相等。  这使数据流块能够并行执行多个操作。  
  
 [!code-csharp[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_degreeofparallelism/cs/dataflowdegreeofparallelism.cs#1)]
 [!code-vb[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_degreeofparallelism/vb/dataflowdegreeofparallelism.vb#1)]  
  
## 编译代码  
 复制代码示例并将其粘贴到 Visual Studio 项目中，或粘贴到一个名为 `DataflowDegreeOfParallelism.cs`（对于 则为 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `DataflowDegreeOfParallelism.vb`）的文件中，然后在 Visual Studio 命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.vb**  
  
## 可靠编程  
 默认情况下，每个预定义的数据流块会按照接收消息的顺序将消息传播出去。  虽然在指定的最大并行度大于 1 时会同时处理多条消息，但这些消息仍然按被接收的顺序进行传播。  
  
 由于 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A> 属性表示最大并行度，因此数据流块执行时的并行度可能小于指定的值。  为了满足功能需求或需要考虑可用系统资源不足的问题时，数据流块可以使用较小的并行度。  数据流块选择的并行度从不会大于您指定的值。  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)