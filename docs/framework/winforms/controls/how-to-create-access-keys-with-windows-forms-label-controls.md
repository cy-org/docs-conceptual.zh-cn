---
title: "如何：使用 Windows 窗体 Label 控件创建访问键 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 访问键"
  - "对话框控件, 助记键"
  - "键盘快捷键, 为控件创建"
  - "Label 控件 [Windows 窗体], 创建访问键"
  - "助记键"
  - "助记键, 添加到对话框控件"
  - "UseMnemonic 属性, Label 控件"
  - "Windows 窗体控件, 访问键"
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 Windows 窗体 Label 控件创建访问键
Windows 窗体 <xref:System.Windows.Forms.Label> 控件可以用来为其他控件定义访问键。  在标签 \(Label\) 控件中定义访问键时，用户可以按 Alt 键和指定字符将焦点移动到 Tab 键顺序中的下一个控件上。  因为标签无法接收焦点，所以焦点自动移动到 Tab 键顺序中的下一个控件上。  使用该技术向文本框、组合框、列表框和数据网格分配访问键。  
  
### 向带标签的控件分配访问键  
  
1.  先绘制标签，然后绘制另一个控件。  
  
     \- 或 \-  
  
     按任意顺序绘制控件，并将该标签的 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性设置为比另一个控件小 1。  
  
2.  将该标签的 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 属性设置为 `true`。  
  
3.  在该标签的 <xref:System.Windows.Forms.Label.Text%2A> 属性中使用“and”符 \(&\) 为该标签分配访问键。  有关更多信息，请参见[创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)。  
  
    > [!NOTE]
    >  您也许希望在标签控件中显示“&”符，而不是使用这些符号创建访问键。  如果将标签 \(Label\) 控件绑定到记录集内的字段而该字段中的数据包含“&”符时，可能会发生这种情况。  若要在标签控件中显示“&”符，请将 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 属性设置为 `false`。  如果希望显示“&”符并且又有访问键，请将 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 属性设置为 `true`，使用一个“and”符 \(&\) 指示该访问键，使用两个“&”符显示“&”符。  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## 请参阅  
 [如何：调整 Windows 窗体标签控件大小以适应其内容](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)   
 [Label 控件概述](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [Label 控件](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)