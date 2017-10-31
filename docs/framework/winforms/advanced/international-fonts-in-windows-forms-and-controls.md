---
title: "Windows 窗体和控件中的国际字体 | Microsoft Docs"
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
  - "Windows 窗体中的字体代用"
  - "字体, 全球化注意事项"
  - "字体, 国际化"
  - "全球化 [Windows 窗体], 字符集"
  - "国际应用程序 [Windows 窗体], 字符显示"
  - "本地化 [Windows 窗体], 字体"
  - "Windows 窗体控件, 标签"
ms.assetid: 2c3066df-9bac-479a-82b2-79e484b346a3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Windows 窗体和控件中的国际字体
在国际化应用程序中，选择字体的推荐方法是尽可能使用字体后备。  字体后备意味着系统确定字符属于哪一脚本。  
  
## 使用字体后备  
 若要利用此功能，则不要为窗体或其他任何元素设置 <xref:System.Drawing.Font> 属性。  应用程序将自动使用默认系统字体，而操作系统的本地化语言不同，则默认系统字体也将不同。  当应用程序运行时，系统将自动为操作系统中选择的区域性提供正确的字体。  
  
 对于此不设置字体规则有一点例外，即对于更改字体样式的情况。  对于某一应用程序，如果用户要在其中单击一个按钮以使文本框中的文本以粗体显示，这一点可能十分重要。  若要执行此操作，应该基于该窗体的任何字体，编写一个函数来将文本框的字体样式更改为粗体。  必须在两个地方调用此函数：在按钮的 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，以及在 <xref:System.Windows.Forms.Control.FontChanged> 事件处理程序中。  如果只在 <xref:System.Windows.Forms.Control.Click> 事件处理程序中调用该函数，并且代码的某些其他部分更改了整个窗体的字体系列，则该文本框将不随窗体的其余部分的更改而更改。  
  
```  
' Visual Basic  
Private Sub MakeBold()  
   ' Change the TextBox to a bold version of the form font  
   TextBox1.Font = New Font(Me.Font, FontStyle.Bold)  
End Sub  
  
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
   ' Clicking this button makes the TextBox bold  
   MakeBold()  
End Sub  
  
Private Sub Form1_FontChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.FontChanged  
   ' If the TextBox is already bold and the form's font changes,  
   ' change the TextBox to a bold version of the new form font  
   If (TextBox1.Font.Style = FontStyle.Bold) Then  
      MakeBold()  
   End If  
End Sub  
  
// C#  
private void button1_Click(object sender, System.EventArgs e)  
{  
   // Clicking this button makes the TextBox bold  
   MakeBold();  
}  
  
private void MakeBold()   
{  
   // Change the TextBox to a bold version of the form's font  
   textBox1.Font = new Font(this.Font, FontStyle.Bold);  
}  
  
private void Form1_FontChanged(object sender, System.EventArgs e)  
{  
   // If the TextBox is already bold and the form's font changes,  
   // change the TextBox to a bold version of the new form font  
   if (textBox1.Font.Style == FontStyle.Bold)   
   {  
      MakeBold();  
   }  
}  
```  
  
 但是，在本地化应用程序时，对于某些语言粗体可能不能正确显示。  如果此问题较为重要，您想让本地化人员来选择将字体从粗体切换为常规文本。  因为本地化人员通常不是开发人员并且没有对源代码的访问权限，而只能访问资源文件，所以需要在资源文件中设置该选项。  为此，需要将 <xref:System.Drawing.Font.Bold%2A> 属性设置为 `true`。  这导致字体设置被写出到资源文件，而本地化人员可以在资源文件中对其进行编辑。  然后可以基于该窗体的任何字体（但使用在资源文件中指定的字体样式），在 `InitializeComponent`  方法之后编写代码来重置该字体。  
  
```  
' Visual Basic  
TextBox1.Font = New System.Drawing.Font(Me.Font, TextBox1.Font.Style)  
  
// C#  
textBox1.Font = new System.Drawing.Font(this.Font, textBox1.Font.Style);  
```  
  
## 请参阅  
 [全球化 Windows 窗体](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)