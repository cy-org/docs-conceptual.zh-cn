---
title: "How to: Cancel a Dataflow Block | Microsoft Docs"
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
  - "dataflow blocks, canceling in TPL"
  - "TPL dataflow library,canceling dataflow blocks"
ms.assetid: fbddda0d-da3b-4ec8-a1d6-67ab8573fcd7
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Cancel a Dataflow Block
本文档演示如何在应用程序的中启动取消。  此示例使用 Windows 窗体显示工作项于活动状态在数据流管道的位置处并移除的效果。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
### 创建 Windows 窗体应用程序  
  
1.  创建一个 C\# 或Visual Basic “Windows窗体应用程序”  项目。  在下列步骤中，项目命名为 `CancellationWinForms`。  
  
2.  在主窗体的窗体设计器，Form1.cs \([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]的Form1.vb \)，和四个 <xref:System.Windows.Forms.ToolStrip> 控件中。  
  
3.  向 <xref:System.Windows.Forms.ToolStrip>控件添加  <xref:System.Windows.Forms.ToolStripButton>控件。  将 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 并将 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性添加工作项。  
  
4.  向 <xref:System.Windows.Forms.ToolStrip>控件添加第二个 <xref:System.Windows.Forms.ToolStripButton> 控件。  将 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle>，<xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为清除而 <xref:System.Windows.Forms.ToolStripItem.Enabled%2A> 属性设置为 `False`。  
  
5.  向 <xref:System.Windows.Forms.ToolStrip> 控件添加四个 <xref:> System.Windows.Forms.ToolStripProgressBar?qualifyHint=False&autoUpgrade=True 对象。  
  
## 创建数据流管道  
 本节介绍如何创建处理工作项并更新进度栏的数据流管道。  
  
#### 创建管线解决方案  
  
1.  在项目中，向 System.Threading.Tasks.Dataflow.dll 添加引用。  
  
2.  确保 Form1.cs \( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]的 Form1.vb\) 包含下面的 `using` \(在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中的`Imports` \) 语句。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#1)]
     [!code-vb[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#1)]  
  
3.  将 `WorkItem` 类添加为 `Form1` 类的内部类型。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#2)]
     [!code-vb[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#2)]  
  
4.  将以下数据成员添加到`Form1`类中。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#3)]
     [!code-vb[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#3)]  
  
5.  将下面的 `CreatePipeline` 方法添加到 `Form1` 类。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#4)]
     [!code-vb[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#4)]  
  
 因为`incrementProgress` 和 `decrementProgress`数据流块在用户界面操作，此操作在用户界面线程上发生这一点很重要。  为此，在构造期间，这些对象将提供 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> 属性设置为 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName>的 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 对象。  <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName> 方法创建对当前同步上下文的 <xref:System.Threading.Tasks.TaskScheduler> 对象。  因为 `Form1` 构造函数从用户界面线程中调用，`incrementProgress` 和 `decrementProgress` 块中的数据流处理也在用户界面线程运行。  
  
 此示例当成员构造管线时设置 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 属性。  因为 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 属性中永久删除数据流执行块，用户取消操作后必须重新创建整个管道，然后将更多工作项到管线。  有关演示取消数据流块以便在取消操作之后其他工作可运行的一种方法，请参见 [Walkthrough: Using Dataflow in a Windows Forms Application](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)。  
  
## 为用户界面 \(UI\) 连接数据流管道  
 本节介绍如何将数据流管道与用户界面连接。  创建管线和添加工作项到管道通过将工作项添加按钮的事件处理程序中进行控制。  取消按钮启动取消。  当用户任意点击其中一个按钮时，相应的操作以异步方式启动。  
  
#### 为用户界面 \(UI\) 连接数据流管道  
  
1.  在主窗体的窗体设计器中，为添加工作项按钮创建 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。  
  
2.  为添加工作项按钮实现 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#5)]
     [!code-vb[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#5)]  
  
3.  在主窗体的窗体设计器，为 <xref:System.Windows.Forms.ToolStripItem.Click> 事件处理创建一个取消按钮的事件处理程序。  
  
4.  实现取消按钮的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件处理。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#6)]
     [!code-vb[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#6)]  
  
## 示例  
 下面的示例演示为 Form1.cs \( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\)的完整代码。  
  
 [!code-csharp[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#100)]
 [!code-vb[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#100)]  
  
 下图演示运行中的应用程序。  
  
 ![Windows 窗体应用程序](../../../docs/standard/parallel-programming/media/tpldataflow-cancellation.png "TPLDataflow\_Cancellation")  
  
## 可靠编程  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)