---
title: "如何：设置元素的宽度属性 | Microsoft Docs"
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
  - "Panel 控件, 元素的宽度属性"
  - "宽度属性"
ms.assetid: 6ee04a9d-63f0-4f5b-a406-0a8cd4c35729
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：设置元素的宽度属性
## 示例  
 本示例形象化地演示了 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中与宽度相关的四个属性之间的呈现行为差异。  
  
 <xref:System.Windows.FrameworkElement> 类公开四个属性，用于描述某一元素的宽度特征。  这四个属性可能会相互冲突，如果相互冲突，则按如下顺序确定优先级：<xref:System.Windows.FrameworkElement.MinWidth%2A> 值优先于 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 值，后者又优先于 <xref:System.Windows.FrameworkElement.Width%2A> 值。  第四个属性 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 是只读属性，它报告与布局进程的交互所确定的实际宽度。  
  
 以下[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例绘制了一个 <xref:System.Windows.Shapes.Rectangle> 元素 \(`rect1`\)，作为 <xref:System.Windows.Controls.Canvas> 的子级。  可以使用一系列表示 <xref:System.Windows.FrameworkElement.MinWidth%2A>、<xref:System.Windows.FrameworkElement.MaxWidth%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 属性值的 <xref:System.Windows.Controls.ListBox> 元素更改 <xref:System.Windows.Shapes.Rectangle> 的宽度属性。  通过这种方式，可以直观地显示每个属性的优先级。  
  
 [!code-xml[WidthMinWidthMaxWidth#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#1)]  
[!code-xml[WidthMinWidthMaxWidth#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#2)]  
  
 下面的代码隐藏示例处理 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 事件引发的事件。  每个自定义方法均从<xref:System.Windows.Controls.ListBox>获取输入，将该值分析为<xref:System.Double>，并将其应用于指定的宽度相关属性。  宽度值还可转换为字符串，并写入各种 <xref:System.Windows.Controls.TextBlock> 元素（这些元素的定义未显示在所选 XAML 中）。  
  
 [!code-csharp[WidthMinWidthMaxWidth#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml.cs#3)]
 [!code-vb[WidthMinWidthMaxWidth#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WidthMinWidthMaxWidth/VisualBasic/Window1.xaml.vb#3)]  
  
 有关完整示例，请参见 [Width Properties Comparison Sample](http://go.microsoft.com/fwlink/?LinkID=160050)（宽度属性比较示例）。  
  
## 请参阅  
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.FrameworkElement.ActualWidth%2A>   
 <xref:System.Windows.FrameworkElement.MaxWidth%2A>   
 <xref:System.Windows.FrameworkElement.MinWidth%2A>   
 <xref:System.Windows.FrameworkElement.Width%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [设置元素的高度属性](../../../../docs/framework/wpf/controls/how-to-set-the-height-properties-of-an-element.md)   
 [Width Properties Comparison Sample](http://go.microsoft.com/fwlink/?LinkID=160050)