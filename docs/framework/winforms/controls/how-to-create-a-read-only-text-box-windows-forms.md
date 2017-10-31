---
title: "如何：创建只读文本框（Windows 窗体） | Microsoft Docs"
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
  - "只读文本框"
  - "文本框, 只读"
  - "TextBox 控件 [Windows 窗体], 只读"
ms.assetid: 60baa9ab-fa57-44ad-bb7c-61b05aa64296
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建只读文本框（Windows 窗体）
可以将可编辑的 Windows 窗体文本框转换成只读控件。  例如，文本框可能显示一个值，该值通常可以进行编辑，但目前因应用程序的状态而无法进行编辑。  
  
### 创建只读文本框  
  
1.  将 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> 属性设置为 `true`。  将该属性设置为 `true` 后，用户仍可滚动并突出显示文本框中的文本，但不允许进行更改。  **“复制”**命令在文本框中仍然有效，但**“剪切”**和**“粘贴”**命令都不起作用。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> 属性仅在运行时影响用户交互。  仍可以在运行时通过更改文本框的 <xref:System.Windows.Forms.TextBox.Text%2A> 属性，以编程方式更改文本框的内容。  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [如何：在 Windows 窗体 TextBox 控件中查看多个行](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)