---
title: "如何：通过缓存元素来改善呈现性能 | Microsoft Docs"
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
  - "BitmapCache [WPF], 改善呈现性能"
  - "CacheMode [WPF], 改善呈现性能"
  - "性能 [WPF], 缓存元素"
  - "呈现性能 [WPF], 缓存元素"
  - "UIElement [WPF], 缓存"
ms.assetid: 4739c1fc-60ba-4c46-aba6-f6c1a2688f19
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：通过缓存元素来改善呈现性能
使用 <xref:System.Windows.Media.BitmapCache> 类来改善复杂 <xref:System.Windows.UIElement> 的呈现性能。  若要缓存元素，请创建 <xref:System.Windows.Media.BitmapCache> 类的新实例，并将其分配给元素的 <xref:System.Windows.UIElement.CacheMode%2A> 属性。  可以在 <xref:System.Windows.Media.BitmapCacheBrush> 中高效地重用 <xref:System.Windows.Media.BitmapCache>。  
  
## 示例  
 下面的代码示例演示如何创建一个复杂的元素，并将其作为位图进行缓存，从而在对该元素进行动画处理时改善性能。  该元素是一个画布，其中容纳带有多个顶点的形状几何图形。  具有默认值的 <xref:System.Windows.Media.BitmapCache> 将分配给画布的 <xref:System.Windows.UIElement.CacheMode%2A>，并且动画将显示缓存的位图的平滑缩放。  
  
 [!code-xml[System.Windows.Media.BitmapCache#_BitmapCacheXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcache/cs/window1.xaml#_bitmapcachexaml)]  
  
## 请参阅  
 <xref:System.Windows.Media.BitmapCache>   
 <xref:System.Windows.Media.BitmapCacheBrush>   
 <xref:System.Windows.UIElement.CacheMode%2A>   
 [如何：使用缓存的元素作为画笔](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-a-cached-element-as-a-brush.md)