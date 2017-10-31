---
title: "如何：将文本绘制到 Visual 中 | Microsoft Docs"
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
  - "绘图, 文本绘制到可视化效果"
  - "文本, 绘制到可视化效果"
  - "版式, 将文本绘制到可视化效果"
  - "可视化效果, 将文本绘制到"
ms.assetid: fee4003c-e8a6-46ec-babd-2c7f4231a101
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：将文本绘制到 Visual 中
下面的示例演示如何使用 <xref:System.Windows.Media.DrawingContext> 对象将文本绘制到 <xref:System.Windows.Media.DrawingVisual> 中。  通过调用 <xref:System.Windows.Media.DrawingVisual> 对象的 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> 方法，返回绘制上下文。  可以将图形和文本绘制到绘制上下文中。  
  
 若要将文本绘制到绘制上下文中，请使用 <xref:System.Windows.Media.DrawingContext> 对象的 <xref:System.Windows.Media.DrawingContext.DrawText%2A> 方法。  将内容绘制到绘制上下文后，调用 <xref:System.Windows.Media.DrawingContext.Close%2A> 方法来关闭绘制上下文并保存内容。  
  
## 示例  
 [!code-csharp[DrawingVisualSample#110](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#110)]
 [!code-vb[DrawingVisualSample#110](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#110)]  
  
> [!NOTE]
>  有关从中提取上述代码示例的完整代码示例，请参见 [Hit Test Using DrawingVisuals Sample](http://go.microsoft.com/fwlink/?LinkID=159994)（使用 DrawingVisual 的命中测试示例）。