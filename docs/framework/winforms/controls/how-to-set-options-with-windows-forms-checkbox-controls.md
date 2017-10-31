---
title: "如何：使用 Windows 窗体 CheckBox 控件设置选项 | Microsoft Docs"
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
  - "checked"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "复选框, 用以设置选项"
  - "CheckBox 控件 [Windows 窗体], 选中状态"
  - "CheckBox 控件 [Windows 窗体], 用以设置选项"
ms.assetid: 2ac70498-7e3e-4e07-8901-ccabaeb5fd3e
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 CheckBox 控件设置选项
Windows 窗体 <xref:System.Windows.Forms.CheckBox> 控件用于为用户提供真\/假或是\/否选项。  当控件选定时，将显示一个复选标记。  
  
### 使用 CheckBox 控件设置选项  
  
1.  检查 <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性的值以确定其状态，并使用该值设置选项。  
  
     在下面的代码示例中，当引发 <xref:System.Windows.Forms.CheckBox> 控件的 <xref:System.Windows.Forms.CheckBox.CheckedChanged> 事件时，如果选中该复选框，则窗体的 <xref:System.Windows.Forms.Control.AllowDrop%2A> 属性将被设置为 `false`。  这在希望限制用户交互的情况下是很有用的。  
  
    ```vb  
    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged  
       ' Determine the CheckState of the check box.  
       If CheckBox1.CheckState = CheckState.Checked Then  
          ' If checked, do not allow items to be dragged onto the form.  
          Me.AllowDrop = False  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_CheckedChanged(object sender, System.EventArgs e)  
    {  
       // Determine the CheckState of the check box.  
       if (checkBox1.CheckState == CheckState.Checked)   
       {  
          // If checked, do not allow items to be dragged onto the form.  
          this.AllowDrop = false;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Determine the CheckState of the check box.  
          if (checkBox1->CheckState == CheckState::Checked)   
          {  
             // If checked, do not allow items to be dragged onto the form.  
             this->AllowDrop = false;  
          }  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.CheckBox>   
 [CheckBox 控件概述](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [如何：响应 Windows 窗体 CheckBox 的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-checkbox-clicks.md)   
 [CheckBox 控件](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)