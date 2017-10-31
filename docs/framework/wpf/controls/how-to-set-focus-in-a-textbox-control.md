---
title: "如何：设置 TextBox 控件中的焦点 | Microsoft Docs"
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
  - "焦点, 设置"
  - "TextBox 控件, 设置焦点"
ms.assetid: 24b61b45-dc2d-425e-9839-b017af7ab86f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：设置 TextBox 控件中的焦点
此示例演示如何使用 <xref:System.Windows.UIElement.Focus%2A> 方法在 <xref:System.Windows.Controls.TextBox> 控件上设置焦点。  
  
## 示例  
 下面的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例介绍了一个简单的 <xref:System.Windows.Controls.TextBox> 控件，名为 *tbFocusMe*。  
  
 [!code-xml[TextBox_MiscCode#_TextBoxFocusXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxfocusxaml)]  
  
## 示例  
 下面的示例调用 <xref:System.Windows.UIElement.Focus%2A> 方法，在名为 *tbFocusMe* 的 <xref:System.Windows.Controls.TextBox> 控件上设置焦点。  
  
 [!code-csharp[TextBox_MiscCode#_FocusTextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_focustextbox)]
 [!code-vb[TextBox_MiscCode#_FocusTextBox](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_focustextbox)]  
  
## 请参阅  
 <xref:System.Windows.UIElement.Focusable%2A>   
 <xref:System.Windows.UIElement.IsFocused%2A>   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)