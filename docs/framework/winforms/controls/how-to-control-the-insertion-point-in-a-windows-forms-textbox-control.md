---
title: "如何：控制 Windows 窗体 TextBox 控件中的插入点 | Microsoft Docs"
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
  - "插入点, TextBox 控件"
  - "文本框, 控制插入点"
  - "TextBox 控件 [Windows 窗体], 插入点"
ms.assetid: 5bee7d34-5121-429e-ab1f-d8ff67bc74c1
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：控制 Windows 窗体 TextBox 控件中的插入点
当 Windows 窗体 <xref:System.Windows.Forms.TextBox> 控件最初获得焦点时，文本框内的默认插入点在任何现有文本的左侧。  用户可以使用键盘或鼠标来移动插入点。  如果文本框失去焦点而后又再次获得焦点，则插入点为用户上一次放置的位置。  
  
 在某些情况下，此行为可能给用户带来不便。  在字处理应用程序中，用户可能希望新字符显示在任何现有文本的后面。  在数据输入应用程序中，用户可能希望新字符替换任何现有项。  <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 和 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 属性使您可以根据自己的需要来修改此行为。  
  
### 控制 TextBox 控件中的插入点  
  
1.  将 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 属性设置为适当的值。  如果值为零，则插入点紧挨第一个字符的左边。  
  
2.  （可选）将 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 属性设置为要选择的文本的长度。  
  
     下面的代码始终将插入点的位置恢复到 0。  `TextBox1_Enter` 事件处理程序必须绑定到控件；有关更多信息，请参见 [在 Windows 窗体中创建事件处理程序](../../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)。  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       TextBox1.SelectionStart = 0  
       TextBox1.SelectionLength = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_Enter(Object sender, System.EventArgs e) {  
       textBox1.SelectionStart = 0;  
       textBox1.SelectionLength = 0;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = 0;  
       }  
    ```  
  
## 使插入点默认情况下可见  
 只有当 <xref:System.Windows.Forms.TextBox> 控件处于 Tab 键顺序中的第一个位置时，<xref:System.Windows.Forms.TextBox> 插入点才默认在新窗体中可见。  否则，只有当使用键盘或鼠标使 <xref:System.Windows.Forms.TextBox> 具有焦点时，才会显示插入点。  
  
#### 使文本框插入点在新窗体中默认可见  
  
-   将 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性设置为 `0`。  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)