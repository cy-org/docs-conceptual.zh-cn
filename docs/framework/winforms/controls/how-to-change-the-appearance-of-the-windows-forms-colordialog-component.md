---
title: "如何：更改 Windows 窗体 ColorDialog 组件的外观 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "颜色对话框, 配置外观"
  - "ColorDialog 组件, 示例"
  - "ColorDialog 组件, 设置外观格式"
ms.assetid: bba4e262-1cd7-4f63-89cf-330a36f7b539
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：更改 Windows 窗体 ColorDialog 组件的外观
可以使用 Windows 窗体 <xref:System.Windows.Forms.ColorDialog> 组件的若干属性来配置其外观。  对话框包括两部分：一部分显示基本颜色，另一部分允许用户定义自定义颜色。  
  
 多数属性限制用户可以从对话框中选择的颜色。  如果将 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> 属性设置为 `true`，则允许用户定义自定义颜色。  如果对话框进行了扩展以定义自定义颜色，则 <xref:System.Windows.Forms.ColorDialog.FullOpen%2A> 属性为 `true`；否则用户必须单击“定义自定义颜色”按钮。  将 <xref:System.Windows.Forms.ColorDialog.AnyColor%2A> 属性设置为 `true` 时，对话框会在基本颜色集内显示所有可用的颜色。  如果将 <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> 属性设置为 `true`，则用户不能选择仿色；只有纯色可供选择。  
  
 如果将 <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> 属性设置为 `true`，则会在对话框上显示“帮助”按钮。  当用户单击“帮助”按钮时，会引发 <xref:System.Windows.Forms.ColorDialog> 组件的 <xref:System.Windows.Forms.CommonDialog.HelpRequest> 事件。  
  
### 配置颜色对话框的外观  
  
1.  将 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>、<xref:System.Windows.Forms.ColorDialog.AnyColor%2A>、<xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> 和 <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> 属性设置为期望值。  
  
    ```vb  
    ColorDialog1.AllowFullOpen = True  
    ColorDialog1.AnyColor = True  
    ColorDialog1.SolidColorOnly = False  
    ColorDialog1.ShowHelp = True  
  
    ```  
  
    ```csharp  
    colorDialog1.AllowFullOpen = true;  
    colorDialog1.AnyColor = true;  
    colorDialog1.SolidColorOnly = false;  
    colorDialog1.ShowHelp = true;  
  
    ```  
  
    ```cpp  
    colorDialog1->AllowFullOpen = true;  
    colorDialog1->AnyColor = true;  
    colorDialog1->SolidColorOnly = false;  
    colorDialog1->ShowHelp = true;  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ColorDialog>   
 [ColorDialog 组件](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)   
 [ColorDialog 组件概述](../../../../docs/framework/winforms/controls/colordialog-component-overview-windows-forms.md)