---
title: "如何：使用缓存的元素作为画笔 | Microsoft Docs"
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
  - "BitmapCache [WPF], using"
  - "BitmapCacheBrush [WPF], using"
  - "缓存的元素 [WPF], 用作画笔"
  - "CacheMode [WPF], using"
ms.assetid: d36e944a-866e-4baf-98c4-fd6a75f6fdd0
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用缓存的元素作为画笔
使用 <xref:System.Windows.Media.BitmapCacheBrush> 类可以高效地重用缓存的元素。  若要缓存元素，请创建 <xref:System.Windows.Media.BitmapCache> 类的新实例，并将其分配给元素的 <xref:System.Windows.UIElement.CacheMode%2A> 属性。  
  
## 示例  
 下面的代码示例演示如何重用缓存的元素。  缓存的元素是一个显示大图像的 <xref:System.Windows.Controls.Image> 控件。  将使用 <xref:System.Windows.Media.BitmapCache> 类以位图的形式缓存 <xref:System.Windows.Controls.Image> 控件，并通过将缓存分配给 <xref:System.Windows.Media.BitmapCacheBrush> 来重用缓存。  画笔将分配给 25 个按钮的背景来显示高效的重用。  
  
 [!code-xml[System.Windows.Media.BitmapCacheBrush#_BitmapCacheBrushXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcachebrush/cs/window1.xaml#_bitmapcachebrushxaml)]  
  
## 请参阅  
 <xref:System.Windows.Media.BitmapCache>   
 <xref:System.Windows.Media.BitmapCacheBrush>   
 <xref:System.Windows.UIElement.CacheMode%2A>   
 [如何：通过缓存元素来改善呈现性能](../../../../docs/framework/wpf/graphics-multimedia/how-to-improve-rendering-performance-by-caching-an-element.md)