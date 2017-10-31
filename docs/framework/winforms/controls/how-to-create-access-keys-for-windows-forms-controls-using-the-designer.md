---
title: "如何：使用设计器为 Windows 窗体控件创建访问键 | Microsoft Docs"
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
  - "助记键, 添加到对话框控件"
  - "Text 属性, 为控件指定访问键"
  - "Windows 窗体控件, 访问键"
ms.assetid: 4c374c4c-4ca9-4a68-ac96-9dc3ab0f518a
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用设计器为 Windows 窗体控件创建访问键
“访问键”是菜单、菜单项或控件（如按钮）标签的文本中带下划线的字符。  它允许用户通过同时按下 Alt 键和预先定义的访问键来“单击”某个按钮。  例如，如果某个按钮可运行打印窗体的过程，并且因此将它的 `Text` 属性设为“Print”，则在字母“P”前添加“&”符会使得字母“P”在运行时的按钮文本中带有下划线。  用户可以通过按下 Alt\+P 运行与该按钮关联的命令。  对于不能接收焦点的控件，不能设置访问键。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建控件的访问键  
  
1.  在**“属性”**窗口中，将 `Text` 属性设置为一个字符串，该字符串在将作为访问键的字母前包含一个“&”符。  例如，若要将字母“P”设置为访问键，请将“&Print”键入到网格中。  
  
## 请参阅  
 <xref:System.Windows.Forms.Button>   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)