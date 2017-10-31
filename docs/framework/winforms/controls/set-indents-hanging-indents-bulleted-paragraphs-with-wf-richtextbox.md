---
title: "如何：在 Windows 窗体 RichTextBox 控件中设置缩进、悬挂缩进和带项目符号的段落 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 文本框"
  - "RichTextBox 控件 [Windows 窗体], 设置缩进和项目符号"
  - "RTF 文件, 在 RichTextBox 控件中设置格式"
  - "文本框, 项目符号"
  - "文本框, 设置缩进"
ms.assetid: abfb40e6-5642-4691-8ec1-9d9ae91688dc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Windows 窗体 RichTextBox 控件中设置缩进、悬挂缩进和带项目符号的段落
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件具有多个用于设置所显示的文本的格式的选项。  可以通过设置 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 属性将选定的段落设置为项目符号列表的格式。  也可以使用 <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A>、<xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A> 和 <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> 属性设置段落相对于控件的左右边缘以及其他文本行的左边缘进行缩进。  
  
### 将段落设置为项目符号列表格式  
  
1.  将 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 属性设置为 `true`。  
  
    ```vb  
    RichTextBox1.SelectionBullet = True  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionBullet = true;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionBullet = true;  
    ```  
  
### 缩进段落  
  
1.  将 <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A> 属性设置为一个整数，该整数表示控件的左边缘和文本的左边缘之间的距离（以像素为单位）。  
  
2.  将 <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> 属性设置为一个整数，该整数表示段落中第一行文本的左边缘与同一段落中后面的行的左边缘之间的距离（以像素为单位）。  <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> 属性的值只适用于段落换行后第一行下面的行。  
  
3.  将 <xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A> 属性设置为一个整数，该整数表示控件的右边缘与文本的右边缘之间的距离（以像素为单位）。  
  
    ```vb  
    RichTextBox1.SelectionIndent = 8  
    RichTextBox1.SelectionHangingIndent = 3  
    RichTextBox1.SelectionRightIndent = 12  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionIndent = 8;  
    richTextBox1.SelectionHangingIndent = 3;  
    richTextBox1.SelectionRightIndent = 12;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionIndent = 8;  
    richTextBox1->SelectionHangingIndent = 3;  
    richTextBox1->SelectionRightIndent = 12;  
    ```  
  
    > [!NOTE]
    >  所有上述属性均会影响包含选定文本的所有段落，还会影响在当前插入点之后键入的文本。  例如，当用户在段落中选择一个词然后调整缩进时，则新设置将应用于包含这个词的整个段落，还会应用于在选定的段落之后输入的任何段落。  有关以编程方式选择文本的更多信息，请参见 [TextBoxBase.Select 方法](frlrfSystemWindowsFormsTextBoxBaseClassSelectTopic)。  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)