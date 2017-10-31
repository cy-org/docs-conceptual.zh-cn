---
title: "如何：使用视频绘制区域 | Microsoft Docs"
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
  - "画笔, 使用视频进行绘制"
  - "使用视频进行绘制"
  - "视频, 绘制"
ms.assetid: 04dd6600-4a6e-4b43-a93e-21cce7dfbcb8
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用视频绘制区域
此示例演示如何绘制带有媒体的区域。  若要绘制带有媒体的区域，一种方法就是结合使用 <xref:System.Windows.Controls.MediaElement> 和 <xref:System.Windows.Media.VisualBrush>。  使用 <xref:System.Windows.Controls.MediaElement> 加载和播放媒体，再使用该元素来设置 <xref:System.Windows.Media.VisualBrush> 的 <xref:System.Windows.Media.VisualBrush.Visual%2A> 属性，  然后可以使用 <xref:System.Windows.Media.VisualBrush> 来绘制带有已加载媒体的区域。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Controls.MediaElement> 和 <xref:System.Windows.Media.VisualBrush> 来绘制带有视频的 <xref:System.Windows.Controls.TextBlock> 控件的 <xref:System.Windows.Controls.TextBlock.Foreground%2A>。  此示例将 <xref:System.Windows.Controls.MediaElement> 的 <xref:System.Windows.Controls.MediaElement.IsMuted%2A> 属性设置为 `true`，使它不发出声音。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundinline)]
 [!code-xml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundinline)]  
  
## 示例  
 由于 <xref:System.Windows.Media.VisualBrush> 是从 <xref:System.Windows.Media.TileBrush> 类继承的，因此它可以提供多种平铺模式。  通过将 <xref:System.Windows.Media.VisualBrush> 的 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性设置为 <xref:System.Windows.Media.TileMode>，并将它的 <xref:System.Windows.Media.TileBrush.Viewport%2A> 属性设置为小于正在绘制的区域的值，可以创建图块图案。  
  
 下面的示例与上一个示例基本相同，二者的区别在于 <xref:System.Windows.Media.VisualBrush> 根据视频生成模式。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-xml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundtiledinline)]  
  
 有关如何向应用程序添加内容文件（如媒体文件）的信息，请参见 [WPF 应用程序资源、内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)。  在添加媒体文件时，必须将其作为内容文件（而非资源文件）添加。  
  
## 请参阅  
 <xref:System.Windows.Media.VisualBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [TileBrush 概述](../../../../docs/framework/wpf/graphics-multimedia/tilebrush-overview.md)   
 [多媒体概述](../../../../docs/framework/wpf/graphics-multimedia/multimedia-overview.md)