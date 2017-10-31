---
title: "如何：对 Visual 中的几何图形进行命中测试 | Microsoft Docs"
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
  - "几何图形对象, 可视化对象包含"
  - "命中测试, 在组成几何图形对象的可视化对象上"
  - "可视化对象, 命中测试"
ms.assetid: 8bf2643f-d7f9-4cb4-9ea6-5b893c23200d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：对 Visual 中的几何图形进行命中测试
此示例演示如何对由一个或多个 <xref:System.Windows.Media.Geometry> 对象组成的可视化对象执行[命中测试](GTMT)。  
  
## 示例  
 下面的示例演示如何从使用 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 方法的可视化对象中检索 <xref:System.Windows.Media.DrawingGroup>。  随后，此示例对 <xref:System.Windows.Media.DrawingGroup> 中每个绘图所呈现的内容执行命中测试，以确定命中了哪个几何图形。  
  
> [!NOTE]
>  在大多数情况下，您将使用 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 方法来确定点是否与可视化对象的任何呈现内容有交集。  
  
 [!code-csharp[VisualsOverview#VisualsOverviewSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#visualsoverviewsnippet4)]
 [!code-vb[VisualsOverview#VisualsOverviewSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#visualsoverviewsnippet4)]  
  
 <xref:System.Windows.Media.Geometry.FillContains%2A> 方法是一种重载的方法，允许您通过使用指定的 <xref:System.Windows.Point> 或 <xref:System.Windows.Media.Geometry> 进行命中测试。  绘制几何图形时，笔画可以延伸到填充边界之外。  在这种情况下，除了调用 <xref:System.Windows.Media.Geometry.FillContains%2A> 之外，可能还要调用 <xref:System.Windows.Media.Geometry.StrokeContains%2A>。  
  
 您还可以提供一个 <xref:System.Windows.Media.ToleranceType> 以用于贝塞尔拉平操作。  
  
> [!NOTE]
>  此示例不会考虑可能应用到几何图形中的任何变形或剪裁。  此外，此示例不会使用已设置样式的控件，因为这种控件没有与它直接关联的绘图。  
  
## 请参阅  
 [可视化层中的命中测试](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)   
 [将几何图形用作参数的命中测试](../../../../docs/framework/wpf/graphics-multimedia/how-to-hit-test-using-geometry-as-a-parameter.md)