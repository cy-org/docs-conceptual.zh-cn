---
title: "PrintPreviewControl 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "PrintPreviewControl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "打印预览"
  - "PrintPreviewControl 控件"
ms.assetid: 4513c6c7-5e9b-4f4c-82ca-00f993a26955
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# PrintPreviewControl 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.PrintPreviewControl> 用于按文档打印时的外观显示 [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)。  该控件没有按钮或其他用户界面元素，因此您通常只有在希望编写自己的打印预览用户界面时才使用 <xref:System.Windows.Forms.PrintPreviewControl>。  如果需要标准的用户界面，请使用 <xref:System.Windows.Forms.PrintPreviewDialog> 控件；有关概述，请参见 [PrintPreviewDialog 控件概述](../../../../docs/framework/winforms/controls/printpreviewdialog-control-overview-windows-forms.md)。  
  
## 主要属性  
 该控件的主要属性是 <xref:System.Windows.Forms.PrintPreviewControl.Document%2A>，用于设置要预览的文档。  文档必须是 <xref:System.Drawing.Printing.PrintDocument> 对象。  有关创建用于打印的文档的概述，请参见 [PrintDocument 组件概述](../../../../docs/framework/winforms/controls/printdocument-component-overview-windows-forms.md) 和 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)。  <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> 和 <xref:System.Windows.Forms.PrintPreviewControl.Rows%2A> 属性确定在控件上水平和垂直显示的页的数目。  抗锯齿可使文字显得更齐整平滑，但也会使显示更慢；若要使用它，请将 <xref:System.Windows.Forms.PrintPreviewControl.UseAntiAlias%2A> 属性设置为 `true`。  
  
## 请参阅  
 <xref:System.Windows.Forms.PrintPreviewControl>   
 [PrintPreviewDialog 控件概述](../../../../docs/framework/winforms/controls/printpreviewdialog-control-overview-windows-forms.md)   
 [PrintPreviewControl 控件](../../../../docs/framework/winforms/controls/printpreviewcontrol-control-windows-forms.md)   
 [对话框控件和组件](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)