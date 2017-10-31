---
title: "如何：为 Windows 窗体 RichTextBox 控件设置字体特性 | Microsoft Docs"
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
  - ".rtf 文件, 在 RichTextBox 控件中设置格式"
  - "字体, 更改 RichTextBox 控件中的特性"
  - "格式设置 [Windows 窗体]"
  - "RichTextBox 控件 [Windows 窗体], 设置字体特性"
  - "RTF 文件, 在 RichTextBox 控件中设置格式"
  - "文本 [Windows 窗体]"
  - "文本框, 格式化文本"
ms.assetid: 2bc23ddb-0529-4489-a1a2-ad253cb43f9a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：为 Windows 窗体 RichTextBox 控件设置字体特性
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件具有多个用于设置所显示的文本的格式的选项。  可以使用 <xref:System.Windows.Forms.RichTextBox.SelectionFont%2A> 属性使选定的字符变为粗体、带下划线或斜体格式。  也可以使用此属性来更改选定字符的大小和字样。  <xref:System.Windows.Forms.RichTextBox.SelectionColor%2A> 属性可用于更改选定字符的颜色。  
  
### 更改字符的外观  
  
1.  将 <xref:System.Windows.Forms.RichTextBox.SelectionFont%2A> 属性设置为合适的字体。  
  
     若要使用户能够在应用程序中设置字体系列、大小和字样，通常可以使用 <xref:System.Windows.Forms.FontDialog> 组件。  有关概述，请参见[FontDialog 组件概述](../../../../docs/framework/winforms/controls/fontdialog-component-overview-windows-forms.md)。  
  
2.  将 <xref:System.Windows.Forms.RichTextBox.SelectionColor%2A> 属性设置为合适的颜色。  
  
     若要使用户能够在应用程序中设置颜色，通常可以使用 <xref:System.Windows.Forms.ColorDialog> 组件。  有关概述，请参见[ColorDialog 组件概述](../../../../docs/framework/winforms/controls/colordialog-component-overview-windows-forms.md)。  
  
    ```vb  
    RichTextBox1.SelectionFont = New Font("Tahoma", 12, FontStyle.Bold)  
    RichTextBox1.SelectionColor = System.Drawing.Color.Red  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionFont = new Font("Tahoma", 12, FontStyle.Bold);  
    richTextBox1.SelectionColor = System.Drawing.Color.Red;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionFont =  
       gcnew System::Drawing::Font("Tahoma", 12, FontStyle::Bold);  
    richTextBox1->SelectionColor = System::Drawing::Color::Red;  
    ```  
  
    > [!NOTE]
    >  这些属性只影响选定的文本，如果未选定文本，则只影响在当前插入点位置键入的文本。  有关以编程方式选择文本的信息，请参见 [TextBoxBase.Select 方法](frlrfSystemWindowsFormsTextBoxBaseClassSelectTopic)。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)