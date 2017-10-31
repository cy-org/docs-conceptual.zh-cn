---
title: "如何：使用 XAML 定义表 | Microsoft Docs"
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
  - "文档, 使用 XAML 定义表"
  - "表, 使用 XAML 定义"
  - "XAML, 定义表"
ms.assetid: 83f2dc58-437e-4cdc-b5dd-0019810c7a85
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：使用 XAML 定义表
下面的示例演示如何使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义 <xref:System.Windows.Documents.Table>。  此示例表有四列（由 <xref:System.Windows.Documents.TableColumn> 元素表示）和若干行（由 <xref:System.Windows.Documents.TableRow> 元素表示），包含数据以及标题、表头和表尾信息。  行必须包含在 <xref:System.Windows.Documents.TableRowGroup> 元素中。  表中的每一行都是由一个或多个单元格组成（由 <xref:System.Windows.Documents.TableCell> 元素表示）。  表单元格中的内容必须包含在 <xref:System.Windows.Documents.Block> 元素中；在此示例中使用的是 <xref:System.Windows.Documents.Paragraph> 元素。  该表还在页脚行中承载一个超链接（由 <xref:System.Windows.Documents.Hyperlink> 元素表示）。  
  
## 示例  
 [!code-xml[TableSnippetsXAML#_TableXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippetsXAML/CS/Window1.xaml#_tablexaml)]  
  
 下图显示了此示例中定义的表的呈现结果。  
  
 ![呈现的表。](../../../../docs/framework/wpf/advanced/media/tableeg.png "TableEG")