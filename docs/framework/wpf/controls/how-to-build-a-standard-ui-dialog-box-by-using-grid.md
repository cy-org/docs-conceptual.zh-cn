---
title: "如何：使用 Grid 来构建标准的 UI 对话框 | Microsoft Docs"
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
  - "对话框, 创建"
  - "Grid 控件, 创建, 对话框"
ms.assetid: d6ac3d51-844b-4d29-96d8-81a696a7b960
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用 Grid 来构建标准的 UI 对话框
此示例演示如何使用 <xref:System.Windows.Controls.Grid> 元素创建标准的 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 对话框。  
  
## 示例  
 下面的示例创建了一个对话框，该对话框类似于 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 操作系统中的**“运行”**对话框。  
  
 此示例创建 <xref:System.Windows.Controls.Grid> 并使用 <xref:System.Windows.Controls.ColumnDefinition> 和 <xref:System.Windows.Controls.RowDefinition> 类定义了五个列和四个行。  
  
 然后，此示例添加一个 `RunIcon.png` <xref:System.Windows.Controls.Image> 并定位，以表示在此对话框中找到的图像。  该图像放置于 <xref:System.Windows.Controls.Grid> 的第一行和第一列（左上角）中。  
  
 接着，该示例将 <xref:System.Windows.Controls.TextBlock> 元素添加到第一列中，此元素将跨越第一行的其余列。  该示例将另一个 <xref:System.Windows.Controls.TextBlock> 元素添加到第一列中的第二行，以表示**“打开”**文本框。  然后添加 <xref:System.Windows.Controls.TextBlock>，以表示数据输入区域。  
  
 最后，此示例将三个 <xref:System.Windows.Controls.Button> 元素添加到最后一行，这三个元素分别表示**“确定”**、**“取消”**和**“浏览”**事件。  
  
 [!code-csharp[GridRunDialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.GridUnitType>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/grid-how-to-topics.md)