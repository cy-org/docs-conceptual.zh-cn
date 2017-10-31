---
title: "如何：沿着路径针对对象进行动画处理（点动画） | Microsoft Docs"
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
  - "动画，沿着路径 （点动画） 针对对象"
  - "点动画"
ms.assetid: 1fa3f817-35bc-41a1-b366-f5a20b70da0c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：沿着路径针对对象进行动画处理（点动画）
此示例演示如何使用<xref:System.Windows.Media.Animation.PointAnimationUsingPath>对象进行动画处理<xref:System.Windows.Point>曲线路径上的位置。  
  
## <a name="example"></a>示例  
 以下示例将<xref:System.Windows.Media.EllipseGeometry>沿着路径由定义<xref:System.Windows.Media.PathGeometry>。 椭圆几何图形<xref:System.Windows.Media.EllipseGeometry.Center%2A>属性，它采用<xref:System.Windows.Point>值时，请指定其位置; 移动椭圆几何，动画在其<xref:System.Windows.Media.EllipseGeometry.Center%2A>属性。 该示例使用<xref:System.Windows.Media.Animation.PointAnimationUsingPath>进行动画处理<xref:System.Windows.Media.EllipseGeometry>对象的<xref:System.Windows.Media.EllipseGeometry.Center%2A>属性。  
  
 [!code-xml[PathAnimationGallery_snippet#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/pointanimationusingpathexample.xaml#pointanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/PointAnimationUsingPathExample.cs#pointanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/PointAnimationUsingPathExample.vb#pointanimationusingpathwholepage)]  
  
 有关完整的示例，请参阅[路径动画示例](http://go.microsoft.com/fwlink/?LinkID=160028)。  
  
 上面的示例使用的代码版本<xref:System.Windows.Media.Animation.Storyboard>进行动画处理<xref:System.Windows.Media.EllipseGeometry>，即使应用了仅一个动画。 一个<xref:System.Windows.Media.Animation.Storyboard>通常是简单的方法，因为这些动画可以控制由同一个应用多个动画<xref:System.Windows.Media.Animation.Storyboard>。 但是，使用代码时，向属性应用单个动画的简单方法是使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>方法。 有关示例，请参阅[进行动画处理属性而不使用演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)。  
  
## <a name="see-also"></a>另请参阅  
 [路径动画示例](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [路径动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)