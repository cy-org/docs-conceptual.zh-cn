---
title: "Panel 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "Panel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "将控件分组, Panel 控件"
  - "Panel 控件 [Windows 窗体], 关于 Panel 控件"
ms.assetid: b6b83636-2c39-4dad-89d6-f0fa41049a74
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Panel 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.Panel> 控件用于为其他控件提供可识别的分组。  通常，使用面板按功能细分窗体。  例如，可能有一个订单窗体，它指定邮寄选项（如使用哪一类通宵承运商）。  将所有选项分组在一个面板中可向用户提供逻辑可视提示。  在设计时所有控件都可以轻松移动 \-\- 当移动 <xref:System.Windows.Forms.Panel> 控件时，它包含的所有控件也将移动。  分组在一个面板中的控件可以通过面板的 <xref:System.Windows.Forms.Control.Controls%2A> 属性进行访问。  此属性返回一批 <xref:System.Windows.Forms.Control> 实例，因此，通常需要将该方式检索得到的控件强制转换为它的特定类型。  
  
## Panel 与 GroupBox  
 <xref:System.Windows.Forms.Panel> 控件类似于 <xref:System.Windows.Forms.GroupBox> 控件；但只有 <xref:System.Windows.Forms.Panel> 控件可以有滚动条，只有 <xref:System.Windows.Forms.GroupBox> 控件可显示标题。  
  
## 主要属性  
 若要显示滚动条，请将 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A> 属性设置为 `true`。  也可以通过设置 <xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.BackgroundImage%2A> 和 <xref:System.Windows.Forms.Panel.BorderStyle%2A> 属性自定义面板的外观。  有关 <xref:System.Windows.Forms.Control.BackColor%2A> 和 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性的更多信息，请参见 [如何：设置面板的背景](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel.md)。  <xref:System.Windows.Forms.Panel.BorderStyle%2A> 属性确定面板轮廓为无可视边框 \(<xref:System.Windows.Forms.BorderStyle>\)、简单线条 \(<xref:System.Windows.Forms.BorderStyle>\) 还是阴影线条 \(<xref:System.Windows.Forms.BorderStyle>\)。  
  
## 请参阅  
 <xref:System.Windows.Forms.Panel>   
 [GroupBox 控件](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md)   
 [如何：使用设计器用 Windows 窗体面板控件对控件进行分组](../../../../docs/framework/winforms/controls/group-controls-with-wf-panel-control-using-the-designer.md)   
 [如何：使用设计器设置 Windows 窗体面板的背景](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel-using-the-designer.md)