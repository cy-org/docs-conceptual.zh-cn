---
title: "Walkthrough: Creating a Custom Dataflow Block Type | Microsoft Docs"
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
  - "TPL dataflow library, creating custom dataflow blocks"
  - "dataflow blocks, creating custom in TPL"
ms.assetid: a6147146-0a6a-4d9b-ab0f-237b3c1ac691
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Walkthrough: Creating a Custom Dataflow Block Type
尽管 TPL 数据流库提供了多种功能的多个数据流块类型，也可以创建自定义块类型。  本文档描述如何创建实现自定义行为块型的数据流。  
  
## 系统必备  
 在阅读文档之前，请阅读[数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) 。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 定义滑动窗口数据流块  
 考虑要求输入值缓存然后输出的滑动窗口的方式的数据流应用程序。  例如，请输入值" {0，1，2，3，4，5}和三个窗口大小。滑动窗口数据流块产生输出数组{0，1，2}，{1，2，3}，{2，3，4}和{，3，4，5}。  以下部分描述两种创建实现自定义行为的数据流块类型。  第一种方法是使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 方法将 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 对象与 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 对象的功能合成一传播器块"  第二种技术定义了从 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602> 派生并组合现有功能来执行自定义行为的类。  
  
## 使用封装方法定义滑动窗口数据流块  
 下面的示例使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 方法根据目标和源创建传播器块  传播器块使源块和目标块能作为数据的接收器和发送方。  
  
 如果需要自定义数据流功能，此方法很有用，但是，您不需要提供其他的方法、属性、字段的类型。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#1)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#1)]  
  
## 从 IPropagatorBlock中派生， 定义滑动窗口数据流块  
 下面的示例演示 `SlidingWindowBlock` 类。  此类从 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602> 派生，所以可以充当数据源和目标。  在前面的示例中，`SlidingWindowBlock` 类是在现有数据流块类型中生成。  不过，`SlidingWindowBlock` 类还实现 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>、<xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>和 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock> 接口需要的方法。  这些方法将所有工作转接给预定义的数据流块类型成员。  例如，`Post` 方法将工作转交给同为 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 对象的 `m_target` 数据成员。  
  
 如果需要自定义数据流功能，此方法很有用，同时也需要提供其他的方法、属性、字段的类型。  例如，`SlidingWindowBlock` 类也是从 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601> 派生，所以可以提供 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 和 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceiveAll%2A> 方法。  `SlidingWindowBlock` 类通过提供 `WindowSize` 属性演示了扩展性，在滑动窗口中检索元素的数目。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#2)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#2)]  
  
## 完整示例  
 下面的示例显示了整个完整代码。  同时演示了如何使用连个滑动窗口，写入块，从中读取数据，并将结果打印到控制台的方法。  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#100)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#100)]  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `SlidingWindowBlock.cs` \(`SlidingWindowBlock.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.vb**  
  
## 后续步骤  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)