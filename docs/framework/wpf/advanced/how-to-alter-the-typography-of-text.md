---
title: "如何：修改文本的版式 | Microsoft Docs"
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
  - "设置版式特性"
  - "版式特性, 设置"
ms.assetid: 19a3b49b-60a2-4c11-a786-e26b4c965588
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# 如何：修改文本的版式
下面的示例演示如何设置 <xref:System.Windows.Documents.TextElement.Typography%2A> 特性，其中使用 <xref:System.Windows.Documents.Paragraph> 作为示例元素。  
  
## 示例  
 [!code-xml[TextElementSnippets#_TextElement_TypogXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：改变版式的文本](../../../../docs/framework/wpf/advanced/media/textelement-typog.png "TextElement\_Typog")  
  
 作为对比，下图显示了一个具有默认版式属性的类似示例的呈现效果。  
  
 ![屏幕快照：改变版式的文本](../../../../docs/framework/wpf/advanced/media/textelement-typog-default.png "TextElement\_Typog\_Default")  
  
## 示例  
 下面的示例演示如何以编程方式设置 <xref:System.Windows.Controls.TextBox.Typography%2A> 属性。  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
## 请参阅  
 [流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)