---
title: "如何：定位网格的子元素 | Microsoft Docs"
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
  - "Grid 控件, 定位子元素"
ms.assetid: 27b3ba9b-ad32-44e2-bcab-a79d573a463c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：定位网格的子元素
下面的示例演示如何使用针对 <xref:System.Windows.Controls.Grid> 定义的 get 和 set 方法来定位子元素。  
  
## 示例  
 下面的示例定义了一个包含三列和三行的 <xref:System.Windows.Controls.Grid> 父元素 \(`grid1`\)，  并将一个 <xref:System.Windows.Shapes.Rectangle> 子元素 \(`rect1`\) 添加到 <xref:System.Windows.Controls.Grid> 中行坐标和列坐标分别为零的位置。  <xref:System.Windows.Controls.Button> 元素表示一些方法，通过调用这些方法可以在 <xref:System.Windows.Controls.Grid> 中重定位 <xref:System.Windows.Shapes.Rectangle> 元素。  当用户单击某个按钮时，相关的方法会被激活。  
  
 [!code-xml[gridGetSetMethods#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml#1)]  
  
 下面的代码隐藏示例处理由按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件所引发的方法。  该示例将这些方法调用写入 <xref:System.Windows.Controls.TextBlock> 元素，这些元素使用相关的 get 方法以字符串形式输出新属性值。  
  
 [!code-csharp[gridGetSetMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[gridGetSetMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridGetSetMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)