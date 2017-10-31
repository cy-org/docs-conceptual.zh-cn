---
title: "PageSetupDialog 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "PageSetupDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "“页设置”对话框, 显示"
  - "PageSetupDialog 组件"
ms.assetid: 791caacb-a5ca-4fca-bad9-1a5721ad697c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# PageSetupDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.PageSetupDialog> 组件是一个预先配置的对话框，用于在基于 Windows 的应用程序中设置页详细信息以便打印。  在基于 Windows 的应用程序中将该组件用作用户设置页首选项的简单解决方案，而不用配置您自己的对话框。  可允许用户设置边框和边距调整量、页眉和页脚以及纵向或横向打印。  利用标准的 Windows 对话框，您可以创建其基本功能可立即为用户所熟悉的应用程序。  
  
## 主要属性和方法  
 可使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法在运行时显示对话框。  此组件具有与单页（<xref:System.Drawing.Printing.PrintDocument> 类）或任何文档（<xref:System.Drawing.Printing.PageSettings> 类）相关的可设置属性。  此外，<xref:System.Windows.Forms.PageSetupDialog> 组件可用于确定特定的打印机设置，这些设置存储在 <xref:System.Drawing.Printing.PrinterSettings> 类中。  
  
 将 <xref:System.Windows.Forms.PageSetupDialog> 组件添加到窗体后，它出现在 Windows 窗体设计器底部的栏中。  
  
## 请参阅  
 <xref:System.Windows.Forms.PageSetupDialog>   
 [PageSetupDialog 组件](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)