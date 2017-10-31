---
title: "如何：使用 Windows 窗体 ErrorProvider 组件显示窗体验证的错误图标 | Microsoft Docs"
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
  - "错误图标"
  - "错误信息, 显示图标"
  - "ErrorProvider 组件 [Windows 窗体], 显示错误图标"
  - "错误 [Windows 窗体], 向用户显示"
ms.assetid: 3b681a32-9db4-497b-a34b-34980eabee46
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 Windows 窗体 ErrorProvider 组件显示窗体验证的错误图标
通过使用 Windows 窗体 <xref:System.Windows.Forms.ErrorProvider> 组件，可以在用户输入无效数据时显示错误图标。  该窗体上必须至少有两个控件，以便在它们之间切换并由此调用验证代码。  
  
### 当控件的值无效时显示错误图标  
  
1.  向 Windows 窗体添加两个控件，例如，文本框。  
  
2.  向该窗体添加一个 <xref:System.Windows.Forms.ErrorProvider> 组件。  
  
3.  选择第一个控件，并将代码添加到它的 <xref:System.Windows.Forms.Control.Validating> 事件处理程序。  为使此代码正确运行，必须将过程连接到该事件。  有关更多信息，请参见 [如何：在运行时为 Windows 窗体创建事件处理程序](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md)。  
  
     下面的代码测试用户输入的数据的有效性；如果该数据无效，将调用 <xref:System.Windows.Forms.ErrorProvider.SetError%2A> 方法。  <xref:System.Windows.Forms.ErrorProvider.SetError%2A> 方法的第一个参数指定在哪个控件的旁边显示图标。  第二个参数为要显示的错误文本。  
  
    ```vb  
    Private Sub TextBox1_Validating(ByVal Sender As Object, _  
       ByVal e As System.ComponentModel.CancelEventArgs) Handles _  
       TextBox1.Validating  
          If Not IsNumeric(TextBox1.Text) Then  
             ErrorProvider1.SetError(TextBox1, "Not a numeric value.")  
          Else  
             ' Clear the error.  
             ErrorProvider1.SetError(TextBox1, "")  
          End If  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void textBox1_Validating (object sender,  
       System.ComponentModel.CancelEventArgs e)  
    {  
       try  
       {  
          int x = Int32.Parse(textBox1.Text);  
          errorProvider1.SetError(textBox1, "");  
       }  
       catch (Exception ex)  
       {  
          errorProvider1.SetError(textBox1, "Not an integer value.");  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void textBox1_Validating(System::Object ^  sender,  
          System::ComponentModel::CancelEventArgs ^  e)  
       {  
          try  
          {  
             int x = Int32::Parse(textBox1->Text);  
             errorProvider1->SetError(textBox1, "");  
          }  
          catch (System::Exception ^ ex)  
          {  
             errorProvider1->SetError(textBox1, "Not an integer value.");  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.textBox1.Validating += new  
    System.ComponentModel.CancelEventHandler(this.textBox1_Validating);  
  
    ```  
  
    ```cpp  
    this->textBox1->Validating += gcnew  
       System::ComponentModel::CancelEventHandler  
       (this, &Form1::textBox1_Validating);  
    ```  
  
4.  运行该项目。  向第一个控件中键入无效（在此例中为非数值的）数据，然后切换到第二个控件。  当显示错误图标时，用鼠标指针指向它以查看错误文本。  
  
## 请参阅  
 <xref:System.Windows.Forms.ErrorProvider.SetError%2A>   
 [ErrorProvider 组件概述](../../../../docs/framework/winforms/controls/errorprovider-component-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ErrorProvider 组件查看数据集中的错误](../../../../docs/framework/winforms/controls/view-errors-within-a-dataset-with-wf-errorprovider-component.md)