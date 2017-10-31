---
title: "如何：创建和使用画布 | Microsoft Docs"
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
  - "Canvas 控件, 创建"
  - "Canvas 控件, using"
  - "控件, Canvas"
ms.assetid: 420b9487-9a15-477c-9489-a22a4dec7779
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：创建和使用画布
此示例演示如何创建和使用 <xref:System.Windows.Controls.Canvas> 的实例。  
  
## 示例  
 下面的示例通过使用 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Canvas.SetTop%2A> 和 <xref:System.Windows.Controls.Canvas.SetLeft%2A> 方法来显式定位两个 <xref:System.Windows.Controls.TextBlock> 元素。  该示例还为 <xref:System.Windows.Controls.Canvas> 指定一种 <xref:System.Windows.Controls.Control.Background%2A> 颜色 `LightSteelBlue`。  
  
> [!NOTE]
>  在使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定位 <xref:System.Windows.Controls.TextBlock> 元素时，使用 <xref:System.Windows.Controls.Canvas.Top%2A> 和 <xref:System.Windows.Controls.Canvas.Left%2A> 属性。  
  
 [!code-csharp[CanvasCode#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasCode/CSharp/Canvas_Code.cs#1)]
 [!code-vb[CanvasCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasCode/VisualBasic/canvas_vb.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.TextBlock>   
 <xref:System.Windows.Controls.Canvas.SetTop%2A>   
 <xref:System.Windows.Controls.Canvas.SetLeft%2A>   
 <xref:System.Windows.Controls.Canvas.Top%2A>   
 <xref:System.Windows.Controls.Canvas.Left%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)