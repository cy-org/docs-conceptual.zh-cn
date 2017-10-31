---
title: "RichTextBox 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "RichTextBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "RichTextBox 控件 [Windows 窗体], 关于 RichTextBox 控件"
  - "文本框, 关于文本框"
ms.assetid: 95081194-3dd4-4b84-9545-dd373e491eca
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# RichTextBox 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件用于显示、输入和操作带有格式的文本。  <xref:System.Windows.Forms.RichTextBox> 控件除了做 <xref:System.Windows.Forms.TextBox> 控件所做的每件事外，还可以显示字体、颜色和链接，从文件加载文本和加载嵌入的图像，以及查找指定的字符。  与字处理应用程序（如 Microsoft Word）类似，<xref:System.Windows.Forms.RichTextBox> 通常用于提供文本操作和显示功能。  <xref:System.Windows.Forms.RichTextBox> 控件可以显示滚动条，这一点与 <xref:System.Windows.Forms.TextBox> 控件相同；但是与 <xref:System.Windows.Forms.TextBox> 控件不同的是，它的默认设置是水平和垂直滚动条均根据需要显示，并且拥有更多的滚动条设置。  
  
## 使用 RichTextBox 控件  
 与 <xref:System.Windows.Forms.TextBox> 控件一样，显示的文本由 <xref:System.Windows.Forms.RichTextBox.Text%2A> 属性设置。  <xref:System.Windows.Forms.RichTextBox> 控件有许多用于设置文本格式的属性。  有关这些属性的详细信息，请参见 [如何：为 Windows 窗体 RichTextBox 控件设置字体特性](../../../../docs/framework/winforms/controls/how-to-set-font-attributes-for-the-windows-forms-richtextbox-control.md) 和 [如何：在 Windows 窗体 RichTextBox 控件中设置缩进、悬挂缩进和带项目符号的段落](../../../../docs/framework/winforms/controls/set-indents-hanging-indents-bulleted-paragraphs-with-wf-richtextbox.md)。  为操作文件，<xref:System.Windows.Forms.RichTextBox.LoadFile%2A> 和 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 方法可以显示和编写包括纯文本、Unicode 纯文本和 RTF 格式 \(RTF\) 在内的多种文件格式。  可能的文件格式在 [RichTextBoxStreamType 枚举](frlrfSystemWindowsFormsRichTextBoxStreamTypeClassTopic)中列出。  可以使用 <xref:System.Windows.Forms.RichTextBox.Find%2A> 方法查找文本字符串或特定字符。  
  
 也可以将 <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> 属性设置为 `true`，并编写处理 <xref:System.Windows.Forms.RichTextBox.LinkClicked> 事件的代码，从而在 Web 样式的链接中使用 <xref:System.Windows.Forms.RichTextBox> 控件。  有关更多信息，请参见 [如何：使用 Windows 窗体 RichTextBox 控件显示 Web 样式的链接](../../../../docs/framework/winforms/controls/how-to-display-web-style-links-with-the-windows-forms-richtextbox-control.md)。  将 <xref:System.Windows.Forms.RichTextBox.SelectionProtected%2A> 属性设置为 `true` 可以防止用户操作控件中的部分或全部文本。  
  
 在 <xref:System.Windows.Forms.RichTextBox> 控件中可以通过调用 <xref:System.Windows.Forms.TextBoxBase.Undo%2A> 和 <xref:System.Windows.Forms.RichTextBox.Redo%2A> 方法撤消和重复大多数编辑操作。  <xref:System.Windows.Forms.RichTextBox.CanRedo%2A> 方法使您可以确定用户最后一次撤消的操作是否可以重新应用于控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)