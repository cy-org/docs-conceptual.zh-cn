---
title: "HScrollBar 控件和 VScrollBar 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "HScrollBar"
  - "VScrollBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "HScrollBar 控件 [Windows 窗体], 关于 HScrollBar"
  - "滚动条, 关于滚动条"
  - "ScrollBar 控件 [Windows 窗体]"
  - "ScrollBar 控件 [Windows 窗体], 关于 ScrollBar 控件"
  - "VScrollBar 控件 [Windows 窗体], 关于 VScrollBar 控件"
ms.assetid: 8b307679-1cae-41d8-99aa-3d1efd207cd6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# HScrollBar 控件和 VScrollBar 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ScrollBar> 控件用于在应用程序或控件中水平或垂直滚动，以方便地在较长的项列表或大量信息中转移。  因为滚动条是 Windows 界面的一种常见元素，所以 <xref:System.Windows.Forms.ScrollBar> 控件通常与 <xref:System.Windows.Forms.ScrollableControl> 类的派生控件之外的控件一起使用。  同样，许多开发人员在创作自己的用户控件时会选择合并 <xref:System.Windows.Forms.ScrollBar> 控件。  
  
 <xref:System.Windows.Forms.HScrollBar>（水平）和 <xref:System.Windows.Forms.VScrollBar>（垂直）控件独立于其他控件操作，它们有自己的一组事件、属性和方法。  <xref:System.Windows.Forms.ScrollBar> 控件与附加到文本框、列表框、组合框或 MDI 窗体的内置滚动条不同（<xref:System.Windows.Forms.TextBox> 控件具有 <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 属性，用于显示或隐藏附加到该控件的滚动条）。  
  
 <xref:System.Windows.Forms.ScrollBar> 控件使用 <xref:System.Windows.Forms.ScrollBar.Scroll> 事件来监视滚动框（有时称之为滚动块）沿着滚动条的移动情况。  使用 <xref:System.Windows.Forms.ScrollBar.Scroll> 事件，可以在拖动滚动条时访问滚动条值。  
  
## Value 属性  
 <xref:System.Windows.Forms.ScrollBar.Value%2A> 属性（默认情况下为 0）是与滚动框在滚动条中的位置相对应的一个 `integer` 值。  当滚动框的位置值为最小值时，滚动框移到最左端位置（对于水平滚动条），或移到顶端位置（对于垂直滚动条）。  当滚动框的位置值为最大值时，滚动框移到最右端位置或底端位置。  同理，在值范围的底端和顶端中间的值会使滚动框的前端位于滚动条的中间。  
  
 除了可以通过鼠标单击来更改滚动条值以外，用户还可以沿着滚动条将滚动框拖动到任何点。  结果值取决于滚动框的位置，但是该值总是在用户设置的 <xref:System.Windows.Forms.ScrollBar.Minimum%2A> 属性和 <xref:System.Windows.Forms.ScrollBar.Maximum%2A> 属性的范围之内。  
  
## LargeChange 和 SmallChange 属性  
 当用户按下 Page Up 键或 Page Down 键或者在滚动框的任何一边单击滚动条轨迹时，<xref:System.Windows.Forms.ScrollBar.Value%2A> 属性将按照 <xref:System.Windows.Forms.ScrollBar.LargeChange%2A> 属性中设置的值而更改。  
  
 当用户按下某个箭头键或单击某个滚动条按钮时，<xref:System.Windows.Forms.ScrollBar.Value%2A> 属性将按照 <xref:System.Windows.Forms.ScrollBar.SmallChange%2A> 属性中设置的值而更改。  
  
## 请参阅  
 <xref:System.Windows.Forms.HScrollBar>   
 <xref:System.Windows.Forms.VScrollBar>   
 [Additions to Windows Forms for the .NET Framework 2.0](http://msdn.microsoft.com/zh-cn/c61a923d-3d6a-4c8c-820c-e94c83f3f9a8)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)