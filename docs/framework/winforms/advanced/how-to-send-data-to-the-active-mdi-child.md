---
title: "如何：将数据发送到活动的 MDI 子窗体 | Microsoft Docs"
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
  - "剪贴板, 获取数据"
  - "剪贴板, 粘贴"
  - "MDI, 将数据发送到窗体"
ms.assetid: 1047d2fe-1235-46db-aad9-563aea1d743b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：将数据发送到活动的 MDI 子窗体
通常，在[多文档界面 \(MDI\) 应用程序](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)的上下文中，需要将数据发送到活动子窗口，例如用户将数据从剪贴板中粘贴到 MDI 应用程序中。  
  
> [!NOTE]
>  有关检验哪个子窗口具有焦点以及将子窗口内容发送到剪贴板的信息，请参见[确定活动 MDI 子窗口](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)。  
  
### 将数据从剪贴板发送到活动 MDI 子窗口  
  
1.  在方法中，将剪贴板上的文本复制到活动子窗体的活动控件。  
  
    > [!NOTE]
    >  此示例假定有一个 MDI 父窗体 \(`Form1`\)，其中包含一个或多个含有 <xref:System.Windows.Forms.RichTextBox> 控件的 MDI 子窗口。  有关更多信息，请参见[创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)。  
  
    ```vb  
    Public Sub mniPaste_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniPaste.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ParentForm.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Try  
             Dim theBox As RichTextBox = Ctype(activeChild.ActiveControl, RichTextBox)  
             If (Not theBox Is Nothing) Then  
                ' Create a new instance of the DataObject interface.  
                Dim data As IDataObject = Clipboard.GetDataObject()  
                ' If the data is text, then set the text of the   
                ' RichTextBox to the text in the clipboard.  
                If (data.GetDataPresent(DataFormats.Text)) Then  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString()  
                End If  
             End If  
          Catch  
             MessageBox.Show("You need to select a RichTextBox.")  
          End Try  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void mniPaste_Click (object sender, System.EventArgs e)  
    {  
      // Determine the active child form.  
       Form activeChild = this.ParentForm.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {  
          try   
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Create a new instance of the DataObject interface.  
                IDataObject data = Clipboard.GetDataObject();  
                // If the data is text, then set the text of the   
                // RichTextBox to the text in the clipboard.  
                if (data.GetDataPresent(DataFormats.Text))  
                {  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString();                 
                }  
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
 [如何：确定活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)   
 [如何：排列 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)