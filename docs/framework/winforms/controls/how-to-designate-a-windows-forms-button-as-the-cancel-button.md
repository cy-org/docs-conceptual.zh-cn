---
title: "如何：将 Windows 窗体按钮指定为“取消”按钮 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 指定为取消按钮"
  - "按钮, 取消按钮"
ms.assetid: 252f0834-e54b-44d9-96f7-ee5f50e94f2c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：将 Windows 窗体按钮指定为“取消”按钮
在任何 Windows 窗体上，您都可以将 <xref:System.Windows.Forms.Button> 控件指定为“取消”按钮。  每当用户按 Esc 键时，即单击“取消”按钮，而不管窗体上的其他哪个控件具有焦点。  通常设计这样的按钮是为了允许用户快速退出操作而无需执行任何动作。  
  
### 指定“取消”按钮  
  
1.  将窗体的 <xref:System.Windows.Forms.Form.CancelButton%2A> 属性设置为适当的 <xref:System.Windows.Forms.Button> 控件。  
  
    ```vb  
    Private Sub SetCancelButton(ByVal myCancelBtn As Button)  
       Me.CancelButton = myCancelBtn  
    End Sub  
    ```  
  
    ```csharp  
    private void SetCancelButton(Button myCancelBtn)  
    {  
       this.CancelButton = myCancelBtn;  
    }  
    ```  
  
    ```cpp  
    private:  
       void SetCancelButton(Button ^ myCancelBtn)  
       {  
          this->CancelButton = myCancelBtn;  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Form.CancelButton%2A>   
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：将 Windows 窗体按钮指定为“接受”按钮](../../../../docs/framework/winforms/controls/how-to-designate-a-windows-forms-button-as-the-accept-button.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)