---
title: "如何：使用模板创建使用 GridView 的 ListView 的样式 | Microsoft Docs"
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
  - "ListView 控件, 样式设置"
ms.assetid: 94bf964b-96c8-4bdf-a0c3-f5271b7cb565
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用模板创建使用 GridView 的 ListView 的样式
此示例演示如何使用 <xref:System.Windows.DataTemplate> 和 <xref:System.Windows.Style> 对象来指定使用 <xref:System.Windows.Controls.GridView> 视图模式的 <xref:System.Windows.Controls.ListView> 控件的外观。  
  
## 示例  
 下面的示例显示 <xref:System.Windows.Style> 和 <xref:System.Windows.DataTemplate> 对象，这些对象自定义 <xref:System.Windows.Controls.GridViewColumn> 的列标题的外观。  
  
 [!code-xml[ListViewTemplate#GridViewHeaderStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheaderstyle)]  
  
 [!code-xml[ListViewTemplate#GridViewHeaderTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheadertemplate)]  
  
 下面的示例演示如何使用这些 <xref:System.Windows.Style> 和 <xref:System.Windows.DataTemplate> 对象来设置 <xref:System.Windows.Controls.GridViewColumn> 的 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> 和 <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> 属性。  <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 属性定义列单元格的内容。  
  
 [!code-xml[ListViewTemplate#GridViewColumnTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcolumntemplate)]  
  
 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> 和 <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> 只是您可用于自定义 <xref:System.Windows.Controls.GridView> 控件的列标题外观的若干属性中的两个。  有关更多信息，请参见 [GridView 列标题的样式和模板概述](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md)。  
  
 下面的示例演示如何定义对 <xref:System.Windows.Controls.GridViewColumn> 中的单元格外观进行自定义的 <xref:System.Windows.DataTemplate>。  
  
 [!code-xml[ListViewTemplate#GridViewCellTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 下面的示例演示如何使用此 <xref:System.Windows.DataTemplate> 来定义 <xref:System.Windows.Controls.GridViewColumn> 单元格的内容。  将使用此模板，而不是前面的 <xref:System.Windows.Controls.GridViewColumn> 示例中显示的 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 属性。  
  
 [!code-xml[ListViewTemplate#CellTemplateProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)