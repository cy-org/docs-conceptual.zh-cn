---
title: "如何：检索文本选定内容 | Microsoft Docs"
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
  - "检索文本"
  - "文本, 检索"
  - "TextBox 控件, 检索文本"
ms.assetid: d5793172-1e11-4a39-9be0-73f336ed858d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：检索文本选定内容
此示例演示一种执行如下操作的方法：使用 <xref:System.Windows.Controls.TextBox.SelectedText%2A> 属性来检索用户已经在 <xref:System.Windows.Controls.TextBox> 控件中选择的文本。  
  
## 示例  
 下面的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例演示 <xref:System.Windows.Controls.TextBox> 控件（包含要选择的部分文本）和 <xref:System.Windows.Controls.Button> 控件（具有指定的 <xref:System.Windows.Controls.Button.OnClick%2A> 方法）的定义。  
  
 在本示例中，具有相关 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序的按钮用来检索文本选定内容。  当用户单击该按钮时，<xref:System.Windows.Controls.Button.OnClick%2A> 方法会将文本框中任何选定的文本复制到字符串中。  可以方便地修改用来检索文本选定内容的具体方法（单击按钮）以及针对该选定内容执行的操作（将文本选定内容复制到字符串），以便使其适应各种不同的情形。  
  
 [!code-xml[TextBox_MiscCode#_TextBoxSelectTextXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxselecttextxaml)]  
  
## 示例  
 下面的 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 示例演示了在上例的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中所定义按钮的 <xref:System.Windows.Controls.Button.OnClick%2A> 事件处理程序。  
  
 [!code-csharp[TextBox_MiscCode#_SelectText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_selecttext)]
 [!code-vb[TextBox_MiscCode#_SelectText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_selecttext)]  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)