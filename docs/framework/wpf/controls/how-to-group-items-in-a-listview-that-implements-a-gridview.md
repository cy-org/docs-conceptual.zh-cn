---
title: "如何：对实现 GridView 的 ListView 中的项进行分组 | Microsoft Docs"
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
  - "GridView 控件, 分组项"
  - "在实现 GridViews 的 ListViews 中对项分组"
  - "ListView 控件, 使用 GridViews 对项分组"
ms.assetid: eebef25b-ddc6-424e-a66d-ea228d1bf33d
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：对实现 GridView 的 ListView 中的项进行分组
此示例演示如何在 <xref:System.Windows.Controls.ListView> 控件的 <xref:System.Windows.Controls.GridView> 视图模式下显示项目组。  
  
## 示例  
 若要在 <xref:System.Windows.Controls.ListView> 中显示项目组，请定义 <xref:System.Windows.Data.CollectionViewSource>。  下面的示例演示了一个按 `Catalog` 数据字段值对数据项进行分组的 <xref:System.Windows.Data.CollectionViewSource>。  
  
 [!code-xml[GridViewWithGroups#GroupingCollectionViewSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#groupingcollectionviewsource)]  
  
 下面的示例将 <xref:System.Windows.Controls.ListView> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 设置为前一个示例所定义的 <xref:System.Windows.Data.CollectionViewSource>。  此示例还定义了实现 <xref:System.Windows.Controls.Expander> 控件的 <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A>。  
  
 [!code-xml[GridViewWithGroups#ListViewGroups](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewgroups)]  
[!code-xml[GridViewWithGroups#ListViewEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewend)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)