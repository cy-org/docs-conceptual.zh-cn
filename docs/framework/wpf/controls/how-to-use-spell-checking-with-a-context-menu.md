---
title: "如何：使用上下文菜单中的拼写检查功能 | Microsoft Docs"
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
  - "在文本框中启用拼写检查 [WPF]"
  - "在文本框中重新启用拼写检查 [WPF]"
  - "上下文菜单中的拼写检查功能 [WPF]"
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：使用上下文菜单中的拼写检查功能
默认情况下，当在类似 <xref:System.Windows.Controls.TextBox> 或 <xref:System.Windows.Controls.RichTextBox> 这样的编辑控件中启用拼写检查功能时，可以在上下文菜单中获得拼写检查选项。  例如，当用户右击一个拼错的单词时，会得到一组拼写建议或**“全部忽略”**选项。  不过，当您用自己的自定义上下文菜单覆盖默认上下文菜单时，将会丢失此功能，而需要编写代码才能在上下文菜单中重新启用拼写检查功能。  下面的示例演示如何在 <xref:System.Windows.Controls.TextBox> 中启用此功能。  
  
## 示例  
 下面的示例演示利用用于实现上下文菜单的某些事件创建 <xref:System.Windows.Controls.TextBox> 的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  
  
 [!code-xml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## 示例  
 下面的示例演示实现上下文菜单的代码。  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 用于在 <xref:System.Windows.Controls.RichTextBox> 中执行上述操作的代码是类似的。  主要区别在于传递给 `GetSpellingError` 方法的参数。  对于 <xref:System.Windows.Controls.TextBox>，传递的是插入符号位置的整数索引：  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 对于 <xref:System.Windows.Controls.RichTextBox>，传递的是指定插入符号位置的 <xref:System.Windows.Documents.TextPointer>：  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [在文本编辑控件中启用拼写检查](../../../../docs/framework/wpf/controls/how-to-enable-spell-checking-in-a-text-editing-control.md)   
 [通过 TextBox 使用自定义上下文菜单](../../../../docs/framework/wpf/controls/how-to-use-a-custom-context-menu-with-a-textbox.md)