---
title: "如何：对分层数据使用主-从模式 | Microsoft Docs"
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
ms.assetid: 11429b9e-058d-4084-bfb6-2cf209c8ddf7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：对分层数据使用主-从模式
此示例演示如何实现主\/从方案。  
  
## 示例  
 在本示例中，`LeagueList` 是 `Leagues` 的集合。  每个 `League` 都有一个 `Name`，并且具有一个 `Divisions` 集合；每个 `Division` 都具有一个名称和一个 `Teams` 集合。  每个 `Team` 都有一个团队名称。  
  
 [!code-xml[MasterDetail#HowTo1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto1)]  
[!code-xml[MasterDetail#HowTo2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto2)]  
  
 以下是该示例的一个屏幕快照。  `Divisions` <xref:System.Windows.Controls.ListBox> 可自动跟踪 `Leagues` <xref:System.Windows.Controls.ListBox> 中的选定内容并显示相应的数据。  `Teams` <xref:System.Windows.Controls.ListBox> 可跟踪其他两个 <xref:System.Windows.Controls.ListBox> 控件中的选定内容。  
  
 ![主&#45;详细信息示例](../../../../docs/framework/wpf/data/media/databindingmasterdetailsample.png "DataBindingMasterDetailSample")  
  
 此示例中需要注意的两点是：  
  
1.  这三个 <xref:System.Windows.Controls.ListBox> 控件都绑定到同一个源。  设置绑定的 <xref:System.Windows.Data.Binding.Path%2A> 属性以指定您希望 <xref:System.Windows.Controls.ListBox> 显示哪个级别的数据。  
  
2.  必须将您正在跟踪其选定内容的 <xref:System.Windows.Controls.ListBox> 控件上的 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 属性设置为 `true`。  设置此属性可以确保选定项始终设置为 <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>。  或者，如果 <xref:System.Windows.Controls.ListBox> 从 <xref:System.Windows.Data.CollectionViewSource> 获取数据，则它将自动同步选定内容和当前内容。  
  
 如果使用 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据，则方式略有不同。  有关示例，请参见[对分层 XML 数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)。  
  
## 请参阅  
 <xref:System.Windows.HierarchicalDataTemplate>   
 [绑定到集合并基于选择显示信息](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)