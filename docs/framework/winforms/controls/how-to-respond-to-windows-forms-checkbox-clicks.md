---
title: "如何：响应 Windows 窗体 CheckBox 的单击 | Microsoft Docs"
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
  - "复选框, 对事件作出响应"
  - "CheckBox 控件 [Windows 窗体], Click 事件"
  - "Click 事件, CheckBox 控件"
  - "双击"
  - "事件 [Windows 窗体], Click 事件"
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：响应 Windows 窗体 CheckBox 的单击
每当用户单击某 Windows 窗体 <xref:System.Windows.Forms.CheckBox> 控件时，便引发 <xref:System.Windows.Forms.Control.Click> 事件。  可以编写应用程序以根据复选框的状态执行某些操作。  
  
### 响应 CheckBox 单击  
  
1.  在 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，使用 <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性确定控件的状态，并执行任何必要操作。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the   
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the   
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  如果用户尝试双击 <xref:System.Windows.Forms.CheckBox> 控件，每次单击都将单独处理；也就是说，<xref:System.Windows.Forms.CheckBox> 控件不支持双击事件。  
  
    > [!NOTE]
    >  如果 <xref:System.Windows.Forms.CheckBox.AutoCheck%2A> 属性为 `true`（默认值），则 <xref:System.Windows.Forms.CheckBox> 在被单击时会自动选中或清除。  否则，当 <xref:System.Windows.Forms.Control.Click> 事件引发时，必须手动设置 <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性。  
  
     还可以使用 <xref:System.Windows.Forms.CheckBox> 控件确定操作的进程。  
  
### 单击复选框时确定操作的进程  
  
1.  使用 case 语句查询 <xref:System.Windows.Forms.CheckBox.CheckState%2A> 属性的值以确定操作的进程。  当 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 属性设置为 `true` 时，<xref:System.Windows.Forms.CheckBox.CheckState%2A> 属性可以返回三个可能值，表示该复选框已选中、未选中或第三种不确定状态（此时复选框以浅灰色显示，表示该选项不可用）。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select   
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  当 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 属性设置为 `true` 时，<xref:System.Windows.Forms.CheckBox.Checked%2A> 属性对于 <xref:System.Windows.Forms.CheckState> 和 <xref:System.Windows.Forms.CheckState> 都返回 `true`。  
  
## 请参阅  
 <xref:System.Windows.Forms.CheckBox>   
 [CheckBox 控件概述](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 CheckBox 控件设置选项](../../../../docs/framework/winforms/controls/how-to-set-options-with-windows-forms-checkbox-controls.md)   
 [CheckBox 控件](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)