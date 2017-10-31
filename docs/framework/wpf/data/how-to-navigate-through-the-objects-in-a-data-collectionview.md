---
title: "如何：在数据集合视图中的对象之间导航 | Microsoft Docs"
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
  - "CollectionView, 在对象中导航"
  - "Data Binding — 数据绑定, 在数据 CollectionView 的对象中导航"
  - "在数据 CollectionView 的对象中导航"
ms.assetid: fcd37590-bce1-4ac9-8b74-3b96c7458b8a
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：在数据集合视图中的对象之间导航
使用视图可以用不同的方式（包括排序、筛选或分组）查看同一数据集合。  此外，视图还提供了当前记录指针概念，并可移动该指针。  本示例演示如何获取当前对象，以及如何使用 <xref:System.Windows.Data.CollectionView> 类所提供的功能在数据集合中的对象之间导航。  
  
## 示例  
 在本示例中，`myCollectionView` 为 <xref:System.Windows.Data.CollectionView> 对象，该对象是建立在绑定集合上的视图。  
  
 在下面的示例中，`OnButton` 是应用程序中 `Previous` 和 `Next` 按钮的事件处理程序，用户可以使用这两个按钮导航数据集合。  请注意，<xref:System.Windows.Data.CollectionView.IsCurrentBeforeFirst%2A> 和 <xref:System.Windows.Data.CollectionView.IsCurrentAfterLast%2A> 属性可分别报告当前记录指针是否到达列表的开头和结尾，以便相应地调用 <xref:System.Windows.Data.CollectionView.MoveCurrentToFirst%2A> 和 <xref:System.Windows.Data.CollectionView.MoveCurrentToLast%2A>。  
  
 该视图的 <xref:System.Windows.Data.CollectionView.CurrentItem%2A> 属性会强制转换为 `Order`，以返回该集合中的当前顺序项。  
  
 [!code-csharp[CollectionView#OnButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#onbutton)]
 [!code-vb[CollectionView#OnButton](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#onbutton)]  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [在视图中对数据进行排序](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [在 XAML 中使用视图对数据进行排序和分组](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)