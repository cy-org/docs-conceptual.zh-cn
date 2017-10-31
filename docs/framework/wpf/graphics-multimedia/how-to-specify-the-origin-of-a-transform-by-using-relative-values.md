---
title: "如何：使用相对值指定变换原点 | Microsoft Docs"
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
  - "图形, 转换的来源"
  - "转换的来源"
  - "转换, 来源"
ms.assetid: f4dbc29d-93c7-41cd-96d8-5cfd8624b470
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用相对值指定变换原点
此示例演示如何使用相对值来指定应用于 <xref:System.Windows.FrameworkElement> 的 <xref:System.Windows.UIElement.RenderTransform%2A> 的原点。  
  
 使用 <xref:System.Windows.UIElement.RenderTransform%2A> 属性旋转、按比例缩放或[扭曲](GTMT)一个 <xref:System.Windows.FrameworkElement> 时，默认设置会在元素的左上角应用变换。  如果要从元素中心进行旋转、按比例缩放或扭曲，则可以通过将变换中心设置为元素中心来进行补偿。  但是，该解决方案要求您知道元素的大小。  在元素中心应用变换的一种较简单的方法是将其 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性设置为 \(0.5, 0.5\)，而不是在变换本身上设置中心值。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.RotateTransform> 将 <xref:System.Windows.Controls.Button> 沿顺时针方向旋转 45 度。  由于示例未指定中心，因此按钮将围绕点 \(0, 0\)（即按钮的左上角）旋转。  <xref:System.Windows.Media.RotateTransform> 应用于 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
 下图显示了以下示例的变换结果。  
  
 ![使用 RenderTransform 变换的按钮](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm\_RenderTransformWithDefaultCenter")  
使用 RenderTransform 属性沿顺时针方向旋转 45 度  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 下一个示例也使用 <xref:System.Windows.Media.RotateTransform> 将 <xref:System.Windows.Controls.Button> 沿顺时针方向旋转 45 度；但它将按钮的 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 设置为 \(0.5, 0.5\)。  因此，将在按钮的中心（而不是其左上角）应用旋转。  
  
 下图显示了以下示例的变换结果。  
  
 ![围绕中心变换的按钮](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformrelativecenter.png "graphicsmm\_RenderTransformRelativeCenter")  
将 RenderTransform 属性与值为 \(0.5, 0.5\) 的 RenderTransformOrigin 结合使用以旋转 45 度  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 有关变换 <xref:System.Windows.FrameworkElement> 对象的更多信息，请参见[变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)