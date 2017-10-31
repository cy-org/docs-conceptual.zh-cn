---
title: "如何：重写面板的 OnRender 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "overriding OnRender method"
  - "Panel control, overriding OnRender method"
  - "OnRender method"
  - "controls, Panel, overriding OnRender method"
helpviewer_keywords: 
  - "OnRender 方法, 重写"
  - "重写 Panel 控件的 OnRender 方法"
  - "Panel 控件, 重写 OnRender 方法"
ms.assetid: 57397834-a085-4e36-90ab-416fad98f341
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：重写面板的 OnRender 方法
本示例演示如何覆盖 <xref:System.Windows.Controls.Panel> 的 <xref:System.Windows.Controls.Panel.OnRender%2A> 方法以便将自定义图形效果添加到布局元素中。  
  
## 示例  
 使用 <xref:System.Windows.Controls.Panel.OnRender%2A> 方法以便将图形效果添加到呈现的面板元素中。  例如，可以使用此方法添加自定义边框或背景效果。  <xref:System.Windows.Media.DrawingContext> 对象作为参数传递，该参数可以为绘制形状、文本、图像或视频提供方法。  因此，此方法对于面板对象的自定义项很有帮助。  
  
 [!code-csharp[LightWeightCustomPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LightWeightCustomPanel/CSharp/OffsetPanel.cs#1)]
 [!code-vb[LightWeightCustomPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/LightWeightCustomPanel/visualbasic/offsetpanel.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Panel>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Custom Radial Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159982)   
 [帮助主题](../../../../docs/framework/wpf/controls/panel-how-to-topics.md)