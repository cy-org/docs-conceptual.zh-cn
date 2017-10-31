---
title: "如何：响应 Windows 窗体按钮的单击 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 单击响应"
  - "按钮, 响应 Click 事件"
  - "Click 事件, Button 控件"
  - "Click 事件, 响应"
  - "双击"
  - "事件 [Windows 窗体], Click 事件"
  - "示例 [Windows 窗体], 控件"
  - "MouseDown 事件"
ms.assetid: 7a4951bd-369c-4662-b246-28ad83eda484
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：响应 Windows 窗体按钮的单击
Windows 窗体 <xref:System.Windows.Forms.Button> 控件的最基本用法是在单击按钮时运行某些代码。  
  
 单击 <xref:System.Windows.Forms.Button> 控件还生成许多其他事件，如 <xref:System.Windows.Forms.Control.MouseEnter>、<xref:System.Windows.Forms.Control.MouseDown> 和 <xref:System.Windows.Forms.Control.MouseUp> 事件。  如果打算为这些相关事件附加事件处理程序，请确保它们的操作不冲突。  例如，如果单击该按钮将清除用户已键入文本框的信息，则鼠标指针在该按钮上暂停时就不应显示带有该已不存在的信息的工具提示。  
  
 如果用户尝试双击 <xref:System.Windows.Forms.Button> 控件，每次单击将单独处理；也就是说，该控件不支持双击事件。  
  
### 响应按钮单击  
  
-   在按钮的`Click` <xref:System.EventHandler> 中编写要运行的代码。  `Button1_Click` 必须绑定到对应的控件。  有关更多信息，请参见 [如何：在运行时为 Windows 窗体创建事件处理程序](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md)。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       MessageBox.Show("Button1 was clicked")  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       MessageBox.Show("button1 was clicked");  
    }  
    ```  
  
    ```cpp#  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          MessageBox::Show("button1 was clicked");  
       }  
    ```  
  
## 请参阅  
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)