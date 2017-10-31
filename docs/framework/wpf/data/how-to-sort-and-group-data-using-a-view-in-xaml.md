---
title: "如何：在 XAML 中使用视图对数据进行排序和分组 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 在 XAML 中将视图中的数据分组"
  - "Data Binding — 数据绑定, 在 XAML 中将视图中的数据排序"
  - "在 XAML 中将视图中的数据分组"
  - "在 XAML 中将视图中的数据排序"
  - "视图, 数据分组"
  - "视图, 对数据进行排序"
  - "XAML, 将视图中的数据分组"
  - "XAML, 将视图中的数据排序"
ms.assetid: 145c8c3f-dbdd-4d0d-816f-90b35eba7eda
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 XAML 中使用视图对数据进行排序和分组
此示例演示如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中创建数据集的视图。  使用视图可以进行分组、排序和筛选，并对当前项进行概念性说明。  
  
## 示例  
 在下面的示例中，名为“地点”的静态资源定义为一组地点对象，其中的每个地点对象都由一个城市名称和相应的州\/省\/市\/自治区名称组成。  前缀 *src* 映射到其中定义了数据源*地点* 的命名空间。  前缀 *scm* 映射到 `"clr-namespace:System.ComponentModel;assembly=WindowsBase"`，*dat* 映射到 `"clr-namespace:System.Windows.Data;assembly=PresentationFramework"`。  
  
 下面的示例创建一个数据集合视图，该视图按城市名称进行排序，并按州\/省\/市\/自治区进行分组。  
  
 [!code-xml[CollectionViewSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#1)]  
  
 该视图随后可以成为绑定源，如下面的示例所示：  
  
 [!code-xml[CollectionViewSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#2)]  
  
 如果是绑定到在 <xref:System.Windows.Data.XmlDataProvider> 资源中定义的 XML 数据，请在 XML 名称前加上 @ 符号。  
  
 [!code-xml[CollectionViewSource#XDPChunk](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#xdpchunk)]  
  
 [!code-xml[CollectionViewSource#Attribute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#attribute)]  
  
## 请参阅  
 <xref:System.Windows.Data.CollectionViewSource>   
 [获取数据集合的默认视图](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)