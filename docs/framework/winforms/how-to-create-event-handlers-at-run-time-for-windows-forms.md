---
title: "如何：在运行时为 Windows 窗体创建事件处理程序 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 事件处理程序"
  - "事件处理程序, 创建"
  - "示例 [Windows 窗体], 事件处理"
  - "运行时, 创建事件处理程序"
  - "Windows 窗体, 事件处理"
ms.assetid: 2e7c9e1a-61fe-444d-8113-3c5bacf1c8cb
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在运行时为 Windows 窗体创建事件处理程序
除了使用“Windows 窗体设计器”创建事件外，还可以在运行时创建事件处理程序。  该操作允许在运行时根据代码中的条件连接相应的事件处理程序，而不是在程序刚启动时连接事件处理程序。  
  
### 在运行时创建事件处理程序  
  
1.  在代码编辑器中打开要向其添加事件处理程序的窗体。  
  
2.  对于要处理的事件，将带有其方法签名的方法添加到窗体上。  
  
     例如，如果要处理 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件，则需创建如下的一个方法：  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)  
       ' Add event handler code here.  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
    // Add event handler code here.  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,   
          System::EventArgs ^ e)  
       {  
          // Add event handler code here.  
       }  
    ```  
  
3.  将适合应用程序的代码添加到事件处理程序中。  
  
4.  确定要为其创建事件处理程序的窗体或控件。  
  
5.  在窗体类中的方法中，添加指定事件处理程序的代码处理事件。  例如，下列代码指定事件处理程序 `button1_Click` 处理 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件：  
  
    ```vb  
    AddHandler Button1.Click, AddressOf Button1_Click  
  
    ```  
  
    ```csharp  
    button1.Click += new EventHandler(button1_Click);  
  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     上文用 Visual Basic 代码演示的 <xref:System.ComponentModel.EventHandlerList.AddHandler%2A> 方法为按钮建立了 click 事件处理程序。  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [事件处理程序概述](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)   
 [有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)