---
title: "Label 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "Label"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "图像 [Windows 窗体], 在标签中显示"
  - "Label 控件 [Windows 窗体], 关于 Label 控件"
  - "标签"
ms.assetid: dcad7f44-11b7-4c55-b0c0-d984ade43d7d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Label 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.Label> 控件用于显示用户不能编辑的文本或图像。  它们用于标识窗体上的对象；例如，描述单击某控件时该控件所进行的操作或显示相应信息以响应应用程序中的运行时事件或进程。  例如，您可以使用标签向文本框、列表框和组合框等添加描述性标题。  也可以编写代码，使标签显示的文本为了响应运行时事件而作出更改。  例如，如果应用程序需要几分钟时间处理更改，则可以在标签中显示处理状态的消息。  
  
## 使用 Label 控件  
 因为 <xref:System.Windows.Forms.Label> 控件不能接收焦点，所以也可以用来为其他控件创建访问键。  访问键允许用户通过按 Alt 键和访问键来选择另一个控件。  有关更多信息，请参见[创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)和 [如何：使用 Windows 窗体 Label 控件创建访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)。  
  
 标签中显示的标题包含在 <xref:System.Windows.Forms.Label.Text%2A> 属性中。  <xref:System.Windows.Forms.Label.TextAlign%2A> 属性使您可以设置文本在标签内的对齐方式。  有关更多信息，请参见 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.Label>   
 [如何：调整 Windows 窗体标签控件大小以适应其内容](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)   
 [如何：使用 Windows 窗体 Label 控件创建访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)