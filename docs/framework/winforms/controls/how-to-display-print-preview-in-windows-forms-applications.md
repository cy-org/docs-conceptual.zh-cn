---
title: "如何：在 Windows 窗体应用程序中显示打印预览 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 打印预览"
  - "打印预览, 显示"
  - "打印 [Windows 窗体], 打印预览"
ms.assetid: e394134c-0886-4517-bd8d-edc4a3749eb5
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：在 Windows 窗体应用程序中显示打印预览
用户可以使用 <xref:System.Windows.Forms.PrintPreviewDialog> 控件显示文档，通常是在打印前显示文档。  
  
 为此，需要指定 <xref:System.Drawing.Printing.PrintDocument> 类的一个实例；该类是要打印的文档。  有关使用 <xref:System.Drawing.Printing.PrintDocument> 组件进行打印预览的更多信息，请参见[如何：使用打印预览在 Windows 窗体中进行打印](../../../../docs/framework/winforms/advanced/how-to-print-in-windows-forms-using-print-preview.md)。  
  
> [!NOTE]
>  要在运行时使用 <xref:System.Windows.Forms.PrintPreviewDialog> 控件，用户必须在计算机上安装打印机（本地安装或通过网络安装），因为这是 <xref:System.Windows.Forms.PrintPreviewDialog> 组件确定打印时文档显示方式的一种方法。  
  
 <xref:System.Windows.Forms.PrintPreviewDialog> 控件使用 <xref:System.Drawing.Printing.PrinterSettings> 类。  此外，与 <xref:System.Windows.Forms.PrintPreviewDialog> 组件一样，<xref:System.Windows.Forms.PrintPreviewDialog> 控件也使用 <xref:System.Drawing.Printing.PageSettings> 类。  在 <xref:System.Windows.Forms.PrintPreviewDialog> 控件的 <xref:System.Windows.Forms.PrintPreviewControl.Document%2A> 属性中指定的打印文档引用 <xref:System.Drawing.Printing.PrinterSettings> 和 <xref:System.Drawing.Printing.PageSettings> 类的实例，而这些实例用于在预览窗口中呈现文档。  
  
### 使用 PrintPreviewDialog 控件查看页  
  
-   可使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示对话框，指定要使用的 <xref:System.Drawing.Printing.PrintDocument>。  
  
     在下面的代码示例中，<xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序打开 <xref:System.Windows.Forms.PrintPreviewDialog> 控件的实例。  打印文档是在 <xref:System.Windows.Forms.PrintDialog.Document%2A> 属性中指定的。  在下面的示例中，未指定任何打印文档。  
  
     该示例要求窗体具有一个 <xref:System.Windows.Forms.Button> 控件、一个名为 `myDocument` 的 <xref:System.Drawing.Printing.PrintDocument> 组件以及一个 <xref:System.Windows.Forms.PrintPreviewDialog> 控件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       ' You will have to specify your own print document.  
       PrintPreviewDialog1.Document = myDocument  
       PrintPreviewDialog1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       printPreviewDialog1.Document = myDocument;  
       printPreviewDialog1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          printPreviewDialog1->Document = myDocument;  
          printPreviewDialog1->ShowDialog();  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## 请参阅  
 [PrintDocument 组件](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)   
 [PrintPreviewDialog 控件](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [Windows 窗体](../../../../docs/framework/winforms/index.md)