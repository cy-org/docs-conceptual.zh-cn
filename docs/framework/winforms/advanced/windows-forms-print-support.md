---
title: "Windows 窗体打印支持 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "窗体, 打印（使用设计器）"
  - "打印 [Windows 窗体]"
  - "打印 [Windows 窗体], 打印支持"
  - "打印, Windows 窗体, 支持"
  - "Windows 窗体, 打印"
ms.assetid: a4a2960c-eb70-48e2-b641-cfb222704e46
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体打印支持
在 Windows 窗体中进行打印主要包括以下两个方面：使用 [PrintDocument 组件](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)组件来使用户可以打印；使用 [PrintPreviewDialog 控件](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)控件、[PrintDialog 组件](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)组件和 [PageSetupDialog 组件](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)组件向了解 Windows 操作系统的用户提供熟悉的图形界面。  
  
 通常，您可以创建 <xref:System.Drawing.Printing.PrintDocument> 组件的一个新实例，使用 <xref:System.Drawing.Printing.PrinterSettings> 和 <xref:System.Drawing.Printing.PageSettings> 类设置描述打印内容的属性，然后调用 <xref:System.Drawing.Printing.PrintDocument.Print%2A> 方法实际打印文档。  
  
 在从基于 Windows 的应用程序进行打印的过程中，<xref:System.Drawing.Printing.PrintDocument> 组件将显示中止打印对话框，该对话框提醒用户正在进行打印，并且可让用户取消打印作业。  
  
## 本节内容  
 [如何：创建标准的 Windows 窗体打印作业](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)  
 解释如何使用 <xref:System.Drawing.Printing.PrintDocument> 组件从 Windows 窗体进行打印。  
  
 [如何：在运行时从 PrintDialog 中捕获用户输入](../../../../docs/framework/winforms/advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)  
 解释如何使用 <xref:System.Windows.Forms.PrintDialog> 组件以编程方式修改选定的打印选项。  
  
 [如何：在 Windows 窗体中选择连接到用户计算机的打印机](../../../../docs/framework/winforms/advanced/how-to-choose-the-printers-attached-to-user-computer-in-windows-forms.md)  
 描述如何在运行时使用 <xref:System.Windows.Forms.PrintDialog> 组件更改要用来打印的打印机。  
  
 [如何：在 Windows 窗体中打印图形](../../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)  
 描述如何向打印机发送图形。  
  
 [如何：打印 Windows 窗体中的多页文本文件](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)  
 描述如何向打印机发送文本。  
  
 [如何：完成 Windows 窗体打印作业](../../../../docs/framework/winforms/advanced/how-to-complete-windows-forms-print-jobs.md)  
 解释如何在完成打印作业时提醒用户。  
  
 [如何：打印 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-print-a-windows-form.md)  
 演示如何打印当前窗体的副本。  
  
 [如何：使用打印预览在 Windows 窗体中进行打印](../../../../docs/framework/winforms/advanced/how-to-print-in-windows-forms-using-print-preview.md)  
 演示如何使用 <xref:System.Windows.Forms.PrintPreviewDialog> 打印文档。  
  
## 相关章节  
 [PrintDocument 组件](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)  
 解释 <xref:System.Drawing.Printing.PrintDocument> 组件的用法。  
  
 [PrintDialog 组件](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)  
 解释 <xref:System.Windows.Forms.PrintDialog> 组件的用法。  
  
 [PrintPreviewDialog 控件](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)  
 解释 <xref:System.Windows.Forms.PrintPreviewDialog> 控件的用法。  
  
 [PageSetupDialog 组件](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)  
 解释 <xref:System.Windows.Forms.PageSetupDialog> 组件的用法。  
  
 <xref:System.Drawing.Printing>  
 描述 <xref:System.Drawing.Printing> 命名空间中的类。