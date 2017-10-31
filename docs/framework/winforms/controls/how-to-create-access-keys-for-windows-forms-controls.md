---
title: "如何：创建 Windows 窗体控件的访问键 | Microsoft Docs"
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
  - "访问键, 为控件创建"
  - "访问键, Windows 窗体"
  - "Alt 键"
  - "快捷键中的“&”符"
  - "Button 控件 [Windows 窗体], 访问键"
  - "控件 [Windows 窗体], 访问键"
  - "对话框控件, 助记键"
  - "示例 [Windows 窗体], 控件"
  - "键盘快捷键, 为控件创建"
  - "助记键"
  - "助记键, 添加到对话框控件"
  - "Text 属性, 为控件指定访问键"
  - "Windows 窗体控件, 访问键"
ms.assetid: 4faa0991-28ec-4eca-91db-51dc2cd6a7ac
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：创建 Windows 窗体控件的访问键
“访问键”是菜单、菜单项或控件（如按钮）标签的文本中带下划线的字符。  访问键允许用户通过同时按 Alt 键和预先定义的访问键来“单击”按钮。  例如，如果某个按钮运行打印窗体的过程，而且因此其 `Text` 属性设置为“Print,”，则在字母“P”前添加“&”符会使得字母“P”在运行时的按钮文本中带有下划线。  用户可以通过按下 Alt\+P 运行与该按钮关联的命令。  对于不能接收焦点的控件，不能设置访问键。  
  
### 创建控件的访问键  
  
1.  将 `Text` 属性设置为一个字符串，该字符串在将设成快捷键的字母前包含一个“&”符。  
  
    ```vb  
    ' Set the letter "P" as an access key.  
    Button1.Text = "&Print"  
  
    ```  
  
    ```csharp  
    // Set the letter "P" as an access key.  
    button1.Text = "&Print";  
  
    ```  
  
    ```cpp  
    // Set the letter "P" as an access key.  
    button1->Text = "&Print";  
    ```  
  
    > [!NOTE]
    >  若要在标题中加入一个“&”符而不创建访问键，请加入两个“&”符 \(&&\)。  这样，在标题中显示单个“&”符，并且没有带下划线的字符。  
  
## 请参阅  
 <xref:System.Windows.Forms.Button>   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)