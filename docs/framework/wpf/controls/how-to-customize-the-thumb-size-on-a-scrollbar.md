---
title: "如何：自定义滚动条上的滚动块大小 | Microsoft Docs"
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
  - "自定义滚动块大小"
  - "ScrollBar 控件"
  - "滚动块大小"
ms.assetid: fa32b866-5ca1-4e73-85e7-2ac64b80d194
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：自定义滚动条上的滚动块大小
本主题说明如何将 <xref:System.Windows.Controls.Primitives.ScrollBar> 的 <xref:System.Windows.Controls.Primitives.Thumb> 设置为固定大小以及如何为 <xref:System.Windows.Controls.Primitives.ScrollBar> 的 <xref:System.Windows.Controls.Primitives.Thumb> 指定最小大小。  
  
## 示例  
  
## 说明  
 下面的示例创建一个其 <xref:System.Windows.Controls.Primitives.Thumb> 具有固定大小的 <xref:System.Windows.Controls.Primitives.ScrollBar>。  此示例将 <xref:System.Windows.Controls.Primitives.Thumb> 的 <xref:System.Windows.Controls.Primitives.Track.ViewportSize%2A> 属性设置为 <xref:System.Double.NaN>，并设置 <xref:System.Windows.Controls.Primitives.Thumb> 的高度。  若要创建其 <xref:System.Windows.Controls.Primitives.Thumb> 具有固定宽度的水平 <xref:System.Windows.Controls.Primitives.ScrollBar>，请设置 <xref:System.Windows.Controls.Primitives.Thumb> 的宽度。  
  
## 代码  
 [!code-xml[ScrollBarCustomThumbSize#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#1)]  
  
## 说明  
 下面的示例创建一个其 <xref:System.Windows.Controls.Primitives.Thumb> 具有最小大小的 <xref:System.Windows.Controls.Primitives.ScrollBar>。  此示例设置 <xref:System.Windows.SystemParameters.VerticalScrollBarButtonHeightKey%2A> 的值。  若要创建其 <xref:System.Windows.Controls.Primitives.Thumb> 具有最小宽度的水平 <xref:System.Windows.Controls.Primitives.ScrollBar>，请设置 <xref:System.Windows.SystemParameters.HorizontalScrollBarButtonWidthKey%2A>。  
  
## 代码  
 [!code-xml[ScrollBarCustomThumbSize#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#2)]  
  
## 请参阅  
 [ScrollBar 样式和模板](../../../../docs/framework/wpf/controls/scrollbar-styles-and-templates.md)