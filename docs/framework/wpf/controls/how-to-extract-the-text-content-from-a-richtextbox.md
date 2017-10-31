---
title: "如何：从 RichTextBox 中提取文本内容 | Microsoft Docs"
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
  - "内容, 提取"
  - "提取文本内容"
  - "RichTextBox 控件, 提取文本内容"
  - "文本内容, 提取"
ms.assetid: f13c093f-1a05-45b3-ac8f-c9ea5e4a11c5
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：从 RichTextBox 中提取文本内容
此示例演示如何将一个 <xref:System.Windows.Controls.RichTextBox> 的内容提取为纯文本。  
  
## 示例  
 下面的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 代码介绍一个包含简单内容的、已命名的 <xref:System.Windows.Controls.RichTextBox> 控件。  
  
 [!code-xml[RichTextBoxSnippets#_RTB_XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml#_rtb_xaml)]  
  
## 示例  
 以下代码实现一个将 <xref:System.Windows.Controls.RichTextBox> 作为参数的方法并返回表示一个 <xref:System.Windows.Controls.RichTextBox> 的纯文本内容的字符串。  
  
 该方法从 <xref:System.Windows.Controls.RichTextBox> 的内容创建一个新的 <xref:System.Windows.Documents.TextRange>，并使用 <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> 和 <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> 指示要提取的内容的范围。  <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> 和 <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> 属性均返回一个 <xref:System.Windows.Documents.TextPointer>，并且在表示 <xref:System.Windows.Controls.RichTextBox> 内容的基础 FlowDocument 上可以进行访问。  <xref:System.Windows.Documents.TextRange> 提供一个 Text 属性，将 <xref:System.Windows.Documents.TextRange> 的纯文本部分作为一个字符串返回。  
  
 [!code-csharp[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml.cs#_rtb_stringfrom)]
 [!code-vb[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxSnippets/visualbasic/window1.xaml.vb#_rtb_stringfrom)]  
  
## 请参阅  
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)