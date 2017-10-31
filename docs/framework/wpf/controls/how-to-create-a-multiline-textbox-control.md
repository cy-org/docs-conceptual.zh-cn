---
title: "如何：创建多行 TextBox 控件 | Microsoft Docs"
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
  - "TextBox 控件, 多行文本"
ms.assetid: 05914a93-d0ea-4a9a-b693-09df7d4e2ac2
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：创建多行 TextBox 控件
本示例演示如何使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义一个 <xref:System.Windows.Controls.TextBox> 控件，该控件将自动扩展以容纳多行文本。  
  
## 示例  
 将 <xref:System.Windows.Controls.TextBox.TextWrapping%2A> 特性设置为 **Wrap** 会导致输入的文本在到达 <xref:System.Windows.Controls.TextBox> 控件的边缘时换至新行，必要时会自动扩展 <xref:System.Windows.Controls.TextBox> 控件以便为新行留出空间。  
  
 将 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> 特性设置为 **true** 会导致在按 Return 键时插入新行，必要时会再次自动扩展 <xref:System.Windows.Controls.TextBox> 以便为新行留出空间。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> 特性向 <xref:System.Windows.Controls.TextBox> 添加一个滚动条，以便在 <xref:System.Windows.Controls.TextBox> 超出包含它的框架或窗口的大小时，可以滚动 <xref:System.Windows.Controls.TextBox> 的内容。  
  
 [!code-xml[TextBox_MiscCode#_MultilineTextBoxXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
## 请参阅  
 <xref:System.Windows.TextWrapping>   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)