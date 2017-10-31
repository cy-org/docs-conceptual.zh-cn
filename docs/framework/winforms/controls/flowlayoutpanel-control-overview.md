---
title: "FlowLayoutPanel 控件概述 | Microsoft Docs"
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
  - "FlowLayoutPanel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "FlowLayoutPanel 控件 [Windows 窗体], 关于 FlowLayoutPanel 控件"
  - "窗体, 动态布局"
  - "布局 [Windows 窗体], dynamic"
  - "Windows 窗体, 动态布局"
ms.assetid: 3883e024-f5a0-456d-9c27-b4dfa1cc9045
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# FlowLayoutPanel 控件概述
<xref:System.Windows.Forms.FlowLayoutPanel> 控件沿水平或纵排方向排列其内容。  可从一行到下一行，或从一列到下一列来进行控件内容换行。  或者，可以剪切其内容，而非进行换行。  
  
 可以通过设置 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性的值来指定排列方向。  <xref:System.Windows.Forms.FlowLayoutPanel> 控件在从右到左 \(RTL\) 布局中正确地反转其排列方向。  也可通过设置 <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A> 属性的值来指定是对 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的内容进行换行还是剪切。  
  
 将 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性设置为 `true` 时，<xref:System.Windows.Forms.FlowLayoutPanel> 控件自动调整根据其内容调整大小。  它还为其子控件提供了 **FlowBreak** 属性。  将 FlowBreak 属性的值设置为 `true` 导致 <xref:System.Windows.Forms.FlowLayoutPanel> 控件停止按当前排列方向对控件进行布局，并换行到下一行或下一列。  
  
 任何 Windows 窗体控件均可以是 <xref:System.Windows.Forms.FlowLayoutPanel> 控制的子控件，包括 <xref:System.Windows.Forms.FlowLayoutPanel> 的其他实例。  使用此功能，可以构造在运行时适应窗体尺寸的复杂布局。  
  
 另请参阅[演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](http://msdn.microsoft.com/library/z9w7ek2f\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [FlowLayoutPanel 控件](../../../../docs/framework/winforms/controls/flowlayoutpanel-control-windows-forms.md)