---
title: "如何：使用设计器设置 Windows 窗体控件显示的文本 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 设置标题"
  - "Windows 窗体, 设置显示的文本"
ms.assetid: 9d18e0e0-f17f-4074-837d-e67ceeeaa89d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用设计器设置 Windows 窗体控件显示的文本
Windows 窗体控件通常显示与该控件的主要功能相关的某些文本。  例如，<xref:System.Windows.Forms.Button> 控件通常显示指示当单击该按钮时将会执行的操作的标题。  对于所有控件，都可以通过使用 <xref:System.Windows.Forms.Control.Text%2A> 属性设置或返回文本。  通过使用 <xref:System.Windows.Forms.Control.Font%2A> 属性可以更改字体。  
  
### 通过设计器设置文本和字体  
  
1.  在“属性”窗口中，将控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为一个适当的字符串。  
  
     若要创建带下划线的快捷键，请在将要成为快捷键的字母前加一个“and”符 \(&\)。  
  
2.  在“属性”窗口中，单击 <xref:System.Windows.Forms.Control.Font%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
     在标准字体对话框中，选择所需的字体、字体样式、大小、效果（如带删除线或下划线）和脚本。  
  
## 请参阅  
 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)