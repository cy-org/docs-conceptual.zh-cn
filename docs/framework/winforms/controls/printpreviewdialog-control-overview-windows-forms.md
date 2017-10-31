---
title: "PrintPreviewDialog 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "PrintPreviewDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "PrintPreviewDialog 控件（使用设计器）, 关于 PrintPreviewDialog"
ms.assetid: efd4ee8d-6edd-47ec-88e4-4a4759bd2384
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# PrintPreviewDialog 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.PrintPreviewDialog> 控件是预先配置的对话框，用于显示 [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md) 在打印时的外观。  可在基于 Windows 的应用程序中使用它作为简单的解决方案，而不用配置自己的对话框。  该控件包含打印、放大、显示一页或多页和关闭此对话框的按钮。  
  
## 主要属性和方法  
 该控件的主要属性是 <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A>，用于设置要预览的文档。  文档必须是 <xref:System.Drawing.Printing.PrintDocument> 对象。  若要显示对话框，必须调用它的 <xref:System.Windows.Forms.Form.ShowDialog%2A> 方法。  抗锯齿可使文字显得更齐整平滑，但也会使显示更慢；若要使用它，请将 <xref:System.Windows.Forms.PrintPreviewDialog.UseAntiAlias%2A> 属性设置为 `true`。  
  
 有些属性可通过 <xref:System.Windows.Forms.PrintPreviewDialog> 包含的 <xref:System.Windows.Forms.PrintPreviewControl> 获得。  （不必向窗体添加此 <xref:System.Windows.Forms.PrintPreviewControl>，向窗体添加 <xref:System.Windows.Forms.PrintPreviewDialog> 对话框时它自动包含在此对话框中。）可通过 <xref:System.Windows.Forms.PrintPreviewControl> 使用的属性示例是 <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> 和 <xref:System.Windows.Forms.PrintPreviewControl.Rows%2A> 属性，它们确定在控件上水平和垂直显示的页的数目。  您可以像访问 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中的 `PrintPreviewDialog1.PrintPreviewControl.Columns`、[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中的 `printPreviewDialog1.PrintPreviewControl.Columns` 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)] 中的 `printPreviewDialog1->PrintPreviewControl->Columns` 一样，访问 <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> 属性。  
  
## 请参阅  
 <xref:System.Windows.Forms.PrintPreviewDialog>   
 [PrintPreviewControl 控件概述](../../../../docs/framework/winforms/controls/printpreviewcontrol-control-overview-windows-forms.md)   
 [PrintPreviewDialog 控件](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [对话框控件和组件](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)