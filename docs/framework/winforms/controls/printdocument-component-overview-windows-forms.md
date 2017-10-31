---
title: "PrintDocument 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "PrintDocument"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "PrintDocument 组件 [Windows 窗体], 关于 PrintDocument 组件"
  - "打印 [Windows 窗体], PrintDocument 组件"
ms.assetid: b59b4b60-dce5-42ca-8421-3a54a2f7bab0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# PrintDocument 组件概述（Windows 窗体）
Windows 窗体 [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md) 组件用于设置一些属性，这些属性说明在基于 Windows 的应用程序中要打印什么内容以及打印文档的能力。  可将它与 [PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md) 组件一起使用来控制文档打印的各个方面。  
  
## 使用 PrintDocument 组件  
 涉及 <xref:System.Drawing.Printing.PrintDocument> 组件的两种主要情况是：  
  
-   简单的打印作业，如打印单个文本文件。  在这种情况下，应将 <xref:System.Drawing.Printing.PrintDocument> 组件添加到 Windows 窗体，然后在 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件处理程序中添加打印文件的编程逻辑。  该编程逻辑应以使用 <xref:System.Drawing.Printing.PrintDocument.Print%2A> 方法打印文档结束。  此方法向打印机发送一个 <xref:System.Drawing.Graphics> 对象，该对象包含在 <xref:System.Drawing.Printing.PrintPageEventArgs> 类的 <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> 属性中。  有关如何使用 <xref:System.Drawing.Printing.PrintDocument> 组件打印文本文档的示例，请参见[如何：打印 Windows 窗体中的多页文本文件](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)。  
  
-   更为复杂的打印作业，如想要重新使用已编写的打印逻辑的情况。  在这种情况下，应从 <xref:System.Drawing.Printing.PrintDocument> 组件派生一个新组件，并重写（请参见 Visual Basic 的[重写](../Topic/Overrides%20\(Visual%20Basic\).md)或 C\# 的[重写](../Topic/override%20\(C%23%20Reference\).md)）<xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件。  
  
 将 <xref:System.Drawing.Printing.PrintDocument> 组件添加到窗体后，它出现在 Windows 窗体设计器底部的栏中。  
  
## 请参阅  
 <xref:System.Drawing.Graphics>   
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [PrintDocument 组件](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)