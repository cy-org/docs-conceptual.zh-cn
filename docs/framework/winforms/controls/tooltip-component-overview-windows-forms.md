---
title: "ToolTip 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "ToolTip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ToolTip 组件 [Windows 窗体], 关于 ToolTip 组件"
  - "工具提示 [Windows 窗体], 关于工具提示"
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# ToolTip 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ToolTip> 组件在用户指向控件时显示相应的文本。  工具提示可与任何控件相关联。  举一个使用此组件的示例：为节省窗体上的空间，可以在按钮上显示一个小图标并用工具提示解释该按钮的功能。  
  
## 使用 ToolTip 组件  
 <xref:System.Windows.Forms.ToolTip> 组件为 Windows 窗体或其他容器上的多个控件提供 `ToolTip` 属性。  例如，如果将一个 <xref:System.Windows.Forms.ToolTip> 组件置于窗体上，则可以为一个 <xref:System.Windows.Forms.TextBox> 控件显示“Type your name here”（在此键入您的姓名），并为一个 <xref:System.Windows.Forms.Button> 控件显示“Click here to save changes”（单击此处保存更改）。  
  
 <xref:System.Windows.Forms.ToolTip> 组件的主要方法包括 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 和 <xref:System.Windows.Forms.ToolTip.GetToolTip%2A>。  可以使用 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 方法设置为控件显示的工具提示。  有关更多信息，请参见 [如何：在设计时为 Windows 窗体上的控件设置工具提示](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)。  主要属性有 <xref:System.Windows.Forms.ToolTip.Active%2A> 和 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>，前者必须设置为 `true` 才能显示工具提示，后者用于设置以下三项内容：显示工具提示字符串的时间，用户必须指在控件上多长时间才会显示工具提示，需要多久才会显示随后的工具提示窗口。  有关更多信息，请参见 [如何：更改 Windows 窗体 ToolTip 组件的延迟](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolTip>   
 [如何：在设计时为 Windows 窗体上的控件设置工具提示](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)   
 [如何：更改 Windows 窗体 ToolTip 组件的延迟](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)