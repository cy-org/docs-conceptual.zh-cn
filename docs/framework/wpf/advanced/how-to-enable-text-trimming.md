---
title: "如何：启用文本修整 | Microsoft Docs"
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
  - "文档, 剪裁文本"
  - "文本, 剪裁"
  - "剪裁文本"
ms.assetid: dd8c9191-d2be-45fd-9fb4-3c75b65578c5
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：启用文本修整
此示例演示 <xref:System.Windows.TextTrimming> 枚举中可用值的用法和效果。  
  
## 示例  
 下面的示例定义一个设置了 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 特性的 <xref:System.Windows.Controls.TextBlock> 元素。  
  
 [!code-xml[TextTrimmingSnippets#_TextTrimmingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml#_texttrimmingxaml)]  
  
## 示例  
 下面演示如何在代码中设置相应的 <xref:System.Windows.TextTrimming> 属性。  
  
 [!code-csharp[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml.cs#_texttrimmingsettexttrimming)]
 [!code-vb[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextTrimmingSnippets/VisualBasic/Window1.xaml.vb#_texttrimmingsettexttrimming)]  
  
 当前有三个文本修整选项：**CharacterEllipsis**、**WordEllipsis** 和 **None**。  
  
 如果将 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 设置为 **CharacterEllipsis**，则会对文本进行修整，并在最靠近修整边缘的字符处使用省略号填充。  此设置旨在修整文本以更靠近修整边界，但这样会导致单词不完整。  下图演示此设置在类似于上述代码定义的 <xref:System.Windows.Controls.TextBlock> 中的效果。  
  
 ![示例：TextTrimming.CharacterEllipsis](../../../../docs/framework/wpf/advanced/media/texttrimming-character.png "TextTrimming\_Character")  
  
 如果将 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 设置为 **WordEllipsis**，则将修整文本，并在最靠近修整边缘的第一个完整的单词结尾处使用省略号填充。  此设置不会显示经过修整之后不完整的单词，但是修整文本时不会像 **CharacterEllipsis** 设置一样靠近修整边缘。  下图演示此设置在上述代码定义的 <xref:System.Windows.Controls.TextBlock> 中的效果。  
  
 ![示例：TextTrimming.WordEllipsis](../../../../docs/framework/wpf/advanced/media/texttrimming-word.png "TextTrimming\_Word")  
  
 如果将 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 设置为 **None**，则不执行文本修整。  在此情况下，只是将文本裁切到父文本容器的边界处。  下图演示此设置在类似于上述代码定义的 <xref:System.Windows.Controls.TextBlock> 中的效果。  
  
 ![示例：TextTrimming.None](../../../../docs/framework/wpf/advanced/media/texttrimming-none.png "TextTrimming\_None")