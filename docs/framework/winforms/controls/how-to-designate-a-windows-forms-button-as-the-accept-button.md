---
title: "如何：将 Windows 窗体按钮指定为“接受”按钮 | Microsoft Docs"
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
  - "Windows 窗体上的“接受”按钮"
  - "Button 控件 [Windows 窗体], 指定为默认值"
  - "按钮, Windows 窗体上的默认按钮"
  - "Windows 窗体控件, 窗体上的默认按钮"
ms.assetid: 22cc9da6-b913-4e04-9554-dee443ac5c3a
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：将 Windows 窗体按钮指定为“接受”按钮
在任何 Windows 窗体上都可以将某个 <xref:System.Windows.Forms.Button> 控件指定为“接受”按钮（也称作默认按钮）。  每当用户按 Enter 键时，即单击默认按钮，而不管窗体上其他哪个控件具有焦点。  
  
> [!NOTE]
>  但当具有焦点的控件为以下情形时存在例外：为另一个按钮，此时，将单击具有焦点的那个按钮；为多行文本框；为捕获了 Enter 键的自定义控件。  
  
### 指定“接受”按钮  
  
1.  将窗体的 <xref:System.Windows.Forms.Form.AcceptButton%2A> 属性设置为适当的 <xref:System.Windows.Forms.Button> 控件。  
  
    ```vb  
    Private Sub SetDefault(ByVal myDefaultBtn As Button)  
      Me.AcceptButton = myDefaultBtn   
    End Sub  
    ```  
  
    ```csharp  
    private void SetDefault(Button myDefaultBtn)  
    {  
       this.AcceptButton = myDefaultBtn;  
    }  
    ```  
  
    ```cpp  
    private:  
       void SetDefault(Button ^ myDefaultBtn)  
       {  
          this->AcceptButton = myDefaultBtn;  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Form.AcceptButton%2A>   
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [选择 Windows 窗体 Button 控件的方法](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：将 Windows 窗体按钮指定为“取消”按钮](../../../../docs/framework/winforms/controls/how-to-designate-a-windows-forms-button-as-the-cancel-button.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)