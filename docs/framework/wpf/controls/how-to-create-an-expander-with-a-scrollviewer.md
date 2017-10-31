---
title: "如何：使用 ScrollViewer 创建 Expander | Microsoft Docs"
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
  - "控件 [WPF], Expander"
  - "控件 [WPF], ScrollViewer"
  - "Expander 控件, 创建"
  - "ScrollViewer 控件, 使用 Expander 控件"
ms.assetid: 2ad124d2-2406-4157-aaf2-64e067298f01
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 ScrollViewer 创建 Expander
下面的示例演示如何创建包含图像和文本等复杂内容的 <xref:System.Windows.Controls.Expander> 控件。  此示例还在 <xref:System.Windows.Controls.ScrollViewer> 控件中包括 <xref:System.Windows.Controls.Expander> 的内容。  
  
## 示例  
 下面的示例演示如何创建 <xref:System.Windows.Controls.Expander>。  此示例使用包含图像和文本的 <xref:System.Windows.Controls.Primitives.BulletDecorator> 控件，以便对 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 进行定义。  <xref:System.Windows.Controls.ScrollViewer> 控件提供滚动已展开内容的方法。  
  
 请注意，此示例设置的是 <xref:System.Windows.Controls.ScrollViewer>（而不是内容）的 <xref:System.Windows.FrameworkElement.Height%2A> 属性。  如果设置的是内容的 <xref:System.Windows.FrameworkElement.Height%2A>，则 <xref:System.Windows.Controls.ScrollViewer> 不允许用户滚动内容。  <xref:System.Windows.FrameworkElement.Width%2A> 属性是针对 <xref:System.Windows.Controls.Expander> 控件设置的，并且此设置适用于 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 和已展开的内容。  
  
 [!code-xml[ExpanderRichContent#CreateExpander](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#createexpander)]  
  
 [!code-csharp[ExpanderRichContent#CreateExpanderCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#createexpandercode)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Expander>   
 [Expander 概述](../../../../docs/framework/wpf/controls/expander-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/expander-how-to-topics.md)