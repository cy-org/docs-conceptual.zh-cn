---
title: "如何：创建自定义 Panel 元素 | Microsoft Docs"
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
  - "自定义 Panel 元素"
  - "Panel 控件"
ms.assetid: e0df4f1e-8c07-4e86-89a3-e22acfffdc2a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建自定义 Panel 元素
## 示例  
 本示例演示如何覆盖 <xref:System.Windows.Controls.Panel> 元素的默认布局行为和创建派生自 <xref:System.Windows.Controls.Panel> 的自定义布局元素。  
  
 本示例定义一个名为 `PlotPanel` 的简单的自定义 <xref:System.Windows.Controls.Panel> 元素，该元素依照两个硬编码的 x 和 y 坐标定位子元素。  在此示例中，`x` 和 `y` 均被设置为 `50`；因此，所有子元素均放置在 x 和 y 轴上的该位置处。  
  
 为了实现自定义的 <xref:System.Windows.Controls.Panel> 行为，此示例使用了 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法。  每个方法均返回定位和呈现子元素所需的 <xref:System.Windows.Size> 数据。  
  
 [!code-cpp[PlotPanel#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Panel>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Create a Custom Content\-Wrapping Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159979)