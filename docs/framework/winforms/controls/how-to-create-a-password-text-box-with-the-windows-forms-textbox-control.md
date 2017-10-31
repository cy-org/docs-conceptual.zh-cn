---
title: "如何：使用 Windows 窗体 TextBox 控件创建密码文本框 | Microsoft Docs"
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
  - "密码框, 创建"
  - "文本框中的 PasswordChar 属性"
  - "密码, 输入屏蔽"
  - "密码, 密码文本框"
  - "TextBox 控件 [Windows 窗体], 输入密码"
ms.assetid: d105d6b9-3d50-44cd-80d8-2c0e2f486727
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 TextBox 控件创建密码文本框
密码框是一种 Windows 窗体文本框，它在用户键入字符串时显示占位符。  
  
### 创建密码文本框  
  
1.  将 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 属性设置为某个特定字符。  
  
     <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 属性指定在文本框中显示的字符。  例如，如果希望在密码框中显示星号，请在“属性”窗口中将 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 属性指定为“\*”。  然后，无论用户在文本框中键入什么字符，都显示为星号。  
  
2.  设置 <xref:System.Windows.Forms.TextBoxBase.MaxLength%2A> 属性（可选）。  此属性确定可在文本框中键入多少字符。  如果超过了最大长度，系统会发出提示音，且文本框不再接受任何字符。  注意，您可能不想设置此属性，因为黑客可能会利用密码的最大长度来尝试猜测密码。  
  
     下面的代码示例演示了如何初始化一个文本框，此文本框可接受最长 14 个字符的字符串，并显示星号来替代该字符串。  `InitializeMyControl`程序不会自动执行;必须调用它。  
  
    > [!IMPORTANT]
    >  使用文本框上的 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 属性可帮助确保实现以下功能：用户输入密码时如有其他人在观看，他们将无法知道输入的密码。  此安全措施未涵盖可能会根据应用程序逻辑的需要而发生的任何种类的密码存储或传输。  因为输入的文本未以任何方式进行加密，所以您应该像处理任何其他机密数据一样处理它。  即使密码未显示为纯文本，它也仍被视为纯文本字符串（除非您已实施了其他安全措施）。  
  
    ```vb  
    Private Sub InitializeMyControl()  
       ' Set to no text.  
       TextBox1.Text = ""  
       ' The password character is an asterisk.  
       TextBox1.PasswordChar = "*"  
       ' The control will allow no more than 14 characters.  
       TextBox1.MaxLength = 14  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InitializeMyControl()  
    {  
       // Set to no text.  
       textBox1.Text = "";  
       // The password character is an asterisk.  
       textBox1.PasswordChar = '*';  
       // The control will allow no more than 14 characters.  
       textBox1.MaxLength = 14;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void InitializeMyControl()  
       {  
          // Set to no text.  
          textBox1->Text = "";  
          // The password character is an asterisk.  
          textBox1->PasswordChar = '*';  
          // The control will allow no more than 14 characters.  
          textBox1->MaxLength = 14;  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)