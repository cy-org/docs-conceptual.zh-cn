---
title: "如何：使元素扭曲 | Microsoft Docs"
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
  - "类, SkewTransform"
  - "图形, 扭曲元素"
  - "扭曲元素"
  - "SkewTransform 类"
ms.assetid: 56b65f2f-dc6e-4238-923f-ca44ec53c52f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使元素扭曲
本示例演示如何使用 <xref:System.Windows.Media.SkewTransform> 扭曲元素。  [扭曲](GTMT)（也称为修剪）是一种以非均匀方式拉伸坐标空间的变换。  <xref:System.Windows.Media.SkewTransform> 的一个典型用法是在 [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)] 对象中模拟 [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)] 深度。  
  
 使用 <xref:System.Windows.Media.SkewTransform.CenterX%2A> 和 <xref:System.Windows.Media.SkewTransform.CenterY%2A> 属性可指定 <xref:System.Windows.Media.SkewTransform> 的中心点。  
  
 使用 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 和 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 属性可指定 x 轴和 y 轴的扭曲角度，使当前坐标系沿着这些轴扭曲。  
  
 若要预测扭曲变换的效果，请考虑 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 相对于原始坐标系扭曲 x 轴的值。  因此，如果 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 为 30，则 y 轴绕原点旋转 30 度，将 x 轴的值从该原点扭曲 30 度。  同样，如果 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 为 30，则会将该形状的 y 轴值从原点扭曲 30 度。  请注意，在 x 或 y 轴中将坐标系变换（移动）30 度的效果不相同。  
  
 下面的示例向 <xref:System.Windows.Shapes.Rectangle> 应用自中心点 \(0,0\) 的 45 度水平扭曲。  
  
## 示例  
 [!code-xml[transformsSample#41](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#41)]  
  
 下面的示例向 <xref:System.Windows.Shapes.Rectangle> 应用自中心点 \(25,25\) 的 45 度水平扭曲。  
  
 [!code-xml[transformsSample#42](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#42)]  
  
 下面的示例向 <xref:System.Windows.Shapes.Rectangle> 应用自中心点 \(25,25\) 的 45 度垂直扭曲。  
  
 [!code-xml[transformsSample#43](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#43)]  
  
 下面的图示演示了此示例中使用的不同扭曲。  
  
 ![SkewTransform 示例](../../../../docs/framework/wpf/graphics-multimedia/media/img-wcpsdk-graphicsmm-skewtransformexample.png "img\_wcpsdk\_graphicsmm\_skewtransformexample")  
三个 SkewTransform 示例的图示  
  
 有关完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.SkewTransform>   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)