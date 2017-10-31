---
title: "如何：获取数据集合的默认视图 | Microsoft Docs"
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
  - "创建, 数据集合的视图"
  - "Data Binding — 数据绑定, 创建数据集合的视图"
  - "数据集合, 创建视图"
ms.assetid: b641e96c-c2f6-42ea-9c5d-bac81176ad65
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：获取数据集合的默认视图
使用视图可以用不同的方式查看同一数据集合，具体的方式取决于排序、筛选或分组条件。  每个集合都有一个共享的默认视图，此视图在绑定指定集合作为其源时用作实际的绑定源。  本示例说明了如何获取集合的默认视图。  
  
## 示例  
 若要创建视图，需要对相应集合的对象引用。  通过以下方法可以获取此数据对象：引用您自己的代码隐藏对象、获取数据上下文、获取数据源的属性或者获取绑定的属性。  本示例说明了如何获取数据对象的 <xref:System.Windows.FrameworkElement.DataContext%2A> 并使用它直接获得此集合的默认集合视图。  
  
 [!code-csharp[CollectionView#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#2)]
 [!code-vb[CollectionView#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#2)]  
  
 在本示例中，根元素是一个 <xref:System.Windows.Controls.StackPanel>。  <xref:System.Windows.FrameworkElement.DataContext%2A> 设置为引用数据提供程序的 *myDataSource*，该数据提供程序是 *Order* 对象的 <xref:System.Collections.ObjectModel.ObservableCollection%601>。  
  
 [!code-xml[CollectionView#CollectionViewDataContext](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml#collectionviewdatacontext)]  
  
 另外，您也可以使用 <xref:System.Windows.Data.CollectionViewSource> 类实例化并绑定到您自己的集合视图。  此集合视图仅由直接绑定到它的控件共享。  有关示例，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中的“如何创建视图”部分。  
  
 有关集合视图提供的功能的示例，请参见[在视图中对数据进行排序](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)、[筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)和[在数据集合视图中的对象之间导航](../../../../docs/framework/wpf/data/how-to-navigate-through-the-objects-in-a-data-collectionview.md)。  
  
## 请参阅  
 [在 XAML 中使用视图对数据进行排序和分组](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)