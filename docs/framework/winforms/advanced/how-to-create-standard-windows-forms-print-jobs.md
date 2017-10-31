---
title: "如何：创建标准的 Windows 窗体打印作业 | Microsoft Docs"
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
  - "打印 [Visual Basic], 在 Windows 应用程序中"
  - "打印 [Windows 窗体]"
  - "打印 [Windows 窗体], 创建打印作业"
ms.assetid: 03342b90-9cfe-40b2-838b-b479a13c5dea
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：创建标准的 Windows 窗体打印作业
在 Windows 窗体中进行打印的基础是 <xref:System.Drawing.Printing.PrintDocument> 组件，更具体地说，是 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件。  通过编写代码来处理 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件，可以指定打印内容和打印方式。  
  
### 创建打印作业  
  
1.  向窗体添加 <xref:System.Drawing.Printing.PrintDocument> 组件。  
  
2.  编写代码以处理 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件。  
  
     您将必须编写您自己的打印逻辑代码。  另外，将必须指定要打印的材料。  
  
     在下面的代码示例中，在 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件处理程序中创建一个红色矩形的示例图形作为要打印的材料。  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))  
    End Sub  
  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,   
         new Rectangle(500, 500, 500, 500));  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
  
    ```  
  
    ```cpp  
    printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
     可能还要为 <xref:System.Drawing.Printing.PrintDocument.BeginPrint> 和 <xref:System.Drawing.Printing.PrintDocument.EndPrint> 事件编写代码，也许还包括一个表示要打印的总页数的整数，该整数随着每一页的打印而递减。  
  
    > [!NOTE]
    >  可以向窗体添加一个 <xref:System.Windows.Forms.PrintDialog> 组件，以便为用户提供整洁高效的用户界面 \(UI\)。  通过设置 <xref:System.Windows.Forms.PrintDialog> 组件的 <xref:System.Windows.Forms.PrintDialog.Document%2A> 属性，可以设置与正在窗体上处理的打印文档相关的属性。  有关 <xref:System.Windows.Forms.PrintDialog> 组件的更多信息，请参见 [PrintDialog 组件](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)。  
  
     有关 Windows 窗体打印作业的具体细节的更多信息，包括如何以编程方式创建打印作业，请参见 <xref:System.Drawing.Printing.PrintPageEventArgs>。  
  
## 请参阅  
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)