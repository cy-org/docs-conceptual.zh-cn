---
title: "如何：使用 ScrollViewer 的内容滚动方法 | Microsoft Docs"
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
  - "IScrollInfo 接口"
  - "滚动方法"
  - "ScrollViewer 控件, 滚动方法"
ms.assetid: 4708cc65-6510-45f8-82e6-30b0d3e30045
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 ScrollViewer 的内容滚动方法
本示例演示如何使用 <xref:System.Windows.Controls.ScrollViewer> 元素的滚动方法。  这些方法在 <xref:System.Windows.Controls.ScrollViewer> 中以行或页为单位提供内容的递增滚动。  
  
## 示例  
 下面的示例创建名为 `sv1` 的 <xref:System.Windows.Controls.ScrollViewer>，用于承载子 <xref:System.Windows.Controls.TextBlock> 元素。  由于 <xref:System.Windows.Controls.TextBlock> 大于父 <xref:System.Windows.Controls.ScrollViewer>，因此将显示滚动条以启用滚动。  代表各种滚动方法的 <xref:System.Windows.Controls.Button> 元素停靠在一个单独的 <xref:System.Windows.Controls.StackPanel> 的左侧。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中的每个 <xref:System.Windows.Controls.Button> 调用一个相关的自定义方法，该方法控制 <xref:System.Windows.Controls.ScrollViewer> 中的滚动行为。  
  
 [!code-xml[ScrollViewerMethods#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml#1)]  
  
 下面的示例使用 <xref:System.Windows.Controls.ScrollViewer.LineUp%2A> 和 <xref:System.Windows.Controls.ScrollViewer.LineDown%2A> 方法。  
  
 [!code-csharp[ScrollViewerMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ScrollViewerMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewerMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.StackPanel>