---
title: "如何：设置 Windows 窗体控件所显示的文本 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 按钮文本"
  - "Button 控件 [Windows 窗体], 文本显示"
  - "按钮, 文本"
  - "标题, 设置"
  - "标题, Windows 窗体控件"
  - "控件 [Windows 窗体], 标题"
  - "示例 [Windows 窗体], 控件"
  - "窗体, 标题"
  - "标签, 添加到 CommandButton 控件"
  - "StdFont 对象和 CommandButton 标题"
  - "文本"
  - "Text 属性, Windows 窗体控件"
  - "文本, Windows 窗体控件"
  - "Windows 窗体, 标题"
ms.assetid: 36b95bff-8780-479d-b86a-f1a0673653aa
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：设置 Windows 窗体控件所显示的文本
Windows 窗体控件通常会显示一些与控件的主要功能相关的文本。  例如，<xref:System.Windows.Forms.Button> 控件通常会显示一个题注，用于指示单击按钮时将执行的操作。  对于所有控件而言，都可通过使用 <xref:System.Windows.Forms.Control.Text%2A> 属性来设置或返回文本。  可以使用 <xref:System.Windows.Forms.Control.Font%2A> 属性更改字体。  还可使用设计器来设置文本。  另请参阅[如何：使用设计器为 Windows 窗体控件创建访问键](http://msdn.microsoft.com/library/ms233673%20\(v=vs.110\))，[如何：使用设计器设置 Windows 窗体控件显示的文本](http://msdn.microsoft.com/library/ms233665%20\(v=vs.110\))，[如何：使用设计器设置 Windows 窗体控件显示的图像](http://msdn.microsoft.com/library/ms233656%20\(v=vs.110\))。  
  
### 以编程方式设置控件所显示的文本  
  
1.  将 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为字符串。  
  
     若要创建一个带下划线的访问键，请使将成为访问键的字母前包含一个 & 号 \(&\)。  
  
2.  将 <xref:System.Windows.Forms.Control.Font%2A> 属性设置为类型 <xref:System.Drawing.Font> 的对象。  
  
    ```vb  
    Button1.Text = "Click here to save changes"  
    Button1.Font = New Font("Arial", 10, FontStyle.Bold, GraphicsUnit.Point)  
    ```  
  
    ```csharp  
    button1.Text = "Click here to save changes";  
    button1.Font = new Font("Arial", 10, FontStyle.Bold,  
       GraphicsUnit.Point);  
    ```  
  
    ```cpp#  
    button1->Text = "Click here to save changes";  
    button1->Font = new System::Drawing::Font("Arial",  
       10, FontStyle::Bold, GraphicsUnit::Point);  
    ```  
  
    > [!NOTE]
    >  可使用转义符来显示用户界面元素中的特殊字符，通常对这些元素（如菜单项）有着不同的解释。  例如，下面的代码行将菜单项的文本设置为“现读取完全不同的内容”：  
  
    ```vb  
    MPMenuItem.Text = "&& Now For Something Completely Different"  
    ```  
  
    ```csharp  
    mpMenuItem.Text = "&& Now For Something Completely Different";  
    ```  
  
    ```cpp#  
    mpMenuItem->Text = "&& Now For Something Completely Different";  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.Text%2A?displayProperty=fullName>   
 [如何：创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)