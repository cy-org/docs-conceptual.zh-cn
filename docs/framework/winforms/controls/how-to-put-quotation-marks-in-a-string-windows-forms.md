---
title: "如何：在字符串中放置引号（Windows 窗体） | Microsoft Docs"
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
  - "引号"
  - "引号, 添加到文本框中的字符串"
  - "TextBox 控件 [Windows 窗体], 显示引号"
ms.assetid: 68bdc3f3-4177-4eab-99cd-cac17a82b515
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：在字符串中放置引号（Windows 窗体）
有时可能需要将引号 \(" "\) 放入文本字符串中。  例如：  
  
 她说：“该好好款待你了！”  
  
 或者，也可以使用 <xref:Microsoft.VisualBasic.ControlChars.Quote> 字段作为常数。  
  
### 在代码中将引号放置于字符串中  
  
1.  在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中，将两个引号插入一行中作为一个嵌入的引号。  在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)] 中，插入转义序列 \\" 作为嵌入的引号。  例如，若要创建前面提到的字符串，可使用下面的代码：  
  
    ```vb  
    Private Sub InsertQuote()  
       TextBox1.Text = "She said, ""You deserve a treat!"" "  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InsertQuote(){  
       textBox1.Text = "She said, \"You deserve a treat!\" ";  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void InsertQuote()  
       {  
          textBox1->Text = "She said, \"You deserve a treat!\" ";  
       }  
    ```  
  
     \- 或 \-  
  
2.  插入表示引号的 ASCII 字符或 Unicode 字符。  在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中，使用 ASCII 字符 \(34\)。  在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中，使用 Unicode 字符 \(\\u0022\)：  
  
    ```vb  
    Private Sub InsertAscii()  
       TextBox1.Text = "She said, " & Chr(34) & "You deserve a treat!" & Chr(34)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InsertAscii(){  
       textBox1.Text = "She said, " + '\u0022' + "You deserve a treat!" + '\u0022';  
    }  
    ```  
  
    > [!NOTE]
    >  在本示例中，您不能使用 \\u0022，因为您不能使用指定基本字符集中字符的通用字符名。  否则，将产生 C3851。  有关更多信息，请参见 [编译器错误 C3851](../Topic/Compiler%20Error%20C3851.md)。  
  
     \- 或 \-  
  
3.  还可以为该字符定义一个常数，然后在需要时使用：  
  
    ```vb  
    Const quote As String = """"  
    TextBox1.Text = "She said, " & quote & "You deserve a treat!" & quote  
  
    ```  
  
    ```csharp  
    const string quote = "\"";  
    textBox1.Text = "She said, " + quote +  "You deserve a treat!"+ quote ;  
  
    ```  
  
    ```cpp  
    const String^ quote = "\"";  
    textBox1->Text = String::Concat("She said, ",  
       const_cast<String^>(quote), "You deserve a treat!",  
       const_cast<String^>(quote));  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 <xref:Microsoft.VisualBasic.ControlChars.Quote>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)