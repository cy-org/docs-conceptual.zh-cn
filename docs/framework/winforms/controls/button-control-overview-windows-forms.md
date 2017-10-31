---
title: "Button 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "Button"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Button 控件 [Windows 窗体], 关于 Button 控件"
  - "按钮, 关于按钮"
ms.assetid: 255b291b-51a9-4a92-a1a4-2400cd82443f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Button 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.Button> 控件允许用户通过单击它来执行操作。  当该按钮被单击时，它看起来像是被按下，然后被释放。  每当用户单击按钮时，即调用 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  可将代码放入 <xref:System.Windows.Forms.Control.Click> 事件处理程序来执行所选择的任意操作。  
  
 按钮上显示的文本包含在 <xref:System.Windows.Forms.Control.Text%2A> 属性中。  如果文本超出按钮宽度，则换到下一行。  但是，如果控件无法容纳文本的总体高度，则将剪裁文本。  有关更多信息，请参见 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)。  <xref:System.Windows.Forms.Control.Text%2A> 属性可以包含访问键，允许用户通过同时按 Alt 键和访问键来“单击”控件。  有关详细信息，请参见[如何：创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)。  文本的外观受 <xref:System.Windows.Forms.Control.Font%2A> 属性和 <xref:System.Windows.Forms.ButtonBase.TextAlign%2A> 属性控制。  
  
 <xref:System.Windows.Forms.Button> 控件还可以使用 <xref:System.Windows.Forms.ButtonBase.Image%2A> 和 <xref:System.Windows.Forms.ButtonBase.ImageList%2A> 属性显示图像。  有关更多信息，请参见 [如何：设置 Windows 窗体控件所显示的图像](../../../../docs/framework/winforms/controls/how-to-set-the-image-displayed-by-a-windows-forms-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.Button>   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [如何：使用设计器将 Windows 窗体按钮指定为“接受”按钮](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-accept-button-using-the-designer.md)   
 [如何：使用设计器将 Windows 窗体按钮指定为“取消”按钮](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-cancel-button-using-the-designer.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)