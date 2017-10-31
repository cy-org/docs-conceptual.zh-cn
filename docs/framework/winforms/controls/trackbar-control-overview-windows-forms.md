---
title: "TrackBar 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "TrackBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "滑块控件, 关于滑块控件"
  - "滑块, 关于滑块"
  - "TrackBar 控件 [Windows 窗体], 关于 TrackBar 控件"
ms.assetid: 95910ecb-8a4c-4776-89fa-206c89ed6973
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# TrackBar 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.TrackBar> 控件（有时也称为“slider”控件）用于在大量信息中进行浏览，或用于以可视的形式调整数值设置。  <xref:System.Windows.Forms.TrackBar> 控件有两部分：滚动块（又称为滑块）和刻度线。  滚动块是可以调整的部分，  其位置与 <xref:System.Windows.Forms.TrackBar.Value%2A> 属性相对应。  刻度线是按规则间隔分隔的可视化指示符。  跟踪条按指定的增量移动并且可以水平或者垂直排列。  例如，可以使用跟踪条来控制系统的鼠标速度或光标闪烁频率。  
  
## 主要属性  
 <xref:System.Windows.Forms.TrackBar> 控件的主要属性包括 <xref:System.Windows.Forms.TrackBar.Value%2A>、<xref:System.Windows.Forms.TrackBar.TickFrequency%2A>、<xref:System.Windows.Forms.TrackBar.Minimum%2A> 和 <xref:System.Windows.Forms.TrackBar.Maximum%2A>。  <xref:System.Windows.Forms.TrackBar.TickFrequency%2A> 为刻度间隔。  <xref:System.Windows.Forms.TrackBar.Minimum%2A> 和 <xref:System.Windows.Forms.TrackBar.Maximum%2A> 是跟踪条上可表示的最小值和最大值。  
  
 其他两个重要的属性是 <xref:System.Windows.Forms.TrackBar.SmallChange%2A> 和 <xref:System.Windows.Forms.TrackBar.LargeChange%2A>。  <xref:System.Windows.Forms.TrackBar.SmallChange%2A> \> 属性值是滚动块响应按下向左键或向右键时移动的位置数。  <xref:System.Windows.Forms.TrackBar.LargeChange%2A> 属性值是滚动块响应按下 Page Up 或 Page Down 键，或者响应鼠标在跟踪条上的滚动块任一边单击时所移动的位置数。  
  
## 请参阅  
 <xref:System.Windows.Forms.TrackBar>   
 [TrackBar 控件](../../../../docs/framework/winforms/controls/trackbar-control-windows-forms.md)