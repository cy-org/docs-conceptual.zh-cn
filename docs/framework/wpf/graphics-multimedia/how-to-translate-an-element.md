---
title: "如何：平移元素 | Microsoft Docs"
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
  - "类, TranslateTransform"
  - "图形, 翻译"
  - "TranslateTransform 类"
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：平移元素
此示例演示如何通过使用 <xref:System.Windows.Media.TranslateTransform> 平移（移动）元素。  
  
 <xref:System.Windows.Media.TranslateTransform> 类对移动不支持绝对定位的面板内的元素特别有用。  例如，通过将 <xref:System.Windows.Media.TranslateTransform> 应用到元素的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性，可以移动 <xref:System.Windows.Controls.StackPanel> 或 <xref:System.Windows.Controls.DockPanel> 内的元素。  
  
 使用 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性指定将元素沿 X 轴移动的量（以[像素](GTMT)为单位）。  使用 <xref:System.Windows.Media.TranslateTransform.Y%2A> 属性指定将元素沿 Y 轴移动的量（以像素为单位）。  最后，将 <xref:System.Windows.Media.TranslateTransform> 应用于元素的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
 下面的示例使用 <xref:System.Windows.Media.TranslateTransform> 将元素向右移动 50 个[像素](GTMT) 并向下移动 50 个像素。  
  
## 示例  
 [!code-xml[transformsSample#53](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 有关完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  
  
## 请参阅  
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)