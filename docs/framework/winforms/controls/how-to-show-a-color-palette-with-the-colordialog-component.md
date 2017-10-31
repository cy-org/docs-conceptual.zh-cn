---
title: "如何：使用 ColorDialog 组件显示调色板 | Microsoft Docs"
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
  - "颜色对话框, 显示调色板"
  - "调色板, 对话框"
  - "调色板, 在 ColorDialog 组件中显示"
  - "Color 属性"
  - "ColorDialog 组件, 显示调色板"
  - "颜色, 允许用户选择"
  - "颜色, 显示调色板"
  - "调色板, 显示颜色"
ms.assetid: ee050f61-dbc8-4436-ba22-51360981ab48
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 ColorDialog 组件显示调色板
[ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md) 组件显示调色板并返回包含用户选定颜色的属性。  
  
### 使用 ColorDialog 组件选择颜色  
  
1.  使用 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 方法显示对话框。  
  
2.  使用 <xref:System.Windows.Forms.DialogResult> 属性确定对话框是如何关闭的。  
  
3.  使用 <xref:System.Windows.Forms.ColorDialog> 组件的 <xref:System.Windows.Forms.ColorDialog.Color%2A> 属性设置选定的颜色。  
  
     在下面的示例中，<xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序打开一个 <xref:System.Windows.Forms.ColorDialog> 组件。  当用户选定颜色并单击 **“确定”**后，<xref:System.Windows.Forms.Button> 控件的背景色将设置为选定的颜色。  本示例假设窗体具有一个 <xref:System.Windows.Forms.Button> 控件和一个 <xref:System.Windows.Forms.ColorDialog> 组件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       If ColorDialog1.ShowDialog() = DialogResult.OK Then  
          Button1.BackColor = ColorDialog1.Color  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(colorDialog1.ShowDialog() == DialogResult.OK)  
       {  
          button1.BackColor = colorDialog1.Color;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,   
          System::EventArgs ^ e)  
       {  
          if(colorDialog1->ShowDialog() == DialogResult::OK)  
          {  
             button1->BackColor = colorDialog1->Color;  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click +=   
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ColorDialog>   
 [ColorDialog 组件](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)