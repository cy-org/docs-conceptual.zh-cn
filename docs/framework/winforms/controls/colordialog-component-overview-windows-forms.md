---
title: "ColorDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "ColorDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "颜色对话框, 关于颜色对话框"
  - "ColorDialog 组件, 关于 ColorDialog"
ms.assetid: 6dbdd8f0-f697-4728-bb09-7ea156f6d800
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# ColorDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ColorDialog> 组件是一个预先配置的对话框，它允许用户从调色板选择颜色以及将自定义颜色添加到该调色板。  此对话框与您在其他基于 Windows 的应用程序中看到的用于选择颜色的对话框相同。  可以在基于 Windows 的应用程序中使用它作为简单的解决方案，而不用配置自己的对话框。  
  
 此对话框中选择的颜色在 <xref:System.Windows.Forms.ColorDialog.Color%2A> 属性中返回。  如果 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> 属性设置为 `false`，则将禁用“定义自定义颜色”按钮，并且用户只能使用调色板中的预定义颜色。  如果 <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> 属性设置为 `true`，则用户无法选择抖色。  若要显示此对话框，必须调用它的 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法。  
  
## 请参阅  
 <xref:System.Windows.Forms.ColorDialog>   
 [ColorDialog 组件](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)   
 [对话框控件和组件](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)   
 [如何：更改 Windows 窗体 ColorDialog 组件的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-colordialog-component.md)