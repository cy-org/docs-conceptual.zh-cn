---
title: "如何：设置 TextBox 控件的文本内容 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "文本内容, 设置"
  - "TextBox 控件, 设置文本内容"
ms.assetid: bcd25fc7-a52f-4453-b802-2c8d2b335ab8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：设置 TextBox 控件的文本内容
本示例演示如何使用 <xref:System.Windows.Controls.TextBox.Text%2A> 属性设置 <xref:System.Windows.Controls.TextBox> 控件的初始文本内容。  
  
 **注意** 尽管示例的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 版本可以在每个按钮的 <xref:System.Windows.Controls.TextBox> 内容的两旁使用 `<TextBox.Text>` 标记，但这不是必需的，因为 <xref:System.Windows.Controls.TextBox> 会将 <xref:System.Windows.Markup.ContentPropertyAttribute> 特性应用于 <xref:System.Windows.Controls.TextBox.Text%2A> 属性。  有关更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
## 示例  
 [!code-xml[TextBox_MiscCode#_TextBoxSetTextXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxsettextxaml)]  
  
## 示例  
 [!code-csharp[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textboxsettext)]
 [!code-vb[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textboxsettext)]  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)