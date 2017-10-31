---
title: "如何：向绘图应用 GuidelineSet | Microsoft Docs"
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
  - "图形 [WPF], GuidelineSet 属性"
  - "GuidelineSet 属性, 应用于绘图"
ms.assetid: 45f3e0b4-8820-45a7-b865-b8ea5b17b0c8
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：向绘图应用 GuidelineSet
此示例演示如何向 <xref:System.Windows.Media.DrawingGroup> 应用 <xref:System.Windows.Media.GuidelineSet>。  
  
 <xref:System.Windows.Media.DrawingGroup> 类是唯一具有 <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> 属性的 <xref:System.Windows.Media.Drawing> 类型。  若要将 <xref:System.Windows.Media.GuidelineSet> 应用到另一种 <xref:System.Windows.Media.Drawing> 类型，请将其添加到 <xref:System.Windows.Media.DrawingGroup>，然后将 <xref:System.Windows.Media.GuidelineSet> 应用到 <xref:System.Windows.Media.DrawingGroup>。  
  
## 示例  
 下面的示例创建两个几乎相同的 <xref:System.Windows.Media.DrawingGroup> 对象；唯一的区别是：第二个 <xref:System.Windows.Media.DrawingGroup> 具有一个 <xref:System.Windows.Media.GuidelineSet>，而第一个没有。  
  
 下面的插图显示此示例的输出。  由于两个 <xref:System.Windows.Media.DrawingGroup> 对象之间的呈现差别很小，因此绘图的某些部分被放大。  
  
 ![具有和没有 GuidelineSet 的 DrawingGroup](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawinggroup-guidelineset.png "graphicsmm\_drawinggroup\_guidelineset")  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMDrawingGroupGuidelineSetExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupGuidelineSetExample.cs#graphicsmmdrawinggroupguidelinesetexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMDrawingGroupGuidelineSetExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupGuidelineSetExample.xaml#graphicsmmdrawinggroupguidelinesetexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingGroup>   
 <xref:System.Windows.Media.GuidelineSet>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)