---
title: "如何：定义钢笔 | Microsoft Docs"
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
  - "创建, 钢笔"
  - "钢笔, 定义"
ms.assetid: 7a4f2900-cdf9-49de-84e0-ba5d0ded4d33
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 2
---
# 如何：定义钢笔
本示例演示如何使用 <xref:System.Windows.Media.Pen> 来绘制形状的轮廓。  若要创建一个简单的 <xref:System.Windows.Media.Pen>，只需指定其 <xref:System.Windows.Media.Pen.Thickness%2A> 和 <xref:System.Windows.Media.Pen.Brush%2A> 即可。  通过指定 <xref:System.Windows.Media.Pen.DashStyle%2A>、<xref:System.Windows.Media.Pen.DashCap%2A>、<xref:System.Windows.Media.Pen.LineJoin%2A>、<xref:System.Windows.Media.Pen.StartLineCap%2A> 和 <xref:System.Windows.Media.Pen.EndLineCap%2A>，可以创建更复杂的 Pen。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Pen> 来绘制由 <xref:System.Windows.Media.GeometryDrawing> 定义的形状轮廓。  
  
 [!code-csharp[PenExamples_snip#PenExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PenExamples_snip/CSharp/PenExample.cs#penexamplewholepage)]
 [!code-vb[PenExamples_snip#PenExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PenExamples_snip/VisualBasic/PenExample.vb#penexamplewholepage)]  
  
 ![通过 Pen 产生的轮廓](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple-pen.png "graphicsmm\_simple\_pen")  
GeometryDrawing