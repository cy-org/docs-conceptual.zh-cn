---
title: "如何：获取 Visual 的偏移量 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "从可视化对象中获取偏移量值"
  - "偏移量值, 从可视化对象中检索"
  - "从可视化对象中检索偏移量值"
  - "可视化对象, 检索偏移量值"
ms.assetid: 889a1dd6-1b11-445a-b351-fbb04c53ee34
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：获取 Visual 的偏移量
这些示例演示如何检索可视化对象相对于其父级、上级或子代的偏移量值。  
  
## 示例  
 下面的标记示例演示了一个使用 <xref:System.Windows.FrameworkElement.Margin%2A> 值 4 定义的 <xref:System.Windows.Controls.TextBlock>。  
  
 [!code-xml[VisualSnippets#VisualSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet1)]  
  
 下面的代码示例演示如何使用 <xref:System.Windows.Media.VisualTreeHelper.GetOffset%2A> 方法检索 <xref:System.Windows.Controls.TextBlock> 的偏移量。  偏移量值包含在返回的 <xref:System.Windows.Vector> 值内。  
  
 [!code-csharp[VisualSnippets#VisualSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet2)]
 [!code-vb[VisualSnippets#VisualSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet2)]  
  
 偏移量考虑了 <xref:System.Windows.FrameworkElement.Margin%2A> 值。  在此例中，<xref:System.Windows.Vector.X%2A> 是 4，<xref:System.Windows.Vector.Y%2A> 也是 4。  
  
 返回的偏移量值相对于 <xref:System.Windows.Media.Visual> 的父级。  如果要让返回的偏移量值不相对于 <xref:System.Windows.Media.Visual> 的父级，请使用 <xref:System.Windows.Media.Visual.TransformToAncestor%2A> 方法。  
  
## 获取相对于上级的偏移量  
 下面的标记示例演示了嵌套在两个 <xref:System.Windows.Controls.StackPanel> 对象中的 <xref:System.Windows.Controls.TextBlock>。  
  
 [!code-xml[VisualSnippets#VisualSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window2.xaml#visualsnippet7)]  
  
 下图演示标记的结果。  
  
 ![对象的偏移量值](../../../../docs/framework/wpf/graphics-multimedia/media/visualoffset-01.png "VisualOffset\_01")  
嵌套在两个 StackPanel 中的 TextBlock  
  
 下面的代码示例演示如何使用 <xref:System.Windows.Media.Visual.TransformToAncestor%2A> 方法检索 <xref:System.Windows.Controls.TextBlock> 相对于包含 <xref:System.Windows.Window> 的偏移量。  偏移量值包含在返回的 <xref:System.Windows.Media.GeneralTransform> 值内。  
  
 [!code-csharp[VisualSnippets#VisualSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet5)]
 [!code-vb[VisualSnippets#VisualSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet5)]  
  
 偏移量考虑了包含 <xref:System.Windows.Window> 中所有对象的 <xref:System.Windows.FrameworkElement.Margin%2A> 值。  在此例中，<xref:System.Windows.Vector.X%2A> 是 28 \(16 \+ 8 \+ 4\)，<xref:System.Windows.Vector.Y%2A> 也是 28。  
  
 返回的偏移量值相对于 <xref:System.Windows.Media.Visual> 的上级。  如果要让返回的偏移量值相对于 <xref:System.Windows.Media.Visual> 的子代，请使用 <xref:System.Windows.Media.Visual.TransformToDescendant%2A> 方法。  
  
## 获取相对于子代的偏移量  
 下面的标记示例演示了 <xref:System.Windows.Controls.StackPanel> 对象中包含的 <xref:System.Windows.Controls.TextBlock>。  
  
 [!code-xml[VisualSnippets#VisualSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml#visualsnippet4)]  
  
 下面的代码示例演示如何使用 <xref:System.Windows.Media.Visual.TransformToDescendant%2A> 方法检索 <xref:System.Windows.Controls.StackPanel> 相对于其子级 <xref:System.Windows.Controls.TextBlock> 的偏移量。  偏移量值包含在返回的 <xref:System.Windows.Media.GeneralTransform> 值内。  
  
 [!code-csharp[VisualSnippets#VisualSnippet9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualSnippets/CSharp/Window1.xaml.cs#visualsnippet9)]
 [!code-vb[VisualSnippets#VisualSnippet9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualSnippets/visualbasic/window1.xaml.vb#visualsnippet9)]  
  
 偏移量将考虑所有对象的 <xref:System.Windows.FrameworkElement.Margin%2A> 值。  在此例中，<xref:System.Windows.Vector.X%2A> 是 \-4，<xref:System.Windows.Vector.Y%2A> 也是 \-4。  因为父对象相对于其子对象进行了负偏移，所以偏移量值为负值。  
  
## 请参阅  
 <xref:System.Windows.Media.Visual>   
 <xref:System.Windows.Media.VisualTreeHelper>   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)