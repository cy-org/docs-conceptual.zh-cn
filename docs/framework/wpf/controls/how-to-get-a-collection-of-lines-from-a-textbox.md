---
title: "如何：从 TextBox 获取线条集合 | Microsoft Docs"
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
  - "文本行, 获取集合"
  - "TextBox 控件, 获取文本行的集合"
ms.assetid: a12f529d-b926-47f6-92bf-cad5f17b532a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：从 TextBox 获取线条集合
此示例演示如何从 <xref:System.Windows.Controls.TextBox> 获取文本行集合。  
  
## 示例  
 下面的示例演示一种简单的方法，该方法采用 <xref:System.Windows.Controls.TextBox> 作为参数，并返回包含 **TextBox** 中的文本行的 <xref:System.Collections.Specialized.StringCollection>。  使用 <xref:System.Windows.Controls.TextBox.LineCount%2A> 属性来确定当前 **TextBox** 中的行数，然后使用 <xref:System.Windows.Controls.TextBox.GetLineText%2A> 方法来提取每行并将它添加到行集合中。  
  
 [!code-csharp[TextBox_MiscCode#_TextBox_GetLines](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textbox_getlines)]  
  
## 请参阅  
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)