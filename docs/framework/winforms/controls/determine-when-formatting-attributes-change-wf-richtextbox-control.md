---
title: "如何：确定 Windows 窗体 RichTextBox 控件中的格式设置特性何时更改 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 文本框"
  - "RichTextBox 控件 [Windows 窗体], 确定字体更改"
  - "SelBold 属性"
  - "SelChange 事件"
  - "文本框, 确定字体更改"
ms.assetid: bdfed015-f77a-41e5-b38f-f8629b2fa166
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：确定 Windows 窗体 RichTextBox 控件中的格式设置特性何时更改
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件的通常用途是使用字体选项或段落样式等特性来格式化文本。  如许多字处理应用程序一样，您的应用程序可能需要跟踪文本格式设置的任何更改，以便显示工具栏。  
  
### 响应格式特性的更改  
  
1.  在 <xref:System.Windows.Forms.RichTextBox.SelectionChanged> 事件处理程序中编写代码以根据特性值来执行合适的操作。  下面的示例根据 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 属性的值来更改工具栏按钮的外观。  只有当插入点在控件中移动时，才会更新工具栏按钮。  
  
     下面的示例假定窗体具有一个 <xref:System.Windows.Forms.RichTextBox> 控件和一个包含工具栏按钮的 <xref:System.Windows.Forms.ToolBar> 控件。  有关工具栏以及工具栏按钮的更多信息，请参见 [如何：向 ToolBar 控件添加按钮](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)。  
  
    ```vb  
    ' The following code assumes the existence of a toolbar control  
    ' with at least one toolbar button.  
    Private Sub RichTextBox1_SelectionChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles RichTextBox1.SelectionChanged  
       If RichTextBox1.SelectionBullet = True Then  
          ' Bullet button on toolbar should appear pressed  
          ToolBarButton1.Pushed = True  
       Else  
           ' Bullet button on toolbar should appear unpressed  
           ToolBarButton1.Pushed = False  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private void richTextBox1_SelectionChanged(object sender,  
    System.EventArgs e)  
    {  
       if (richTextBox1.SelectionBullet == true)   
       {  
          // Bullet button on toolbar should appear pressed  
          toolBarButton1.Pushed = true;  
       }  
       else   
       {  
          // Bullet button on toolbar should appear unpressed  
          toolBarButton1.Pushed = false;  
       }  
    }  
  
    ```  
  
    ```cpp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private:  
       System::Void richTextBox1_SelectionChanged(  
          System::Object ^  sender, System::EventArgs ^  e)  
       {  
          if (richTextBox1->SelectionBullet == true)  
          {  
             // Bullet button on toolbar should appear pressed  
             toolBarButton1->Pushed = true;  
          }  
          else  
          {  
             // Bullet button on toolbar should appear unpressed  
             toolBarButton1->Pushed = false;  
          }  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox.SelectionChanged>   
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)