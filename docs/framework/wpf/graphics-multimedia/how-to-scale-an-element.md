---
title: "如何：缩放元素 | Microsoft Docs"
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
  - "类, ScaleTransform"
  - "图形, 缩放元素"
  - "ScaleTransform 类"
  - "缩放, 元素"
ms.assetid: 18158d94-bbe7-4f6a-814e-84d27fa748bf
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：缩放元素
本示例演示如何使用 <xref:System.Windows.Media.ScaleTransform> 来缩放元素。  
  
 使用 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 和 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 属性可以按照指定的系数调整元素的大小。  例如，<xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 值为 1.5 时，会将元素拉伸到其原始宽度的 150%。  <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 值为 0.5 时，会将元素的高度缩小 50%。  
  
 使用 <xref:System.Windows.Media.ScaleTransform.CenterX%2A> 和 <xref:System.Windows.Media.ScaleTransform.CenterY%2A> 属性可以指定缩放操作的中心点。  默认情况下，<xref:System.Windows.Media.ScaleTransform> 的中心点是 \(0,0\)，该点与矩形的左上角相对应。  这会导致该元素移动并使其看上去更大，原因是，当您应用 <xref:System.Windows.Media.Transform> 时，对象所在的坐标空间会改变。  
  
 下面的示例使用 <xref:System.Windows.Media.ScaleTransform> 将长和宽均为 50 的 <xref:System.Windows.Shapes.Rectangle> 的尺寸放大一倍。  对于 <xref:System.Windows.Media.ScaleTransform.CenterX%2A> 和 <xref:System.Windows.Media.ScaleTransform.CenterY%2A> 来说，<xref:System.Windows.Media.ScaleTransform> 的值均为 0（默认值）。  
  
## 示例  
 [!code-xml[transformsSample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#21)]  
  
 通常，可以将 <xref:System.Windows.Media.ScaleTransform.CenterX%2A> 和 <xref:System.Windows.Media.ScaleTransform.CenterY%2A> 设置为缩放的对象的中心 \(<xref:System.Windows.FrameworkElement.Width%2A>\/2, <xref:System.Windows.FrameworkElement.Height%2A>\/2\)。  
  
 下面的示例演示了另一个尺寸放大一倍的 <xref:System.Windows.Shapes.Rectangle>；但是，对于 <xref:System.Windows.Media.ScaleTransform.CenterX%2A> 和 <xref:System.Windows.Media.ScaleTransform.CenterY%2A> 来说，这个 <xref:System.Windows.Media.ScaleTransform> 的值均为 25（与矩形的中心相对应）。  
  
 [!code-xml[transformsSample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#22)]  
  
 下面的插图演示了这两个 <xref:System.Windows.Media.ScaleTransform> 操作之间的区别。  虚线显示的是矩形在缩放之前的大小和位置。  
  
 ![以不同中心点进行的 2x 缩放](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-scalecenter.png "wcpsdk\_graphicsmm\_scalecenter")  
两个具有相同 ScaleX 和 ScaleY 值但是具有不同中心的 ScaleTransform 操作  
  
 有关完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.ScaleTransform>   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)