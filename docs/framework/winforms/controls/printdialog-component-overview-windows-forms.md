---
title: "PrintDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "PrintDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "打印对话框, 显示"
  - "PrintDialog 组件 [Windows 窗体], 关于 PrintDialog 组件"
ms.assetid: 8327b8ac-1017-4b5e-a88b-fea9dd56999c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# PrintDialog 组件概述（Windows 窗体）
Windows 窗体 [PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md) 控件是一个预先配置的对话框，可在基于 Windows 的应用程序中用于选择打印机、选择要打印的页以及确定其他与打印相关的设置。  将该控件用作选择打印机和打印相关设置的简单解决方案，而不用配置您自己的对话框。  可使用户能够打印文档的很多部分：全部打印、打印选定的页范围或打印选定内容。  利用标准的 Windows 对话框，您可以创建其基本功能可立即为用户所熟悉的应用程序。  <xref:System.Windows.Forms.PrintDialog> 组件从 <xref:System.Windows.Forms.CommonDialog> 类继承。  
  
## 使用该组件  
 可使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法在运行时显示对话框。  此组件具有与单个打印作业（<xref:System.Drawing.Printing.PrintDocument> 类）或个别打印机的设置（<xref:System.Drawing.Printing.PrinterSettings> 类）相关的属性。  这两类属性反过来可由多个打印机共享。  
  
 将 <xref:System.Windows.Forms.PrintDialog> 组件添加到窗体后，它出现在 Windows 窗体设计器底部的栏中。  
  
## 请参阅  
 <xref:System.Windows.Forms.PrintDialog>   
 [PrintDialog 组件](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)