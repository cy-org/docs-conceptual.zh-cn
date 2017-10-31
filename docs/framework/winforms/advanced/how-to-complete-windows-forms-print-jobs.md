---
title: "如何：完成 Windows 窗体打印作业 | Microsoft Docs"
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
  - "打印作业, 在 Windows 窗体中完成"
  - "打印 [Windows 窗体], 打印作业"
ms.assetid: 23ec74f7-34c5-4710-82a0-ee2914518548
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 如何：完成 Windows 窗体打印作业
通常，涉及打印的字处理器和其他应用程序都提供为用户显示打印作业完成消息的选项。  通过处理 <xref:System.Drawing.Printing.PrintDocument> 组件的 <xref:System.Drawing.Printing.PrintDocument.EndPrint> 事件，可以在 Windows 窗体中提供此项功能。  
  
 下面的过程要求创建有 <xref:System.Drawing.Printing.PrintDocument> 组件且基于 Windows 的应用程序，这是从基于 Windows 的应用程序启用打印的标准方法。  有关使用 <xref:System.Drawing.Printing.PrintDocument> 组件从 Windows 窗体进行打印的更多信息，请参见 [如何：创建标准的 Windows 窗体打印作业](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)。  
  
### 完成打印作业  
  
1.  设置 <xref:System.Drawing.Printing.PrintDocument> 组件的 <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> 属性。  
  
    ```vb  
    PrintDocument1.DocumentName = "MyTextFile"  
  
    ```  
  
    ```csharp  
    printDocument1.DocumentName = "MyTextFile";  
  
    ```  
  
    ```cpp  
    printDocument1->DocumentName = "MyTextFile";  
    ```  
  
2.  编写代码以处理 <xref:System.Drawing.Printing.PrintDocument.EndPrint> 事件。  
  
     在下面的代码示例中，将显示一个消息框，指示文档已打印完毕。  
  
    ```vb  
    Private Sub PrintDocument1_EndPrint(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintEventArgs) Handles PrintDocument1.EndPrint  
       MessageBox.Show(PrintDocument1.DocumentName + " has finished printing.")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void printDocument1_EndPrint(object sender,   
    System.Drawing.Printing.PrintEventArgs e)  
    {  
       MessageBox.Show(printDocument1.DocumentName +   
          " has finished printing.");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_EndPrint(System::Object ^ sender,  
          System::Drawing::Printing::PrintEventArgs ^ e)  
       {  
          MessageBox::Show(String::Concat(printDocument1->DocumentName,  
             " has finished printing."));  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.printDocument1.EndPrint += new  
       System.Drawing.Printing.PrintEventHandler  
       (this.printDocument1_EndPrint);  
  
    ```  
  
    ```cpp  
    this->printDocument1->EndPrint += gcnew  
       System::Drawing::Printing::PrintEventHandler  
       (this, &Form1::printDocument1_EndPrint);  
    ```  
  
## 请参阅  
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows 窗体打印支持](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)