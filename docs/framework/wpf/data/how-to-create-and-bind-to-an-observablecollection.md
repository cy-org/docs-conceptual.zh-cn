---
title: "如何：创建和绑定到 ObservableCollection | Microsoft Docs"
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
  - "类, ObservableCollection"
  - "Data Binding — 数据绑定, ObservableCollection 类"
  - "通知"
ms.assetid: 6cf7e275-df76-41c6-a611-53b889b8fd5a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：创建和绑定到 ObservableCollection
本主题中的示例演示如何创建和绑定到派生自 <xref:System.Collections.ObjectModel.ObservableCollection%601> 类的集合，该类是一个在添加或移除项时提供通知的集合类。  
  
## 示例  
 下面的示例演示如何实现 `NameList` 集合：  
  
 [!code-csharp[MultiBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[MultiBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MultiBinding/VisualBasic/NameList.vb#1)]  
  
 可以根据[使数据可用于 XAML 中的绑定](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)中的说明，按照与其他[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象相同的方式使集合可用于绑定。  例如，可以在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中实例化该集合，并将该集合指定为一个资源，如下所示：  
  
 [!code-xml[MultiBinding#OCHowTo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#ochowto)]  
[!code-xml[MultiBinding#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources2)]  
  
 然后可以绑定到该集合：  
  
 [!code-xml[MultiBinding#MultiBindingListBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#multibindinglistbox)]  
  
 此处没有显示 `NameItemTemplate` 的定义。  
  
> [!NOTE]
>  集合中的对象必须满足[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)中所述的要求。  特别是，如果您使用 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode>（例如，您希望 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在源属性发生显著变化时进行更新），则必须实现一个适当的“属性已更改”通知机制，如 <xref:System.ComponentModel.INotifyPropertyChanged> 接口。  
  
 有关更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中的“绑定到集合”一节。  
  
## 请参阅  
 [在视图中对数据进行排序](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [在 XAML 中使用视图对数据进行排序和分组](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)