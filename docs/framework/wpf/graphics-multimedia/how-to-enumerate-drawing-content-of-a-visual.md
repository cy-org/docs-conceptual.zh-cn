---
title: "如何：枚举 Visual 的绘图内容 | Microsoft Docs"
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
  - "枚举 Visual 对象的内容 [WPF]"
  - "检索 Visual 对象的 DrawingGroup 值 [WPF]"
ms.assetid: 2974ddb3-2997-4713-8fd2-e93d549c58a8
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# 如何：枚举 Visual 的绘图内容
<xref:System.Windows.Media.Drawing> 对象提供了用来枚举 <xref:System.Windows.Media.Visual> 内容的对象模型。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 方法来检索 <xref:System.Windows.Media.Visual> 的 <xref:System.Windows.Media.DrawingGroup> 值并枚举该值。  
  
> [!NOTE]
>  您在枚举可视化层的内容时，就是相当于在检索 <xref:System.Windows.Media.Drawing> 对象，而不是以向量图形指令列表形式检索呈现数据的基础表示。  有关更多信息，请参见 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## 请参阅  
 <xref:System.Windows.Media.Drawing>   
 <xref:System.Windows.Media.DrawingGroup>   
 <xref:System.Windows.Media.VisualTreeHelper>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)