---
title: "How to: Use JoinBlock to Read Data From Multiple Sources | Microsoft Docs"
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
  - "TPL dataflow library, joining blocks in"
  - "dataflow blocks, joining in TPL"
ms.assetid: e9c1ada4-ac57-4704-87cb-2f5117f8151d
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Use JoinBlock to Read Data From Multiple Sources
文档说明当多个源的数可用时时如何使用 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 类来执行操作。  还演示如何使用非贪婪模式允许多个的示例联接块更有效地共享数据源，请参见 。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 示例  
 下面的示例定义三个资源类型、`NetworkResource`、`FileResource`和 `MemoryResource`，然后当资源可用时执行操作。  此示例需要`NetworkResource` 和 `MemoryResource` 对来执行第一个运算和 `FileResource` 和 `MemoryResource` 对执行第二个操作。  所有需求的资源可用时启动这些操作，该示例使用 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 类。  当 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 对象从所有源中接收数据，则会将该数据传播给目标，该示例中为一个 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象。   两个`MemoryResource` 对象都从 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 对象的共享池中读取。  
  
 [!code-csharp[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_nongreedyjoin/cs/nongreedyjoin.cs#1)]
 [!code-vb[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_nongreedyjoin/vb/nongreedyjoin.vb#1)]  
  
 若要使 `MemoryResource` 对象的共享池的高效使用，此示例指定将 <xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions.Greedy%2A> 属性设置为`False`的<xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions> 对象创建在非贪婪模式下操作的 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>对象。   非贪婪的联接块推迟所有传入消息，直至有一种资源可以满足所有的源。  如果任何会推迟的消息被其他块接受，联接块重新启动该进程。  非贪婪模式使链接块共享一个或多个源块来使取得进程的进展，而其他块等待数据。  在此示例中，将`MemoryResource` 对象添加到 `memoryResources`池，接收第二个数据源的第一联接块可以取得进展。  如果此示例是使用贪婪模式，其默认情况下，一个链接块会采用 `MemoryResource` 对象并等待第二个资源变为可用。  但是，如果其他联接块有可用的第二个数据源，不可以取得进展，因为 `MemoryResource` 对象被其他联接块占据。  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DataflowNonGreedyJoin.cs` \(`DataflowNonGreedyJoin.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowNonGreedyJoin.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowNonGreedyJoin.vb**  
  
## 可靠编程  
 使用非贪婪联接还可以有助于防止应用程序中出现死锁。  在软件应用程序中，在两个或更多进程中的每个进程都占用一个资源，并相互等待另一个进程释放一些其他资源时，会发生死锁。  考虑定义两个 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 对象的应用程序。  两个对象每个都从两个的共享源块读取数据。  在贪婪模式中，如果有一个联接块从第一源读取，第二个联接块从第二个源读取，应用程序可能发生死锁，这是因为两个联接块相互等待另外一个释放其资源。  在非贪婪模式，每个联接块只有当所有数据都有效时才从其源读取，因此消除了死锁风险。  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)