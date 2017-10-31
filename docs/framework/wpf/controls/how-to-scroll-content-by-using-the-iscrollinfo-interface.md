---
title: "如何：使用 IScrollInfo 接口来滚动内容 | Microsoft Docs"
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
  - "滚动内容"
  - "ScrollViewer 控件, 滚动内容"
ms.assetid: d8700bef-a3f8-4c12-9de2-fc3b79f32cd3
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 IScrollInfo 接口来滚动内容
此示例演示如何使用 <xref:System.Windows.Controls.Primitives.IScrollInfo> 接口来滚动内容。  
  
## 示例  
 下面的示例演示 <xref:System.Windows.Controls.Primitives.IScrollInfo> 接口的功能。  该示例使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 创建了一个嵌套在父 <xref:System.Windows.Controls.ScrollViewer> 中的 <xref:System.Windows.Controls.StackPanel> 元素。  <xref:System.Windows.Controls.StackPanel> 的子元素逻辑上可以使用由 <xref:System.Windows.Controls.Primitives.IScrollInfo> 接口定义的方法进行滚动，并且可以在代码中强制转换为 <xref:System.Windows.Controls.StackPanel> \(`sp1`\) 的实例。  
  
 [!code-xml[IScrollInfoMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml#2)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中的每个 <xref:System.Windows.Controls.Button> 将触发一个相关的自定义方法，该方法控制 <xref:System.Windows.Controls.StackPanel> 中的滚动行为。  下面的示例演示如何使用 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> 和 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A> 方法；它还大概地演示了如何使用 <xref:System.Windows.Controls.Primitives.IScrollInfo> 类定义的所有定位方法。  
  
 [!code-csharp[IScrollInfoMethods#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.Primitives.IScrollInfo>   
 <xref:System.Windows.Controls.StackPanel>   
 [ScrollViewer 概述](../../../../docs/framework/wpf/controls/scrollviewer-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/scrollviewer-how-to-topics.md)   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)