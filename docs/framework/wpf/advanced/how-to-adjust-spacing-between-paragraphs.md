---
title: "如何：调整段落间的间距 | Microsoft Docs"
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
  - "文档, 调整段落间的间距"
  - "段, 间距"
  - "段落间的间距"
ms.assetid: 7cd2f2ac-0e19-4587-bfb6-7f5b18c9536e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：调整段落间的间距
此示例演示如何调整或消除流内容中段落之间的间距。  
  
 在流内容中，显示在段落之间的额外空间是由于在这些段落上设置的边距所造成的；因此，可以通过调整这些段落上的边距来控制段落之间的间距。  若要完全消除两个段落之间的额外间距，请将段落的边距设置为 **0**。  若要在整个 <xref:System.Windows.Documents.FlowDocument> 内实现段落之间的统一间距，请使用样式来为 <xref:System.Windows.Documents.FlowDocument> 中的所有段落设置统一的边距值。  
  
 应该注意的是，两个相邻段落之间的边距将“折算”成两个边距值中较大的一个，而不是将两值相加。  因此，如果两个相邻段落的边距分别为 20 像素和 40 像素，那么两个段落之间的最终间距为 40 像素，即两个边距值中较大的一个。  
  
## 示例  
 下面的示例使用样式将 <xref:System.Windows.Documents.FlowDocument> 中的所有 <xref:System.Windows.Documents.Paragraph> 元素的边距设置为 **0**，这将有效地消除 <xref:System.Windows.Documents.FlowDocument> 中段落之间的额外间距。  
  
 [!code-xml[BlockSnippets#_ParagraphSpacingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BlockSnippets/CSharp/Window1.xaml#_paragraphspacingxaml)]