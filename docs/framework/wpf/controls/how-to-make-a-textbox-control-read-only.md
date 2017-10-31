---
title: "如何：将 TextBox 控件设为只读 | Microsoft Docs"
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
  - "只读 TextBox 控件"
  - "TextBox 控件只读"
ms.assetid: e707ec59-8b22-473e-b77c-3060a237517a
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：将 TextBox 控件设为只读
本主题中的示例演示如何将 <xref:System.Windows.Controls.TextBox> 控件配置为禁止用户输入或修改。  
  
## 示例  
 为了防止用户修改 <xref:System.Windows.Controls.TextBox> 控件的内容，请将 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 特性设置为 **true**。  
  
 [!code-xml[TextBox_MiscCode#_ReadOnlyTextBoxXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_readonlytextboxxaml)]  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 特性仅影响用户输入，而不会影响在 <xref:System.Windows.Controls.TextBox> 控件的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 说明中设置的文本或者通过 <xref:System.Windows.Controls.TextBox.Text%2A> 属性以编程方式设置的文本。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 的默认值为 **false**。  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)