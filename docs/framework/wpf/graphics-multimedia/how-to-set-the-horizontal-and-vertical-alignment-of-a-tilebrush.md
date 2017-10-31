---
title: "如何：设置 TileBrush 的水平对齐方式和垂直对齐方式 | Microsoft Docs"
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
  - "对齐, TileBrush"
  - "TileBrush 的水平对齐"
  - "TileBrush, 对齐方式"
  - "TileBrush 的垂直对齐"
ms.assetid: 65ae89bd-9246-4c9e-bde4-2fb991d4060d
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：设置 TileBrush 的水平对齐方式和垂直对齐方式
本示例演示如何控制图块内容的水平对齐方式和垂直对齐方式。  若要控制 <xref:System.Windows.Media.TileBrush> 的水平对齐方式和垂直对齐方式，请使用其 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 和 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性。  
  
 当满足以下任一条件时将使用 <xref:System.Windows.Media.TileBrush> 的 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 和 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性：  
  
-   <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性为 <xref:System.Windows.Media.Stretch> 或 <xref:System.Windows.Media.Stretch>，而 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 和 <xref:System.Windows.Media.TileBrush.Viewport%2A> 的[纵横比](GTMT)不同。  
  
-   <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性为 <xref:System.Windows.Media.Stretch> 并且<xref:System.Windows.Media.TileBrush.Viewbox%2A>和<xref:System.Windows.Media.TileBrush.Viewport%2A>具有不同的大小。  
  
## 示例  
 下面的示例将类型为 <xref:System.Windows.Media.TileBrush> 的 <xref:System.Windows.Media.DrawingBrush> 的内容与其图块的左上角对齐。  为了对齐内容，此示例将 <xref:System.Windows.Media.DrawingBrush> 的 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 属性设置为 <xref:System.Windows.Media.AlignmentX>，将 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性设置为 <xref:System.Windows.Media.AlignmentY>。  该示例产生下面的输出。  
  
 ![左上角对齐的 TileBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tilebrushalignmentexampletopleft.png "graphicsmm\_TileBrushAlignmentExampleTopLeft")  
内容与左上角对齐的 TileBrush  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushtopleftalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushtopleftalignmentinline)]
 [!code-xml[brushoverviewexamples_snip#TileBrushTopLeftAlignmentInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushtopleftalignmentinline)]  
  
## 示例  
 下一个示例通过将 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 属性设置为 <xref:System.Windows.Media.AlignmentX>，将 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性设置为 <xref:System.Windows.Media.AlignmentY>，将 <xref:System.Windows.Media.DrawingBrush> 的内容与其图块的右下角对齐。  该示例产生下面的输出。  
  
 ![右下角对齐的 TileBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tilebrushalignmentexamplebottomright.png "graphicsmm\_TileBrushAlignmentExampleBottomRight")  
内容与右下角对齐的 TileBrush  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushbottomrightalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushbottomrightalignmentinline)]
 [!code-xml[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushbottomrightalignmentinline)]  
  
## 示例  
 下一个示例通过将 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 属性设置为 <xref:System.Windows.Media.AlignmentX>，将 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性设置为 <xref:System.Windows.Media.AlignmentY>，将 <xref:System.Windows.Media.DrawingBrush> 的内容与其图块的左上角对齐。  它还设置了 <xref:System.Windows.Media.DrawingBrush> 的<xref:System.Windows.Media.TileBrush.Viewport%2A>和<xref:System.Windows.Media.TileBrush.TileMode%2A>以生成图块图案。  该示例产生下面的输出。  
  
 ![左上角对齐的平铺 TileBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tilebrushalignmentexampletoplefttiled.png "graphicsmm\_TileBrushAlignmentExampleTopLeftTiled")  
内容与基本图块的左上角对齐的图块图案  
  
 上图突出显示了基本图块，以便显示其内容的对齐方式。  请注意，<xref:System.Windows.Media.TileBrush.AlignmentX%2A> 设置不起作用，因为 <xref:System.Windows.Media.DrawingBrush> 的内容完全水平填充了基本图块。  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushtopleftalignmenttiledinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushtopleftalignmenttiledinline)]
 [!code-xml[brushoverviewexamples_snip#TileBrushTopLeftAlignmentTiledInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushtopleftalignmenttiledinline)]  
  
## 示例  
 最后一个示例通过将 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 属性设置为 <xref:System.Windows.Media.AlignmentX>，将 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性设置为 <xref:System.Windows.Media.AlignmentY>，将已图块的 <xref:System.Windows.Media.DrawingBrush> 的内容与其基本图块的右下角对齐。  该示例产生下面的输出。  
  
 ![右下角对齐的平铺 TileBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tilebrushalignmentexamplebottomrighttiled.png "graphicsmm\_TileBrushAlignmentExampleBottomRightTiled")  
内容与基本图块的右下角对齐的图块图案  
  
 同样，<xref:System.Windows.Media.TileBrush.AlignmentX%2A> 设置不起作用，因为 <xref:System.Windows.Media.DrawingBrush> 的内容完全水平填充了基本图块。  
  
 [!code-csharp[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/TileBrushAlignmentExample.cs#tilebrushbottomrightalignmentinline)]
 [!code-vb[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_snip/visualbasic/tilebrushalignmentexample.vb#tilebrushbottomrightalignmentinline)]
 [!code-xml[brushoverviewexamples_snip#TileBrushBottomRightAlignmentInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileBrushAlignmentExample.xaml#tilebrushbottomrightalignmentinline)]  
  
 这些示例使用 <xref:System.Windows.Media.DrawingBrush> 对象演示如何使用 <xref:System.Windows.Media.TileBrush.AlignmentX%2A> 和 <xref:System.Windows.Media.TileBrush.AlignmentY%2A> 属性。  这些属性的行为对于所有图块画笔都相同：<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.ImageBrush> 和 <xref:System.Windows.Media.VisualBrush>。  有关图块画笔的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingBrush>   
 <xref:System.Windows.Media.ImageBrush>   
 <xref:System.Windows.Media.VisualBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)