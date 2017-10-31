---
title: "如何：处理 ListView 中每一项的 MouseDoubleClick 事件 | Microsoft Docs"
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
  - "ListView 控件, MouseDoubleClick 事件"
ms.assetid: 81b39369-655a-4585-ac58-4640e5bb8fed
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：处理 ListView 中每一项的 MouseDoubleClick 事件
若要处理 <xref:System.Windows.Controls.ListView> 中的项的事件，需要向每个 <xref:System.Windows.Controls.ListViewItem> 添加一个事件处理程序。  当 <xref:System.Windows.Controls.ListView> 绑定到数据源时，不需要显式创建一个 <xref:System.Windows.Controls.ListViewItem>，但可以通过向 <xref:System.Windows.Controls.ListViewItem> 的样式添加一个 <xref:System.Windows.EventSetter> 来处理每一项的事件。  
  
## 示例  
 下面的示例创建一个进行了数据绑定的 <xref:System.Windows.Controls.ListView>，并创建一个 <xref:System.Windows.Style> 以便向每个 <xref:System.Windows.Controls.ListViewItem> 添加事件处理程序。  
  
 [!code-xml[ListViewHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xml[ListViewHowTos#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#5)]  
[!code-xml[ListViewHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 下面的示例处理 <xref:System.Windows.Controls.Control.MouseDoubleClick> 事件。  
  
 [!code-csharp[ListViewHowTos#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml.cs#6)]
 [!code-vb[ListViewHowTos#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewHowTos/VisualBasic/Window1.xaml.vb#6)]  
  
> [!NOTE]
>  虽然将 <xref:System.Windows.Controls.ListView> 绑定到数据源是一种非常常见的做法，但可以使用样式向未进行数据绑定的 <xref:System.Windows.Controls.ListView> 中的每个 <xref:System.Windows.Controls.ListViewItem> 添加事件处理程序，而无论是否显式创建了 <xref:System.Windows.Controls.ListViewItem>。  有关显式和隐式创建的 <xref:System.Windows.Controls.ListViewItem> 控件的更多信息，请参见 <xref:System.Windows.Controls.ItemsControl>。  
  
## 请参阅  
 <xref:System.Xml.XmlElement>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)