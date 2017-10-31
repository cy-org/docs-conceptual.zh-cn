---
title: "如何：在视图中对数据进行排序 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 将视图中的数据分组"
  - "Data Binding — 数据绑定, 将视图中的数据排序"
  - "将视图中的数据分组"
  - "将视图中的数据排序"
  - "视图, 数据分组"
  - "视图, 对数据进行排序"
ms.assetid: f4c43578-01b7-4774-a953-acb95a13b94a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：在视图中对数据进行排序
此示例介绍如何在视图中对数据进行排序。  
  
## 示例  
 下面的示例创建一个简单的 <xref:System.Windows.Controls.ListBox> 和一个 <xref:System.Windows.Controls.Button>：  
  
 [!code-xml[ListBoxSort_snip#HowTo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml#howto)]  
  
 按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序包含按降序顺序对 <xref:System.Windows.Controls.ListBox> 中的项进行排序的逻辑。  之所以可以这样做是因为：按此方式向 <xref:System.Windows.Controls.ListBox> 添加项时，会将这些项添加至 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemCollection>，并且 <xref:System.Windows.Controls.ItemCollection> 是从 <xref:System.Windows.Data.CollectionView> 类派生的。  如果正在使用 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性将 <xref:System.Windows.Controls.ListBox> 绑定到集合，则可以使用同样的技术进行排序。  
  
 [!code-csharp[ListBoxSort_snip#HowToCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml.cs#howtocode)]
 [!code-vb[ListBoxSort_snip#HowToCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxSort_snip/visualbasic/window1.xaml.vb#howtocode)]  
  
 只要具有对视图对象的引用，就可以使用同样的技术对其他集合视图的内容进行排序。  有关如何获取视图的示例，请参见[获取数据集合的默认视图](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)。  若要查看其他示例，请参见[在单击标题时对 GridView 列进行排序](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)。  有关视图的更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中的“绑定到集合”。  
  
 有关如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中应用排序逻辑的示例，请参见[在 XAML 中使用视图对数据进行排序和分组](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)。  
  
## 请参阅  
 <xref:System.Windows.Data.ListCollectionView.CustomSort%2A>   
 [在单击标题时对 GridView 列进行排序](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)