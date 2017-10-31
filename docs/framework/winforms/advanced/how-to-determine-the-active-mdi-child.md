---
title: "如何：确定活动的 MDI 子窗体 | Microsoft Docs"
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
  - "子窗体"
  - "剪贴板, 将数据复制到"
  - "MDI, 激活窗体"
  - "MDI, 子窗口"
  - "MDI, 查找焦点"
ms.assetid: 33880ec3-0207-4c2b-a616-ff140443cc0f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：确定活动的 MDI 子窗体
有时需要提供一个在控件上操作的命令，而该控件在当前活动的子窗体上具有焦点。  例如，假设要将子窗体文本框中的选定文本复制到剪贴板。  可以创建这样一个过程：使用标准“编辑”菜单上“复制”菜单项的 <xref:System.Windows.Forms.Control.Click> 事件将选定的文本复制到剪贴板。  
  
 因为一个 MDI 应用程序可以有同一个子窗体的多个实例，因此该过程需要知道使用哪个窗体。  若要指定正确的窗体，请使用 <xref:System.Windows.Forms.Form.ActiveMdiChild%2A> 属性，该属性返回具有焦点的或最近活动的子窗体。  
  
 当窗体上有数个控件时，还需要指定哪个控件是活动的。  与 <xref:System.Windows.Forms.Form.ActiveMdiChild%2A> 属性一样，<xref:System.Windows.Forms.ContainerControl.ActiveControl%2A> 属性返回活动子窗体中具有焦点的控件。  下面的过程阐释了可以从子窗体菜单、MDI 窗体菜单或工具栏按钮调用的复制过程。  
  
### 确定活动的 MDI 子窗体（将它的文本复制到剪贴板）  
  
1.  在方法中，将活动子窗体的活动控件的文本复制到剪贴板。  
  
    > [!NOTE]
    >  此示例假定有一个 MDI 父窗体 \(`Form1`\)，其中包含一个或多个含有 <xref:System.Windows.Forms.RichTextBox> 控件的 MDI 子窗口。  有关更多信息，请参见[创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)。  
  
    ```vb  
    Public Sub mniCopy_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniCopy.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Dim theBox As RichTextBox = _  
            TryCast(activeChild.ActiveControl, RichTextBox)  
  
          If (Not theBox Is Nothing) Then  
             'Put selected text on Clipboard.  
             Clipboard.SetDataObject(theBox.SelectedText)  
          Else  
             MessageBox.Show("You need to select a RichTextBox.")  
          End If  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void mniCopy_Click (object sender, System.EventArgs e)  
    {  
       // Determine the active child form.  
       Form activeChild = this.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {    
          try  
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Put the selected text on the Clipboard.  
                Clipboard.SetDataObject(theBox.SelectedText);  
  
             }  
          }  
          catch  
          {  
             MessageBox.Show("You need to select a RichTextBox.");  
          }  
       }  
    }  
  
    ```  
  
## 请参阅  
 [多文档界面 \(MDI\) 应用程序](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [如何：将数据发送到活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)   
 [如何：排列 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)