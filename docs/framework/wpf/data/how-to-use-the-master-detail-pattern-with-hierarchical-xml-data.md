---
title: "如何：对分层 XML 数据使用主-从模式 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 主/从数据范例"
  - "主/从数据范例"
ms.assetid: eb8dbdd8-5871-42bb-a16b-04e655fea677
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：对分层 XML 数据使用主-从模式
此示例演示如何实现具有 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据的主\-从方案。  
  
## 示例  
 此示例是[对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)中所讨论示例的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据版本。  此示例中的数据源自 `League.xml` 文件。  请注意第三个 <xref:System.Windows.Controls.ListBox> 控件如何通过绑定到第二个 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> 属性来跟踪第二个控件中的选项更改。  
  
 [!code-xml[MasterDetailXml#HowTo1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto1)]  
[!code-xml[MasterDetailXml#HowTo2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto2)]  
  
## 请参阅  
 <xref:System.Windows.HierarchicalDataTemplate>   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)