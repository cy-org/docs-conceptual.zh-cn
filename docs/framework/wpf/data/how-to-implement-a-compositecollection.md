---
title: "如何：实现 CompositeCollection | Microsoft Docs"
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
  - "类, CompositeCollection"
  - "Data Binding — 数据绑定, CompositeCollection 类"
ms.assetid: 0d8fc84c-7920-427f-8ad7-d55ca656c170
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：实现 CompositeCollection
## 示例  
 下面的示例演示如何使用 <xref:System.Windows.Data.CompositeCollection> 类以一个列表的形式显示多个集合和项。  在此示例中，`GreekGods` 是 `GreekGod` 自定义对象的 <xref:System.Collections.ObjectModel.ObservableCollection%601>。  对数据模板进行了定义，使 `GreekGod` 对象和 `GreekHero` 对象的前景色可分别显示为金色和青色。  
  
 [!code-xml[CompositeCollections#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositeCollections/CS/Window1.xaml#1)]  
  
## 请参阅  
 <xref:System.Windows.Data.CollectionContainer>   
 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>   
 <xref:System.Windows.Data.XmlDataProvider>   
 <xref:System.Windows.DataTemplate>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)