---
title: "如何：显示 PrintDialog 组件 | Microsoft Docs"
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
  - "打印对话框, 显示"
  - "PrintDialog 组件 [Windows 窗体], 显示"
  - "打印 [Windows 窗体], 显示打印对话框"
ms.assetid: 745a8db7-0526-4b21-b09d-18e13ed32014
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：显示 PrintDialog 组件
<xref:System.Windows.Forms.PrintDialog> 组件是许多用户都非常熟悉的标准 Windows 打印对话框。  由于用户会立即适应它，因此使用 <xref:System.Windows.Forms.PrintDialog> 组件对您来说是十分有益的。  
  
### 显示 PrintDialog 组件  
  
-   从应用程序的代码内调用 <xref:System.Windows.Forms.Form.ShowDialog%2A> 方法。  
  
     在显示该组件后，用户将与之进行交互，设置打印作业的属性。  这些项保存在与该打印作业关联的 [PrinterSettings](frlrfSystemDrawingPrintingPrinterSettingsMembersTopic) 类和 [PageSettings](frlrfSystemDrawingPrintingPageSettingsMembersTopic) 类（如果用户通过 <xref:System.Windows.Forms.PrintDialog> 组件访问 [PageSetupDialog 组件](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)）中。  然后可以调用它们所设置的属性以确定打印作业的细节。  
  
## 请参阅  
 [如何：创建标准的 Windows 窗体打印作业](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)   
 [如何：在运行时从 PrintDialog 中捕获用户输入](../../../../docs/framework/winforms/advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)   
 [PrintPreviewDialog 控件](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [PrintDialog 组件](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)