---
title: "如何：通过 Inlines 属性操作流内容元素 | Microsoft Docs"
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
  - "文档, 通过 Inlines 属性操作流内容元素"
  - "流内容元素, 通过 Inlines 属性操作"
  - "Inlines 属性, 操作流内容元素"
  - "属性, Inlines, 操作流内容元素"
ms.assetid: 510780d2-3da1-4360-8763-7054bda22ea3
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：通过 Inlines 属性操作流内容元素
这些示例演示可通过 **Inlines** 属性在内联流内容元素（以及这些元素的容器，例如 <xref:System.Windows.Controls.TextBlock>）上执行的一些常见操作。  此属性用于从 <xref:System.Windows.Documents.InlineCollection> 添加和移除项。  具有 **Inlines** 属性的流内容元素包括：  
  
-   <xref:System.Windows.Documents.Bold>  
  
-   <xref:System.Windows.Documents.Hyperlink>  
  
-   <xref:System.Windows.Documents.Italic>  
  
-   <xref:System.Windows.Documents.Paragraph>  
  
-   <xref:System.Windows.Documents.Span>  
  
-   <xref:System.Windows.Documents.Underline>  
  
 这些示例只是将 <xref:System.Windows.Documents.Span> 用作流内容元素，但是这些技术可应用于承载 <xref:System.Windows.Documents.InlineCollection> 集合的所有元素或控件。  
  
## 示例  
 下面的示例创建一个新 <xref:System.Windows.Documents.Span> 对象，然后使用 **Add** 方法添加两个文本运行，作为 <xref:System.Windows.Documents.Span> 的子内容。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
## 示例  
 下面的示例创建一个新 <xref:System.Windows.Documents.Run> 元素并将其插入到 <xref:System.Windows.Documents.Span> 的开始位置。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
## 示例  
 下面的示例获取包含在 <xref:System.Windows.Documents.Span> 中的顶级 <xref:System.Windows.Documents.Inline> 元素的数目。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesCount](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinescount)]
 [!code-vb[SpanSnippets#_SpanInlinesCount](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinescount)]  
  
## 示例  
 下面的示例删除 <xref:System.Windows.Documents.Span> 中的最后一个 <xref:System.Windows.Documents.Inline> 元素。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
## 示例  
 下面的示例从 <xref:System.Windows.Documents.Span> 中清除所有内容（<xref:System.Windows.Documents.Inline> 元素）。  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
## 请参阅  
 <xref:System.Windows.Documents.BlockCollection>   
 <xref:System.Windows.Documents.InlineCollection>   
 <xref:System.Windows.Documents.ListItemCollection>   
 [流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [通过 Blocks 属性操作 FlowDocument](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [通过 Columns 属性操作表列](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-columns-through-the-columns-property.md)   
 [通过 RowGroups 属性操作表的行组](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)