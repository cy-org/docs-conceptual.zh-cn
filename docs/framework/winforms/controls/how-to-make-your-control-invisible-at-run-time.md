---
title: "如何：使控件在运行时不可见 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 使在运行时不可见"
  - "自定义控件 [Windows 窗体], 不可见"
  - "不可见的控件"
  - "运行时, 使控件不可见"
  - "用户控件 [Windows 窗体], 不可见"
ms.assetid: 69eb2e72-32f5-4f79-a157-c2c5f60c1628
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使控件在运行时不可见
有时可能需要创建在运行时不可见的用户控件。  例如，除在闹铃响时外，用作闹钟的控件可以不可见。  通过设置 <xref:System.Windows.Forms.Control.Visible%2A> 属性很容易做到这一点。  如果 <xref:System.Windows.Forms.Control.Visible%2A> 属性为 `true`，控件将正常显示。  如果为 `false`，控件被隐藏。  尽管在不可见状态下控件中的代码仍可运行，但您无法通过用户界面与控件交互。  如果想创建仍可响应用户输入（例如鼠标单击）的不可见控件，则应创建透明控件。  有关更多信息，请参见[使控件拥有透明背景](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)。  
  
### 使控件在运行时不可见  
  
1.  将 <xref:System.Windows.Forms.Control.Visible%2A> 属性设置为 `false`。  
  
    ```vb  
    ' To set the Visible property from within your object's own code.  
    Me.Visible = False  
    ' To set the Visible property from another object.  
    myControl1.Visible = False  
  
    ```  
  
    ```csharp  
    // To set the Visible property from within your object's own code.  
    this.Visible = false;  
    // To set the Visible property from another object.  
    myControl1.Visible = false;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.Visible%2A>   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [如何：使控件拥有透明背景](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)