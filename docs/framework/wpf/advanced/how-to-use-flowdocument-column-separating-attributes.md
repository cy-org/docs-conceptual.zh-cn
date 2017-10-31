---
title: "如何：使用 FlowDocument 列分隔特性 | Microsoft Docs"
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
  - "列分隔特性"
  - "文档, FlowDocument 列分隔特性"
  - "FlowDocument 列分隔特性"
ms.assetid: c7a822f8-aeca-45bd-a258-2852ff28005c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用 FlowDocument 列分隔特性
此示例演示如何使用 <xref:System.Windows.Documents.FlowDocument> 的列分隔功能。  
  
## 示例  
 下面的示例定义一个 <xref:System.Windows.Documents.FlowDocument>，并设置 <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A> 和 <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> 特性。  <xref:System.Windows.Documents.FlowDocument> 包含一段示例内容。  
  
 [!code-xml[FlowDocumentSnippets#_FlowDocumentColumnStuffXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml#_flowdocumentcolumnstuffxaml)]  
  
 下图显示的是 <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A> 和 <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> 特性在所呈现的 <xref:System.Windows.Documents.FlowDocument> 中的效果。  
  
 ![屏幕快照：FlowDocument Intra 列](../../../../docs/framework/wpf/advanced/media/flowdocumentintracolumn.png "FlowDocumentIntraColumn")