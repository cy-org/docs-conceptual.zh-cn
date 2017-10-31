---
title: "RadioButton 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "RadioButton"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "单选按钮, 关于单选按钮"
  - "单选按钮, 确定状态"
  - "RadioButton 控件 [Windows 窗体], 关于 RadioButton 控件"
  - "RadioButton 控件 [Windows 窗体], 确定状态"
ms.assetid: cd11f0c2-d098-4022-adf9-1455bc166a13
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# RadioButton 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.RadioButton> 控件为用户提供由两个或多个互斥选项组成的选项集。  虽然单选按钮和复选框看似功能类似，却存在重要差异：当用户选择某单选按钮时，同一组中的其他单选按钮不能同时选定。  相反，却可以选择任意数目的复选框。  定义单选按钮组将告诉用户：“这里有一组选项，您可以从中选择一个且只能选择一个。  
  
## 使用控件  
 当单击 <xref:System.Windows.Forms.RadioButton> 控件时，其 <xref:System.Windows.Forms.RadioButton.Checked%2A> 属性设置为 `true`，并且调用 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  当 <xref:System.Windows.Forms.RadioButton.Checked%2A> 属性的值更改时，将引发 <xref:System.Windows.Forms.RadioButton.CheckedChanged> 事件。  如果 <xref:System.Windows.Forms.RadioButton.AutoCheck%2A> 属性设置为 `true`（默认值），则当选择单选按钮时，将自动清除该组中的所有其他单选按钮。  通常仅当使用验证代码确保选定的单选按钮是允许的选项时，才将该属性设置为 `false`。  控件内显示的文本使用 <xref:System.Windows.Forms.Control.Text%2A> 属性进行设置，该属性可以包含访问键快捷方式。  访问键允许用户通过按 Alt 键和访问键来“单击”控件。  有关更多信息，请参见[如何：创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)和 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)。  
  
 如果 <xref:System.Windows.Forms.RadioButton.Appearance%2A> 属性设置为 <xref:System.Windows.Forms.Appearance>，则 <xref:System.Windows.Forms.RadioButton> 控件的显示与命令按钮相似，选中时会显示为按下状态。  通过使用 <xref:System.Windows.Forms.ButtonBase.Image%2A> 和 <xref:System.Windows.Forms.ButtonBase.ImageList%2A> 属性，单选按钮还可以显示图像。  有关更多信息，请参见 [如何：设置 Windows 窗体控件所显示的图像](../../../../docs/framework/winforms/controls/how-to-set-the-image-displayed-by-a-windows-forms-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.RadioButton>   
 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [GroupBox 控件概述](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md)   
 [CheckBox 控件概述](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [如何：创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)   
 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [如何：按功能分组 Windows 窗体 RadioButton 控件](../../../../docs/framework/winforms/controls/how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)   
 [RadioButton 控件](../../../../docs/framework/winforms/controls/radiobutton-control-windows-forms.md)