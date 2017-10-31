---
title: "如何：绑定到 LINQ 查询的结果 | Microsoft Docs"
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
  - "绑定到 LINQ 查询结果 [WPF]"
  - "运行 LINQ 查询 [WPF], 绑定到结果"
ms.assetid: ff2844d9-17ed-4ea6-aab1-5111af0bc684
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：绑定到 LINQ 查询的结果
本示例演示如何运行 LINQ 查询然后绑定到查询结果。  
  
## 示例  
 下面的示例创建两个列表框。  第一个列表框包含三个列表项。  
  
 [!code-xml[LinqExample#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml#ui)]  
  
 在第一个列表框中选择一项会激发下面的事件处理程序。  在本示例中，`Tasks` 是 `Task` 对象的集合。  `Task` 类具有名为 `Priority` 的属性。  此事件处理程序运行一个 LINQ 查询，该查询返回具有选定优先级值的 `Task` 对象的集合，然后将其设置为 <xref:System.Windows.FrameworkElement.DataContext%2A>：  
  
 [!code-csharp[LinqExample#Using](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#using)]  
[!code-csharp[LinqExample#Tasks](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#tasks)]  
[!code-csharp[LinqExample#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#handler)]  
  
 第二个列表框绑定到该集合，因为该列表框的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 值设置为 `{Binding}`。  因此，该列表框显示返回的集合（基于 `myTaskTemplate` <xref:System.Windows.DataTemplate>）。  
  
## 请参阅  
 [使数据可用于 XAML 中的绑定](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)   
 [绑定到集合并基于选择显示信息](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)   
 [WPF 版本 4.5 的新增功能](../../../../docs/framework/wpf/getting-started/whats-new.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)