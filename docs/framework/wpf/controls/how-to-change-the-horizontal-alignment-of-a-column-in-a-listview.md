---
title: "如何：更改 ListView 中列的水平对齐方式 | Microsoft Docs"
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
  - "ListView 控件, 水平对齐"
ms.assetid: b9573e44-9dad-4d14-939c-7859ca372758
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：更改 ListView 中列的水平对齐方式
默认情况下，<xref:System.Windows.Controls.ListViewItem> 中的每个列的内容都是左对齐的。  通过提供 <xref:System.Windows.DataTemplate>，然后设置 <xref:System.Windows.DataTemplate> 中的元素上的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性，可以更改每个列的对齐方式。  本主题演示默认情况下 <xref:System.Windows.Controls.ListView> 如何对齐其内容，并且演示如何更改 <xref:System.Windows.Controls.ListView> 中某个列的对齐方式。  
  
## 示例  
 在下面的示例中，`Title` 和 `ISBN` 列中的数据左对齐。  
  
 [!code-xml[ListViewHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xml[ListViewHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 若要更改 `ISBN` 列的对齐方式，需要指定每个 <xref:System.Windows.Controls.ListViewItem> 的 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 属性为 <xref:System.Windows.HorizontalAlignment>，这样每个 <xref:System.Windows.Controls.ListViewItem> 中的元素就可以跨越或占据每个列的整个宽度。  由于 <xref:System.Windows.Controls.ListView> 被绑定到数据源，因此需要创建用于设置 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 的样式。  接下来，需要使用 <xref:System.Windows.DataTemplate> 来显示内容，而不是使用 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 属性。  若要显示每个模板的 `ISBN`，<xref:System.Windows.DataTemplate> 只能包含一个将其 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性设置为 <xref:System.Windows.HorizontalAlignment> 的 <xref:System.Windows.Controls.TextBlock>。  
  
 下面的示例定义使 `ISBN` 列右对齐所需的样式和 <xref:System.Windows.DataTemplate>，并更改 <xref:System.Windows.Controls.GridViewColumn> 以引用 <xref:System.Windows.DataTemplate>。  
  
 [!code-xml[ListViewHowTos#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#3)]  
[!code-xml[ListViewHowTos#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#4)]  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)