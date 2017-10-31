---
title: "如何：使用 GridSplitter 调整行的大小 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "网格行, 调整大小"
  - "GridSplitter 控件, 调整网格行的大小"
  - "调整网格行的大小"
ms.assetid: 2413a9f2-1d81-46ed-95cb-95ec8233eea2
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用 GridSplitter 调整行的大小
下面的示例演示如何使用水平 <xref:System.Windows.Controls.GridSplitter> 在不更改 <xref:System.Windows.Controls.Grid> 中维度的情况下重新分配 <xref:System.Windows.Controls.Grid> 中两行之间的空间。  
  
## 示例  
 **如何创建覆盖行边缘的 GridSplitter**  
  
 若要指定对 <xref:System.Windows.Controls.Grid> 中相邻行的大小进行调整的 <xref:System.Windows.Controls.GridSplitter>，请将 <xref:System.Windows.Controls.Grid.Row%2A> [附加属性](GTMT)设置为要调整大小的行之一。  如果 <xref:System.Windows.Controls.Grid> 有多列，请将 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 附加属性设置为指定列数，  然后将 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 设置为 <xref:System.Windows.VerticalAlignment> 或 <xref:System.Windows.VerticalAlignment>（要设置哪一种对齐取决于要调整哪两行的大小），  最后将 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性设置为 <xref:System.Windows.HorizontalAlignment>。  
  
 下面的示例演示如何定义对相邻行的大小进行调整的水平 <xref:System.Windows.Controls.GridSplitter>。  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterRowOverlay](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterrowoverlay)]  
  
 不占据自身行的 <xref:System.Windows.Controls.GridSplitter> 可能会被 <xref:System.Windows.Controls.Grid> 中的其他控件遮盖。  有关如何避免此问题的更多信息，请参见[确保 GridSplitter 可见](../../../../docs/framework/wpf/controls/how-to-make-sure-that-a-gridsplitter-is-visible.md)。  
  
 **如何创建占据一行的 GridSplitter**  
  
 若要指定在 <xref:System.Windows.Controls.Grid> 中占据一行的 <xref:System.Windows.Controls.GridSplitter>，请将 <xref:System.Windows.Controls.Grid.Row%2A> [附加属性](GTMT)设置为要调整大小的行之一。  如果 <xref:System.Windows.Controls.Grid> 有多列，请将 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 附加属性设置为列数，  然后将 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 设置为 <xref:System.Windows.VerticalAlignment>，将 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性设置为 <xref:System.Windows.HorizontalAlignment>，将包含 <xref:System.Windows.Controls.GridSplitter> 的行的 <xref:System.Windows.Controls.RowDefinition.Height%2A> 设置为 <xref:System.Windows.GridLength.Auto%2A>。  
  
 下面的示例演示如何定义占据一行并对任意一侧的行大小进行调整的水平 <xref:System.Windows.Controls.GridSplitter>。  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterEntireRowPart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart1)]  
[!code-xml[GridSplitterRowColumn#GridSplitterEntireRowPart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GridSplitter>   
 [帮助主题](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)