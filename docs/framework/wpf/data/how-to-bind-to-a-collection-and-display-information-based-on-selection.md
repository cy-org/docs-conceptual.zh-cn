---
title: "如何：绑定到集合并基于选择显示信息 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 绑定到集合"
  - "Data Binding — 数据绑定, 创建数据集合的视图"
  - "Data Binding — 数据绑定, 选择视图的数据"
  - "数据集合, 选择视图的数据"
ms.assetid: 952a7d76-dd29-49e5-86f5-32c4530e70eb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：绑定到集合并基于选择显示信息
在一个简单的主\-从方案中，您有一个已绑定数据的 <xref:System.Windows.Controls.ItemsControl>，例如 <xref:System.Windows.Controls.ListBox>。  基于用户的选择显示有关选定项的更多信息。  此示例演示如何实现该方案。  
  
## 示例  
 在此示例中，`People` 是 `Person` 类的一个 <xref:System.Collections.ObjectModel.ObservableCollection%601>。  该 `Person` 类包含三个属性：`FirstName`、`LastName` 和 `HomeTown`，它们的类型均为 `string`。  
  
 [!code-xml[CollectionBinding#Source](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#source)]  
[!code-xml[CollectionBinding#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#ui)]  
  
 <xref:System.Windows.Controls.ContentControl> 使用以下 <xref:System.Windows.DataTemplate>，该模板定义如何显示 `Person` 的信息：  
  
 [!code-xml[CollectionBinding#DetailTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#detailtemplate)]  
  
 以下是该示例生成的内容的一个屏幕快照。  <xref:System.Windows.Controls.ContentControl> 显示所选人员的其他属性。  
  
 ![绑定到集合](../../../../docs/framework/wpf/data/media/databinding-collectionbindingsample.png "DataBinding\_CollectionBindingSample")  
  
 此示例中需要注意的两点是：  
  
1.  <xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.ContentControl> 绑定到同一个源。  两个绑定的 <xref:System.Windows.Data.Binding.Path%2A> 属性均未指定，因为两个控件都绑定到整个集合对象。  
  
2.  为此，必须将 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 属性设置为 `true`。  设置此属性可以确保选定项始终设置为 <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>。  或者，如果 <xref:System.Windows.Controls.ListBox> 从 <xref:System.Windows.Data.CollectionViewSource> 获取数据，则它将自动同步选定内容和当前内容。  
  
 请注意，`Person` 类按以下方式重写 `ToString` 方法。  默认情况下，<xref:System.Windows.Controls.ListBox> 调用 `ToString` 并显示绑定集合中每个对象的字符串表示形式。  因此，每个 `Person` 都显示为 <xref:System.Windows.Controls.ListBox> 中的第一个名称。  
  
 [!code-csharp[CollectionBinding#ToString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Data.cs#tostring)]
 [!code-vb[CollectionBinding#ToString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionBinding/VisualBasic/Person.vb#tostring)]  
  
## 请参阅  
 [对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)   
 [对分层 XML 数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)