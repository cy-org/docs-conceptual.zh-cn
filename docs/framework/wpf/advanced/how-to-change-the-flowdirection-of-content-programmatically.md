---
title: "如何：以编程方式更改内容的 FlowDirection | Microsoft Docs"
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
  - "文档, 以编程方式更改 FlowDirection 属性"
  - "FlowDirection 属性, 以编程方式更改"
ms.assetid: 02f5a8ba-f8c0-4e5a-84b9-4c5bf12922a2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：以编程方式更改内容的 FlowDirection
此示例演示如何以编程方式更改 <xref:System.Windows.Controls.FlowDocumentReader> 的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性。  
  
## 示例  
 创建两个 <xref:System.Windows.Controls.Button> 元素，其中每个元素均代表 <xref:System.Windows.FlowDirection> 的一个可能值。  当单击某个按钮时，关联的属性值会应用于名为 `tf1` 的 <xref:System.Windows.Controls.FlowDocumentReader> 的内容。  该属性值还会写入名为 `txt1` 的一个 <xref:System.Windows.Controls.TextBlock>。  
  
 [!code-xml[FlowDirectionSnippets#_FlowDirectionXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml#_flowdirectionxaml)]  
  
## 示例  
 与上面定义的按钮单击关联的事件在 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 代码隐藏文件中进行处理。  
  
 [!code-csharp[FlowDirectionSnippets#_FlowDirection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml.cs#_flowdirection)]
 [!code-vb[FlowDirectionSnippets#_FlowDirection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDirectionSnippets/VisualBasic/Window1.xaml.vb#_flowdirection)]