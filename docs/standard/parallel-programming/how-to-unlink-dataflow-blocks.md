---
title: "How to: Unlink Dataflow Blocks | Microsoft Docs"
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
  - "dataflow blocks, unlinking in TPL"
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, unlinking dataflow blocks"
ms.assetid: 40f0208d-4618-47f7-85cf-4913d07d2d7d
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Unlink Dataflow Blocks
本文档描述如何取消源与目标数据流块的链接。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 示例  
 下面的示例创建了三个 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象，其中每个调用 `TrySolution` 方法计算值。  此示例只需要从第一次调用`TrySolution` 到结束的结果。  
  
 [!code-csharp[TPLDataflow_ReceiveAny#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_receiveany/cs/dataflowreceiveany.cs#1)]
 [!code-vb[TPLDataflow_ReceiveAny#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_receiveany/vb/dataflowreceiveany.vb#1)]  
  
 为了收到第一 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 对象完成的值，该示例定义了 `ReceiveFromAny(T)` 方法。  `ReceiveFromAny(T)` 方法接受一个 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 对象数据并将每个对象链接到 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 对象。  当使用 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法将源数据流流块链接给目标块时，源传播消息到目标的信息作为可用数据。  因为 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 类只接受提供它的第一条消息，`ReceiveFromAny(T)` 方法通过调用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> 方法生成其结果。  产生提供给 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 对象的第一条消息。  <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法具有接受 <xref:System.Boolean> 参数的重载版本， `unlinkAfterOne`设置为 `True`，则指示源块在目标收到来自源的消息后从目标断开链接。  <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 对象跟源断开链接很重要，因为 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 对象和源数组之间的关系在 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 对象接收消息后就不再需要。  
  
 启动剩下的 `TrySolution` 调用直至结束，在其中一个估计值之后， `TrySolution` 方法使用在调用`ReceiveFromAny(T)` 之后取消的<xref:System.Threading.CancellationToken> 对象返回。  当 <xref:System.Threading.CancellationToken> 对象移除时，<xref:System.Threading.SpinWait.SpinUntil%2A> 方法返回。  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DataflowReceiveAny.cs` \(`DataflowReceiveAny.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReceiveAny.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReceiveAny.vb**  
  
## 可靠编程  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)