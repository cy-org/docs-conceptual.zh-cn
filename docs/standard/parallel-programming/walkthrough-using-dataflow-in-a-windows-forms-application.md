---
title: "Walkthrough: Using Dataflow in a Windows Forms Application | Microsoft Docs"
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
  - "TPL dataflow library, in Windows Forms"
  - "Task Parallel Library, dataflows"
  - "Windows Forms, and TPL"
ms.assetid: 9c65cdf7-660c-409f-89ea-59d7ec8e127c
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Walkthrough: Using Dataflow in a Windows Forms Application
文档演示如何创建在 Windows 窗体应用程序中执行图像处理的数据流网络块。  
  
 此示例从指定的文件夹加载图像文件，生成复合映像，并显示结果。  本示例使用数据流模型在网络上路由图像。  在数据流模型中，程序的各个独立组件通过发送消息来互相通信。  当某个组件收到消息时，它执行某项操作然后将结果传递给另一个组件。  相比之下，在控制流模型中，应用程序使用控制结构（例如条件语句和循环等等）控制程序中操作的顺序。  
  
## 系统必备  
 在开始本演练之前，请阅读 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)这一主题。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从项目菜单中选择“Manage NuGet Packages”，并在线搜索`Microsoft.Tpl.Dataflow`包。  
  
## 各节内容  
 本演练包含以下各节：  
  
-   [创建 Windows 窗体应用程序](#winforms)  
  
-   [创建数据流网络](#network)  
  
-   [为用户界面 \(UI\) 连接数据流网络](#ui)  
  
-   [完整示例](#complete)  
  
<a name="winforms"></a>   
## 创建 Windows 窗体应用程序  
 本节描述如何创建基本的 Windows 窗体应用程序并将控件添加到主窗体。  
  
#### 创建 Windows 窗体应用程序  
  
1.  在[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中创建一个[!INCLUDE[csprcs](../../../includes/csprcs-md.md)]或Visual Basic“Windows窗体应用程序 项目。  在本文档，该项目命名为 `CompositeImages`。  
  
2.  在主窗体的窗体设计器，Form1.cs \([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]的Form1.vb \)，和四个 <xref:System.Windows.Forms.ToolStrip> 控件中。  
  
3.  向 <xref:System.Windows.Forms.ToolStrip>控件添加  <xref:System.Windows.Forms.ToolStripButton>控件。  将 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A>属性设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 而 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为选择文件夹 。  
  
4.  向 <xref:System.Windows.Forms.ToolStrip>控件添加第二个 <xref:System.Windows.Forms.ToolStripButton> 控件。  将 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle>，<xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为清除而 <xref:System.Windows.Forms.ToolStripItem.Enabled%2A> 属性设置为 `False`。  
  
5.  向主窗体添加 <xref:System.Windows.Forms.PictureBox> 对象。  将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
<a name="network"></a>   
## 创建数据流网络  
 本节介绍如何创建执行图像处理的数据流网络。  
  
#### 创建数据流网络  
  
1.  在项目中，向 System.Threading.Tasks.Dataflow.dll 添加引用。  
  
2.  确保 Form1.cs \( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]的 Form1.vb\) 包含下面的 `using` \(在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中的`Using` \) 语句。  
  
     [!code-csharp[TPLDataflow_CompositeImages#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#1)]  
  
3.  将以下数据成员添加到`Form1`类中。  
  
     [!code-csharp[TPLDataflow_CompositeImages#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#2)]  
  
4.  将下面的 `CreateImageProcessingNetwork` 方法添加到 `Form1` 类。  此方法创建图像处理网络。  
  
     [!code-csharp[TPLDataflow_CompositeImages#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#3)]  
  
5.  实现 `LoadBitmaps` 方法。  
  
     [!code-csharp[TPLDataflow_CompositeImages#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#4)]  
  
6.  实现 `CreateCompositeBitmap` 方法。  
  
     [!code-csharp[TPLDataflow_CompositeImages#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#5)]  
  
    > [!NOTE]
    >  `CreateCompositeBitmap` 方法的 C\# 版本使用指针可以高效处理 <xref:System.Drawing.Bitmap?displayProperty=fullName> 对象。  为了使用 [unsafe](../Topic/unsafe%20\(C%23%20Reference\).md) 关键字，必须在项目中启用 "允许不安全代码" 选项。  有关如何在 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 项目中启用不安全代码的更多信息，请参见 [“项目设计器”\-\>“生成”页 \(C\#\)](../Topic/Build%20Page,%20Project%20Designer%20\(C%23\).md)。  
  
 下表描述了网络中的成员。  
  
|成员|类型|说明|  
|--------|--------|--------|  
|`loadBitmaps`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|将文件夹路径作为输入并生成 <xref:System.Drawing.Bitmap> 对象的集合作为输出。|  
|`createCompositeBitmap`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|将 <xref:System.Drawing.Bitmap> 对象的集合作为输入并生成复合位图作为输出。|  
|`displayCompositeBitmap`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|窗体上显示复合位图。|  
|`operationCancelled`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|显示图像以表示操作取消并使用户能选择其他文件夹。|  
  
 若要连接数据块以形成"数据流网络，此示例使用了 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法。  <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法包含采用 <xref:System.Predicate%601> 对象确定目标块是接受还是拒绝消息的重载版本。  此筛选机制启用到消息块以确保只接收特定值。  在本示例中，网络能够有两种方式进行分支。  主分支从磁盘加载图像，创建复合映像并在窗体上显示该图像。  备用分支取消当前操作。  <xref:System.Predicate%601> 使对象通过主分支启用数据流块，通过转换到备用分支拒绝某些消息。  例如，如果用户取消操作，数据流块 `createCompositeBitmap` 生成 `null` \( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中的`Nothing` \) 作为其输出。  数据流块 `displayCompositeBitmap` 被拒绝 `null` 输入了值，并且，消息提供给 `operationCancelled`。  数据流块 `operationCancelled` 接受所有消息，并显示图像来提示操作取消。  
  
 下图显示图像处理网络：  
  
 ![图像处理网络](../../../docs/standard/parallel-programming/media/dataflowwinforms.png "DataflowWinForms")  
  
 因为`displayCompositeBitmap` 和 `operationCancelled`数据流块在用户界面操作，此操作在用户界面线程上发生这一点很重要。  为此，在构造期间，这些对象将提供 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> 属性设置为 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName>的 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 对象。  <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName> 方法创建对当前同步上下文的 <xref:System.Threading.Tasks.TaskScheduler> 对象。  由于 `CreateImageProcessingNetwork` 方法是通过选取文件夹按钮的处理程序调用的，运行于用户界面线程上，`displayCompositeBitmap` 和 `operationCancelled` 数据流块同样也在用户界面线程运行。  
  
 此示例使用共享的取消标记而不是设置 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 属性，因为 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 属性中永久取消了数据流执行块。  即使当用户取消一个或多个操作，取消标记使此示例能多次重新使用同一数据流网络。  有关使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 永久移除数据流执行块的示例，请参见 [How to: Cancel a Dataflow Block](../../../docs/standard/parallel-programming/how-to-cancel-a-dataflow-block.md)。  
  
<a name="ui"></a>   
## 为用户界面 \(UI\) 连接数据流网络  
 本节介绍如何将数据流网络与用户界面连接。  复合映像的操作创建和移操作除是由选定文件和取消按钮启动的。  当用户任意选择其中一个按钮时，相应的操作以异步方式启动。  
  
#### 为用户界面 \(UI\) 连接数据流网络  
  
1.  在主窗体的窗体设计器，为 <xref:System.Windows.Forms.ToolStripItem.Click> 事件创建一个选择文件夹按钮的事件处理程序。  
  
2.  实现选取文件夹按钮的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。  
  
     [!code-csharp[TPLDataflow_CompositeImages#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#6)]  
  
3.  在主窗体的窗体设计器，为 <xref:System.Windows.Forms.ToolStripItem.Click> 事件创建一个取消按钮的事件处理程序。  
  
4.  实现取消按钮的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。  
  
     [!code-csharp[TPLDataflow_CompositeImages#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#7)]  
  
<a name="complete"></a>   
## 完整示例  
 下面的示例显示了整个完整代码。  
  
 [!code-csharp[TPLDataflow_CompositeImages#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#100)]  
  
 下面的插图显示公共路径\\Sample Pictures \\folder的典型输出。  
  
 ![Windows 窗体应用程序](../../../docs/standard/parallel-programming/media/tpldataflow-compositeimages.gif "TPLDataflow\_CompositeImages")  
  
## 后续步骤  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)