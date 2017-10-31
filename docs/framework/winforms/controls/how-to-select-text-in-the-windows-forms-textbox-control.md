---
title: "如何：在 Windows 窗体 TextBox 控件中选择文本 | Microsoft Docs"
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
  - "文本框, 以编程方式选择文本"
  - "文本, 以编程方式在文本框中选择内容"
  - "TextBox 控件 [Windows 窗体], 以编程方式选择文本"
ms.assetid: 8c591546-6a01-45c7-8e03-f78431f903b1
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 如何：在 Windows 窗体 TextBox 控件中选择文本
在 Windows 窗体 <xref:System.Windows.Forms.TextBox> 控件中，可以通过编程方式选择文本。  例如，如果创建一个可在文本中搜索特定字符串的函数，就可以选择那些文本，将找到的字符串的位置醒目地通报给读者。  
  
### 以编程方式选择文本  
  
1.  将 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 属性设置为要选择的文本的开始位置。  
  
     <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 属性是一个数字，它指示在文本字符串内的插入点，值为 0 表示最左边的位置。  如果将 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 属性设置为等于或大于文本框内的字符数，则插入点放在最后一个字符之后。  
  
2.  将 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 属性设置为要选择的文本的长度。  
  
     <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 属性是一个设置插入点宽度的数值。  如果将 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 设置为大于 0 的数，则会从当前插入点处开始选择该数目的字符。  
  
3.  （可选）通过 <xref:System.Windows.Forms.TextBoxBase.SelectedText%2A> 属性访问选定的文本。  
  
     下面的代码将在控件的 <xref:System.Windows.Forms.Control.Enter> 事件发生时选择文本框的内容。  此示例检查文本框是否具有 <xref:System.Windows.Forms.TextBox.Text%2A> 属性值（该值不是 `null` 或空的字符串）。  当文本框接收焦点时，将会选择文本框中的当前文本。  `TextBox1_Enter` 事件处理程序必须绑定到控件；有关更多信息，请参见[如何：在运行时为 Windows 窗体创建事件处理程序](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md)。  
  
     要测试此示例，请按 Tab 键直到文本框具有焦点。  在文本框中单击时，将取消选中文本。  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       If (Not String.IsNullOrEmpty(TextBox1.Text)) Then  
          TextBox1.SelectionStart = 0  
          TextBox1.SelectionLength = TextBox1.Text.Length  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_Enter(object sender, System.EventArgs e){  
       if (!String.IsNullOrEmpty(textBox1.Text))  
       {  
          textBox1.SelectionStart = 0;  
          textBox1.SelectionLength = textBox1.Text.Length;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^ sender,  
          System::EventArgs ^ e) {  
       if (!System::String::IsNullOrEmpty(textBox1->Text))  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = textBox1->Text->Length;  
       }  
    }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)