---
title: "如何：筛选视图中的数据 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 在视图中筛选数据"
  - "在视图中筛选数据"
  - "视图, 筛选数据"
ms.assetid: c76e8606-4cc4-45a8-9110-e2ec66dc6afd
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：筛选视图中的数据
此示例演示如何筛选视图中的数据。  
  
## 示例  
 若要创建一个筛选器，请定义一种用来提供筛选逻辑的方法。  该方法用作回调并接受类型为 `object` 的参数。  下面的方法返回 `filled` 属性设置为“No”（否）的所有 `Order` 对象，并筛选掉其余对象。  
  
 [!code-csharp[SortFilter#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#2)]
 [!code-vb[SortFilter#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#2)]  
  
 然后，您可以应用筛选器，如下例所示。  在本示例中，`myCollectionView` 是一个 <xref:System.Windows.Data.ListCollectionView> 对象。  
  
 [!code-csharp[SortFilter#Filter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#filter)]
 [!code-vb[SortFilter#Filter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#filter)]  
  
 若要撤消筛选，可以将 <xref:System.Windows.Data.CollectionView.Filter%2A> 属性设置为 `null`：  
  
 [!code-csharp[SortFilter#Unfilter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#unfilter)]
 [!code-vb[SortFilter#Unfilter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#unfilter)]  
  
 有关如何创建或获取视图的信息，请参见[获取数据集合的默认视图](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)。  有关完整示例，请参见 [Sorting and Filtering Items in a View Sample](http://go.microsoft.com/fwlink/?LinkID=160040)（对视图中的项进行排序和筛选示例）。  
  
 如果您的视图对象来自 <xref:System.Windows.Data.CollectionViewSource> 对象，则可以通过为 <xref:System.Windows.Data.CollectionViewSource.Filter> 事件设置事件处理程序来应用筛选逻辑。  在下面的示例中，`listingDataView` 是 <xref:System.Windows.Data.CollectionViewSource> 的一个实例。  
  
 [!code-csharp[DataBindingLab#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 下面将演示示例 `ShowOnlyBargainsFilter` 筛选事件处理程序的实现。  此事件处理程序使用 <xref:System.Windows.Data.FilterEventArgs.Accepted%2A> 属性筛选掉 `CurrentPrice` 为 25 美元或更高金额的 `AuctionItem` 对象。  
  
 [!code-csharp[DataBindingLab#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
## 请参阅  
 <xref:System.Windows.Data.CollectionView.CanFilter%2A>   
 <xref:System.Windows.Data.BindingListCollectionView.CustomFilter%2A>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [在视图中对数据进行排序](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)