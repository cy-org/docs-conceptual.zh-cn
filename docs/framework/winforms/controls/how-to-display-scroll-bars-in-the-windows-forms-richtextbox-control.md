---
title: "如何：在 Windows 窗体 RichTextBox 控件中显示滚动条 | Microsoft Docs"
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
  - "RichTextBox 控件 [Windows 窗体], 显示滚动条"
  - "滚动条, 在控件中显示"
  - "文本框, 显示滚动条"
ms.assetid: cdeb42e1-86e8-410c-ba46-18aec264ef5f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 Windows 窗体 RichTextBox 控件中显示滚动条
默认情况下，Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件在必要时会显示水平和垂直滚动条。  <xref:System.Windows.Forms.RichTextBox> 控件的 <xref:System.Windows.Forms.RichTextBox.ScrollBars%2A> 属性有七个可能的值，在下面的表中对这些值进行了说明。  
  
### 在 RichTextBox 控件中显示滚动条  
  
1.  将 <xref:System.Windows.Forms.RichTextBox.Multiline%2A> 属性设置为 `true`。  如果 <xref:System.Windows.Forms.RichTextBox.Multiline%2A> 属性设置为 `false`，则不显示任何类型的滚动条，包括水平滚动条。  
  
2.  将 <xref:System.Windows.Forms.RichTextBox.ScrollBars%2A> 属性设置为 <xref:System.Windows.Forms.RichTextBoxScrollBars> 枚举的适当值。  
  
    |值|说明|  
    |-------|--------|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>（默认值）|只有当文本超过控件的宽度或长度时，才显示水平滚动条或垂直滚动条，或两个滚动条都显示。|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|从不显示任何类型的滚动条。|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|只有当文本超过控件的宽度时，才显示水平滚动条。  （必须将 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为 `false`，才会出现这种情况。）|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|只有当文本超过控件的高度时，才显示垂直滚动条。|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|当 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为 `false` 时，显示水平滚动条。  在文本未超过控件的宽度时，该滚动条显示为浅灰色。|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|始终显示垂直滚动条。  在文本未超过控件的长度时，该滚动条显示为浅灰色。|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|始终显示垂直滚动条。  当 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为 `false` 时，显示水平滚动条。  在文本未超过控件的宽度或长度时，两个滚动条均显示为灰色。|  
  
3.  将 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为适当的值。  
  
    |值|说明|  
    |-------|--------|  
    |`false`|控件中的文本不会自动调整来适应控件的宽度，所以，该文本可一直向右滚动，直到到达换行符为止。  如果选择了上面的“Horizontal”（水平）滚动条或“Both”（两者），则使用此值。|  
    |`true`（默认值）|控件中的文本将自动调整来适应控件的宽度。  不会出现水平滚动条。  如果选择了上面的“Vertical”（垂直）滚动条或“None”（无）以显示一个或多个段落，则使用此值。|  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBoxScrollBars>   
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)