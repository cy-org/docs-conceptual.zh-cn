---
title: "How to: Perform Action When a Dataflow Block Receives Data | Microsoft Docs"
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
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, receiving data"
ms.assetid: fc2585dc-965e-4632-ace7-73dd02684ed3
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Perform Action When a Dataflow Block Receives Data
在接收数据时，*数据流执行块* 类型调用用户提供的委托。  <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=fullName>、<xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=fullName>和 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=fullName> 类是数据流执行块类型。  您可以使用 `delegate` 关键字 \(在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中的`Sub` \)，<xref:System.Action%601>、<xref:System.Func%602>或 lambda 表达式，则可以向数据流执行块提供工作函数。  文档描述如何使用 <xref:System.Func%602> 和 lambda 表达式在执行块中操作。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 示例  
 以下示例使用数据流从磁盘读取文件并计算该文件中等于零的字节数。  它使用 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 读取文件并计算字零的节数，并<xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 打印零的字节数到控制台。  块在接收数据时，<xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象指定 <xref:System.Func%602> 对象执行工作。  <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象使用了 lambda 表达式打印读取到零的字节数到控制台。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#1)]
 [!code-vb[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#1)]  
  
 虽然可以给<xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象提供 lambda 表达式，该示例使用 <xref:System.Func%602> 允许其他代码使用 `CountBytes` 方法。  因为工作时执行特此任务是指定的，不一定比其他代码更有用，<xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象使用 lambda 表达式。  有关表达式 lambda 方式如何在任务并行库中工作的更多信息，请参见 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)。  
  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) 文档中委托类型摘要的章节汇总了可提供给 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>、<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>和 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602> 对象的委托类型。  此表还指出委托类型同步执行还是异步执行。  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DataflowExecutionBlocks.cs` \(`DataflowExecutionBlocks.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowExecutionBlocks.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowExecutionBlocks.vb**  
  
## 可靠编程  
 此示例提供 <xref:System.Func%602> 类型的委托给 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象使数据流执行块的任务同步。  为了使数据流块异步执行操作，请向数据流块提供 <xref:System.Func%601> 类型的委托。  当数据流块异步执行时，数据流块的任务只有在返回的<xref:System.Threading.Tasks.Task%601> 对象完成时才完成。  下面的示例修改   `CountBytes` 方法并使用 [async](../Topic/async%20\(C%23%20Reference\).md) 和 [await](../Topic/await%20\(C%23%20Reference\).md) 操作 \(在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]为[Async](../Topic/Async%20\(Visual%20Basic\).md) 和 [Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md)\) 异步计算提供的文件的零的总字节数。  <xref:System.IO.FileStream.ReadAsync%2A> 方法执行文件读取操作。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#2)]
 [!code-vb[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#2)]  
  
 在数据流执行块中可也以使用异步的 lambda 表达式作为执行操作。  以下示例修改了前面示例用到的 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象，以便使用 lambda 表达式执行异步工作。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#3)]
 [!code-vb[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#3)]  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)