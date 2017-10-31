---
title: "TextBox 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "TextBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "文本框, 添加"
  - "TextBox 控件 [Windows 窗体], 关于 TextBox 控件"
ms.assetid: d1a9c7f5-fa53-480a-a75c-158f8649ea2f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# TextBox 控件概述（Windows 窗体）
Windows 窗体文本框用于获取用户输入或显示文本。  <xref:System.Windows.Forms.TextBox> 控件通常用于可编辑文本，不过也可使其成为只读控件。  文本框可以显示多个行，对文本换行使其符合控件的大小以及添加基本的格式设置。  <xref:System.Windows.Forms.TextBox> 控件为在该控件中显示的或输入的文本提供一种格式化样式。  若要显示多种类型的带格式文本，请使用 <xref:System.Windows.Forms.RichTextBox> 控件。  有关更多信息，请参见 [RichTextBox 控件概述](../../../../docs/framework/winforms/controls/richtextbox-control-overview-windows-forms.md)。  
  
## 使用 TextBox 控件  
 控件显示的文本包含在 <xref:System.Windows.Forms.TextBox.Text%2A> 属性中。  默认情况下，最多可在一个文本框中输入 2048 个字符。  如果将 <xref:System.Windows.Forms.TextBox.Multiline%2A> 属性设置为 `true`，则最多可输入 32 KB 的文本。  <xref:System.Windows.Forms.TextBox.Text%2A> 属性可以在设计时使用“属性”窗口设置，在运行时用代码设置，或者在运行时通过用户输入来设置。  可以在运行时通过读取 <xref:System.Windows.Forms.TextBox.Text%2A> 属性来检索文本框的当前内容。  
  
 下面的代码示例在运行时设置控件中的文本。  `InitializeMyControl`程序不会自动执行;必须调用它。  
  
```vb  
Private Sub InitializeMyControl()  
   ' Put some text into the control first.  
   TextBox1.Text = "This is a TextBox control."  
End Sub  
  
```  
  
```csharp  
private void InitializeMyControl() {  
   // Put some text into the control first.  
   textBox1.Text = "This is a TextBox control.";  
}  
  
```  
  
```cpp  
private:  
   void InitializeMyControl()  
   {  
      // Put some text into the control first.  
      textBox1->Text = "This is a TextBox control.";  
   }  
```  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)