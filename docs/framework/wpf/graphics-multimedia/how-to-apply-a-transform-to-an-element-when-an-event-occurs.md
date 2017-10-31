---
title: "如何：在事件发生时向元素应用变换 | Microsoft Docs"
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
  - "图形, 作为事件响应的转换"
  - "LayoutTransform 属性"
  - "属性, LayoutTransform"
  - "属性, RenderTransform"
  - "RenderTransform 属性"
  - "作为事件响应的转换"
ms.assetid: 71e4327e-ca57-444c-a3cf-09fb381491a0
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在事件发生时向元素应用变换
本示例演示事件发生时如何应用 <xref:System.Windows.Media.ScaleTransform>。  此处说明的概念与您用于应用其他类型的变换的概念相同。  有关可用变换类型的更多信息，请参见 <xref:System.Windows.Media.Transform> 类或[变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)。  
  
 您可以通过以下两种方式向元素应用变换：  
  
-   如果您不希望变换影响布局，请使用该元素的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
-   如果您希望变换影响布局，请使用该元素的 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 属性。  
  
 下面的示例将 <xref:System.Windows.Media.ScaleTransform> 应用于按钮的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  当鼠标移动到该按钮时，<xref:System.Windows.Media.ScaleTransform> 的 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 和 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 属性将被设置为 `2`，这将导致按钮变大。  当鼠标离开该按钮时，<xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 和 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 将被设置为 `1`，这将导致按钮返回到其原始大小。  
  
## 示例  
 [!code-xml[ButtonTransform#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml#1)]  
  
 [!code-csharp[ButtonTransform#1cb](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml.cs#1cb)]
 [!code-vb[ButtonTransform#1cb](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ButtonTransform/VisualBasic/ButtonTransformExample.xaml.vb#1cb)]  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.ScaleTransform>   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)