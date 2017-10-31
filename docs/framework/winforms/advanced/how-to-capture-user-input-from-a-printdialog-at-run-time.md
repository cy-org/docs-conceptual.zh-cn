---
title: "如何：在运行时从 PrintDialog 中捕获用户输入 | Microsoft Docs"
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
  - "打印选项"
  - "打印选项, 在运行时更改"
  - "打印 [Windows 窗体], 选项"
  - "运行时, 更改打印选项"
ms.assetid: 438501d8-9a70-4fb3-aae6-e46579aba0c6
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：在运行时从 PrintDialog 中捕获用户输入
虽然可以在设计时设置与打印有关的选项，但有时您也希望在运行时更改这些选项（多数情况下是由于用户的选择）。  可以使用 <xref:System.Windows.Forms.PrintDialog> 和 <xref:System.Drawing.Printing.PrintDocument> 组件捕获用于打印文档的用户输入。  
  
### 以编程方式更改打印选项  
  
1.  向窗体添加一个 <xref:System.Windows.Forms.PrintDialog> 和一个 <xref:System.Drawing.Printing.PrintDocument> 组件。  
  
2.  将 <xref:System.Windows.Forms.PrintDialog> 的 <xref:System.Windows.Forms.PrintDialog.Document%2A> 属性设置为添加到窗体的 <xref:System.Drawing.Printing.PrintDocument>。  
  
    ```vb  
    PrintDialog1.Document = PrintDocument1  
  
    ```  
  
    ```csharp  
    printDialog1.Document = PrintDocument1;  
  
    ```  
  
    ```cpp  
    printDialog1->Document = PrintDocument1;  
    ```  
  
3.  使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示 <xref:System.Windows.Forms.PrintDialog> 组件。  
  
    ```vb  
    PrintDialog1.ShowDialog()  
  
    ```  
  
    ```csharp  
    printDialog1.ShowDialog();  
  
    ```  
  
    ```cpp  
    printDialog1->ShowDialog();  
    ```  
  
4.  来自对话框的用户打印选项将被复制到 <xref:System.Drawing.Printing.PrintDocument> 组件的 <xref:System.Drawing.Printing.PrinterSettings> 属性。  
  
## 请参阅  
 [如何：打印 Windows 窗体中的多页文本文件](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)