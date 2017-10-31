---
title: "How to: Write Messages to and Read Messages from a Dataflow Block | Microsoft Docs"
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
  - "TPL dataflow library, reading and writing messages"
ms.assetid: 1a9bf078-aa82-46eb-b95a-f87237f028c5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Write Messages to and Read Messages from a Dataflow Block
本文档描述如何使用TPL 数据流库将消息写入和从数据流块中读取消息。  TPL 数据流库提供数据流消息写入和读取的同步和异步方法。  文档使用 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601?displayProperty=fullName> 类。  <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 类缓存消息即作为消息源也作为消息目标。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 同步从数据流块中读取和写入  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法将数据流块写入到 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> ， <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> 方法从相同的对象读取。  
  
 [!code-csharp[TPLDataflow_ReadWrite#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#2)]
 [!code-vb[TPLDataflow_ReadWrite#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#2)]  
  
 如以下示例所示，您还可以使用 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法读取数据流块。  <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法不会阻止当前线程，偶尔轮询数据时非常有用。  
  
 [!code-csharp[TPLDataflow_ReadWrite#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#3)]
 [!code-vb[TPLDataflow_ReadWrite#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#3)]  
  
 由于 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法同步操作，在前面示例的 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象在第二个循环读取数据之前接收所有数据。  下面的示例通过使用 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 同时读写消息块，是第一个示例的扩展。  由于 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 的同时执行，值就不会被以特定顺序写入到任何<xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象。  
  
 [!code-csharp[TPLDataflow_ReadWrite#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#4)]
 [!code-vb[TPLDataflow_ReadWrite#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#4)]  
  
## 异步读写数据流块  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> 方法异步写入 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 对象，<xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> 方法异步读取同一对象。  此示例使用 [async](../Topic/async%20\(C%23%20Reference\).md) 和[await](../Topic/await%20\(C%23%20Reference\).md) 操作 \(在 Visual Basic 中为[Async](../Topic/Async%20\(Visual%20Basic\).md)和 [Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md)） 对目标块进行异步读写。  当必须使用数据流块推迟消息时，<xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> 方法会很有用。  当要操作变为可用的数据时，<xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> 方法会很有用。  有关在消息块中传播消息的方式的更多信息，请参见位于 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)消息传递章节。  
  
 [!code-csharp[TPLDataflow_ReadWrite#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#5)]
 [!code-vb[TPLDataflow_ReadWrite#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#5)]  
  
## 完整的示例  
 下面的示例显示了该文档的完整代码。  
  
 [!code-csharp[TPLDataflow_ReadWrite#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#1)]
 [!code-vb[TPLDataflow_ReadWrite#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#1)]  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DataflowReadWrite.cs` \(`DataflowReadWrite.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.vb**  
  
## 后续步骤  
 此示例演示如何直接读写消息块。  也可以连接数据流块以形成 *管线*，这是数据流线性序列块，或 *网络*，这是数据流图块。  在管线或网络中，当数据可用时源向目标异步传播数据。  有关创建基本数据流管道的示例，请参见 [Walkthrough: Creating a Dataflow Pipeline](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md)。  有关创建更复杂的数据流网络的示例，请参见 [Walkthrough: Using Dataflow in a Windows Forms Application](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)