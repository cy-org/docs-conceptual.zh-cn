---
title: "如何：使用画布的附加属性来定位子元素 | Microsoft Docs"
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
  - "附加属性 [WPF 设计器]"
  - "Canvas 控件, 附加属性"
ms.assetid: 48f1d25d-3820-4107-a4cc-d6c1e5664a44
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用画布的附加属性来定位子元素
本示例演示如何使用 <xref:System.Windows.Controls.Canvas> 的[附加属性](GTMT)来定位子元素。  
  
## 示例  
 下面的示例将四个 <xref:System.Windows.Controls.Button> 元素添加为父 <xref:System.Windows.Controls.Canvas> 的子元素。  每个子元素代表 <xref:System.Windows.Controls.Canvas> 的一个不同附加属性：<xref:System.Windows.Controls.Canvas.Bottom%2A>、<xref:System.Windows.Controls.Canvas.Left%2A>、<xref:System.Windows.Controls.Canvas.Right%2A> 和 <xref:System.Windows.Controls.Canvas.Top%2A>。  每个 <xref:System.Windows.Controls.Button> 通过相对于其父 <xref:System.Windows.Controls.Canvas> 并根据其分配的属性值来定位。  
  
 [!code-cpp[CanvasAttachedProperties#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/CanvasAttachedProperties/CPP/CanvasAttachedProps.cpp#1)]
 [!code-csharp[CanvasAttachedProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasAttachedProperties/CSharp/CanvasAttachedProps.cs#1)]
 [!code-vb[CanvasAttachedProperties#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasAttachedProperties/VisualBasic/CanvasAttachedProps.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.Canvas.Bottom%2A>   
 <xref:System.Windows.Controls.Canvas.Left%2A>   
 <xref:System.Windows.Controls.Canvas.Right%2A>   
 <xref:System.Windows.Controls.Canvas.Top%2A>   
 <xref:System.Windows.Controls.Button>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)   
 [附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)