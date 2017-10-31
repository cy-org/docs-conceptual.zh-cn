---
title: "如何：使用 BetweenShowDelay 属性 | Microsoft Docs"
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
  - "BetweenShowDelay 时间属性"
  - "ToolTip 控件, BetweenShowDelay 时间属性"
ms.assetid: 984ea76d-f2a2-4326-a02e-f97ec3d036d6
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用 BetweenShowDelay 属性
此示例演示如何使用 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 时间属性，以便在用户将鼠标指针从一个工具提示直接移到另一个工具提示时，工具提示可以快速出现 — 只会稍有延迟或者不会延迟。  
  
## 示例  
 在下面的示例中，对于两个 <xref:System.Windows.Shapes.Ellipse> 控件的工具提示，<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> 属性都设置为一秒（1000 毫秒），并且 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 都设置为两秒（2000 毫秒）。  如果显示其中一个椭圆的工具提示，然后在两秒内将鼠标指针移至并停放在另一个椭圆上，则第二个椭圆的工具提示将立即显示。  
  
 在以下任一方案中，将应用 <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>，这会导致第二个椭圆的工具提示要等待一秒才会出现：  
  
-   如果移到第二个按钮所花的时间长于两秒。  
  
-   如果工具提示在第一个椭圆的时间间隔开始时不可见。  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
[!code-xml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [帮助主题](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)   
 [ToolTip 概述](../../../../docs/framework/wpf/controls/tooltip-overview.md)