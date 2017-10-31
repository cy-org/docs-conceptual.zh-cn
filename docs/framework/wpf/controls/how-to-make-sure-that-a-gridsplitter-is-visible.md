---
title: "如何：确保 GridSplitter 可见 | Microsoft Docs"
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
  - "GridSplitter 控件, 确保可见性"
ms.assetid: 0a62a964-89c8-48f0-9023-5df721a8cf47
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：确保 GridSplitter 可见
下面的示例演示如何确保 <xref:System.Windows.Controls.GridSplitter> 控件不会被 <xref:System.Windows.Controls.Grid> 中的其他控件隐藏。  
  
## 示例  
 <xref:System.Windows.Controls.Grid> 控件的 <xref:System.Windows.Controls.Panel.Children%2A> 按照它们在标记或代码中的定义顺序呈现。  如果没有将 <xref:System.Windows.Controls.GridSplitter> 控件定义为 <xref:System.Windows.Controls.Panel.Children%2A> 集合中最后面的元素，或者向其他控件给予了更高的 <xref:System.Windows.Controls.Panel.ZIndexProperty>，则其他控件可以隐藏该控件。  
  
 要避免隐藏 <xref:System.Windows.Controls.GridSplitter> 控件，请执行下列操作之一。  
  
-   确保 <xref:System.Windows.Controls.GridSplitter> 控件是添加到 <xref:System.Windows.Controls.Grid> 中的最后一个 <xref:System.Windows.Controls.Panel.Children%2A>。  在下面的示例中，<xref:System.Windows.Controls.GridSplitter> 用作 <xref:System.Windows.Controls.Grid> 的 <xref:System.Windows.Controls.Panel.Children%2A> 集合中的最后一个元素。  
  
 [!code-xml[GridSplitterSnips#GridSplitterLastChild](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterlastchild)]  
  
-   将 <xref:System.Windows.Controls.GridSplitter> 的 <xref:System.Windows.Controls.Panel.ZIndexProperty> 值设置为高于某个控件的值，否则该控件会将其隐藏。  下面的示例赋予给 <xref:System.Windows.Controls.GridSplitter> 控件的 <xref:System.Windows.Controls.Panel.ZIndexProperty> 值大于赋予给 <xref:System.Windows.Controls.Button> 控件的值。  
  
 [!code-xml[GridSplitterSnips#GridSplitterZIndex](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterzindex)]  
  
-   设置控件的边距（否则该控件将会隐藏 <xref:System.Windows.Controls.GridSplitter>），以显示 <xref:System.Windows.Controls.GridSplitter>。  下面的示例将设置控件的边距，否则该控件将会覆盖并隐藏 <xref:System.Windows.Controls.GridSplitter>。  
  
 [!code-xml[GridSplitterSnips#GridSplitterMargin](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplittermargin)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GridSplitter>   
 [帮助主题](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)