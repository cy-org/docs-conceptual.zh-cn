---
title: "如何：使用 FontDialog 组件显示字体列表 | Microsoft Docs"
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
  - "“字体”对话框, 显示"
  - "Font 属性, 使用 FontDialog 组件设置"
  - "FontDialog 组件 [Windows 窗体]"
  - "字体, 特性"
  - "字体, 选择"
  - "字体, 显示列表"
ms.assetid: 35692c1b-0937-4b7a-9207-1ae6bdc244a0
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 FontDialog 组件显示字体列表
用户可以使用 [FontDialog](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md) 组件选择字体，并可以更改字体显示方式，例如粗细和大小。  
  
 在该对话框中选择的字体在 <xref:System.Windows.Forms.FontDialog.Font%2A> 属性中返回。  因此，使用用户选定的字体就像读取属性一样简单。  
  
### 使用 FontDialog 组件选择字体属性  
  
1.  使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示对话框。  
  
2.  使用 <xref:System.Windows.Forms.DialogResult> 属性确定对话框是如何关闭的。  
  
3.  使用 <xref:System.Windows.Forms.FontDialog.Font%2A> 属性设置所需的字体。  
  
     在下面的示例中，<xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序打开一个 <xref:System.Windows.Forms.FontDialog> 组件。  当用户选定字体并单击**“确定”**时，窗体上的 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.FontDialog.Font%2A> 属性被设置为选定的字体。  本示例假定窗体上有一个 <xref:System.Windows.Forms.Button> 控件、一个 <xref:System.Windows.Forms.TextBox> 控件、一个 <xref:System.Windows.Forms.FontDialog> 组件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If FontDialog1.ShowDialog() = DialogResult.OK Then  
          TextBox1.Font = FontDialog1.Font  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(fontDialog1.ShowDialog() == DialogResult.OK)  
       {  
          textBox1.Font = fontDialog1.Font;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(fontDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Font = fontDialog1->Font;  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码来注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.FontDialog>   
 [FontDialog 组件](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md)