---
title: "如何：使用 GridSplitter 调整列的大小 | Microsoft Docs"
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
  - "网格列, 调整大小"
  - "GridSplitter 控件, 调整网格列的大小"
  - "调整网格列的大小"
ms.assetid: 47b20fe6-7adc-4aa6-9693-b4e184eef74b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用 GridSplitter 调整列的大小
本示例演示如何创建垂直 <xref:System.Windows.Controls.GridSplitter> 以便在不更改 <xref:System.Windows.Controls.Grid> 的尺寸的情况下重新分配 <xref:System.Windows.Controls.Grid> 中两列之间的空间。  
  
## 示例  
 **如何创建覆盖列边缘的 GridSplitter**  
  
 若要指定对 <xref:System.Windows.Controls.Grid> 中相邻列的大小进行调整的 <xref:System.Windows.Controls.GridSplitter>，请将 <xref:System.Windows.Controls.Grid.Column%2A> [附加属性](GTMT)设置为要调整大小的列之一。  如果 <xref:System.Windows.Controls.Grid> 具有多个行，请将 <xref:System.Windows.Controls.Grid.RowSpan%2A> 附加属性设置为行数。  然后，将 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性设置为 <xref:System.Windows.HorizontalAlignment> 或 <xref:System.Windows.HorizontalAlignment>（设置的对齐方式取决于要调整大小的两个列）。  最后，将 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性设置为 <xref:System.Windows.VerticalAlignment>。  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterColumnOverlay](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplittercolumnoverlay)]  
  
 没有自己的列的 <xref:System.Windows.Controls.GridSplitter> 可能会被 <xref:System.Windows.Controls.Grid> 中的其他控件遮盖。  有关如何避免此问题的更多信息，请参见[确保 GridSplitter 可见](../../../../docs/framework/wpf/controls/how-to-make-sure-that-a-gridsplitter-is-visible.md)。  
  
 **如何创建占据一列的 GridSplitter**  
  
 若要指定在 <xref:System.Windows.Controls.Grid> 中占据一列的 <xref:System.Windows.Controls.GridSplitter>，请将 <xref:System.Windows.Controls.Grid.Column%2A> [附加属性](GTMT)设置为要调整大小的列之一。  如果网格具有多个行，请将 <xref:System.Windows.Controls.Grid.RowSpan%2A> 附加属性设置为行数。  然后，将 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 设置为 <xref:System.Windows.HorizontalAlignment>，将 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性设置为 <xref:System.Windows.VerticalAlignment>，将包含 <xref:System.Windows.Controls.GridSplitter> 的列的 <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 设置为 <xref:System.Windows.GridLength.Auto%2A>。  
  
 下面的示例演示如何定义占据一列并对其一侧的列大小进行调整的垂直 <xref:System.Windows.Controls.GridSplitter>。  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterEntireColumnPart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart1)]  
[!code-xml[GridSplitterRowColumn#GridSplitterEntireColumnPart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GridSplitter>   
 [帮助主题](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)