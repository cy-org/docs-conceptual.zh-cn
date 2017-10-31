---
title: "如何：在 Windows 窗体 TextBox 控件中查看多个行 | Microsoft Docs"
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
  - "回车"
  - "CRLF"
  - "行尾"
  - "换行"
  - "TextBox 控件中的 MultiLine 属性"
  - "换行"
  - "ScrollBars 属性, 在 TextBox 控件中"
  - "TextBox 控件 [Windows 窗体], 查看多行"
  - "WordWrap 属性"
ms.assetid: 43173201-0b74-4067-a472-605029ca5f35
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在 Windows 窗体 TextBox 控件中查看多个行
默认情况下，Windows 窗体 <xref:System.Windows.Forms.TextBox> 控件显示单行文本，并且不显示滚动条。  如果文本长度超过了可用的空间，则只有一部分文本可见。  可以通过将 <xref:System.Windows.Forms.TextBox.Multiline%2A> 属性、<xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性和 <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 属性设置为适当的值来更改此默认行为。  
  
### 在 TextBox 控件中显示回车符  
  
-   若要在多行 <xref:System.Windows.Forms.TextBox> 中显示回车符，请使用 <xref:System.Environment.NewLine%2A> 属性。  
  
     请注意，转义符“\\”的解释取决于语言。  Visual Basic 使用 `Chr$(13) & Chr$(10)` 作为回车符和换行符的组合。  
  
### 在 TextBox 控件中查看多行  
  
1.  将 <xref:System.Windows.Forms.TextBox.Multiline%2A> 属性设置为 `true`。  如果 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 为 `true`（默认值），则控件中的文本将显示为一个或多个段落；否则它将显示为一个列表，其中的某些行可能在控件边缘处被剪裁。  
  
2.  将 <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 属性设置为适当的值。  
  
    |值|说明|  
    |-------|--------|  
    |<xref:System.Windows.Forms.ScrollBars>|如果文本是一个几乎总能适合控件的段落，就使用此值。  如果文本太长，不能同时显示全部内容，用户可以使用鼠标指针在控件内来回移动。|  
    |<xref:System.Windows.Forms.ScrollBars>|如果要显示行列表，则使用此值；其中某些行的长度可能大于 <xref:System.Windows.Forms.TextBox> 控件的宽度。|  
    |<xref:System.Windows.Forms.ScrollBars>|如果列表的长度可能大于控件的高度，则使用此值。|  
  
3.  将 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为适当的值。  
  
    |值|说明|  
    |-------|--------|  
    |`false`|控件中的文本不会自动换行，所以将一直向右延伸到换行符为止。  如果选择了上面的 <xref:System.Windows.Forms.ScrollBars> 滚动条或 <xref:System.Windows.Forms.ScrollBars>，则使用此值。|  
    |`true`（默认值）|不会出现水平滚动条。  如果选择了上面的 <xref:System.Windows.Forms.ScrollBars> 滚动条或 <xref:System.Windows.Forms.ScrollBars>，则使用此值来显示一个或多个段落。|  
  
## 请参阅  
 <xref:System.Windows.Forms.TextBox>   
 [TextBox 控件概述](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [如何：控制 Windows 窗体 TextBox 控件中的插入点](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [如何：创建只读文本框](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [如何：在字符串中放置引号](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [如何：在 Windows 窗体 TextBox 控件中选择文本](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)