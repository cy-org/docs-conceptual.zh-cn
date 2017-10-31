---
title: "GridView 列标题的样式和模板概述 | Microsoft Docs"
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
  - "列标题, 自定义"
  - "控件, ListView"
  - "GridView 视图模式, 自定义列标题"
  - "页眉, 自定义"
  - "ListView 控件 [WPF], GridView 列标题样式"
ms.assetid: 74835674-a39e-4ab5-9418-ad7f6ab7b956
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# GridView 列标题的样式和模板概述
本概述讨论了属性的优先级顺序（这些属性用于在 <xref:System.Windows.Controls.ListView> 控件的 <xref:System.Windows.Controls.GridView> 视图模式中自定义列标头）。  
  
## 在 GridView 中自定义列标头  
 在多个相关类中找到定义内容、布局和 <xref:System.Windows.Controls.GridView> 中的列标头样式的属性。  这些属性中的某些属性具有类似或相同的功能。  
  
 下表中的行显示执行相同功能的属性组。  您可以使用这些属性自定义 <xref:System.Windows.Controls.GridView> 中的列标头。  相关属性的优先级顺序是从右向左，其中最右边列中的属性具有最高优先级。  例如，如果 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 设置在 <xref:System.Windows.Controls.GridViewColumnHeader> 对象上，而 <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A> 设置在相关 <xref:System.Windows.Controls.GridViewColumn> 上，那么 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 具有更高的优先级。  此种情况下，<xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A> 无效。  
  
 **GridView 中的列标头的相关属性**  
  
|||||  
|-|-|-|-|  
|**类**|<xref:System.Windows.Controls.GridView>|<xref:System.Windows.Controls.GridViewColumn>|<xref:System.Windows.Controls.GridViewColumnHeader>|  
|**上下文菜单属性**|<xref:System.Windows.Controls.GridView.ColumnHeaderContextMenu%2A>|不适用|<xref:System.Windows.FrameworkElement.ContextMenu%2A>|  
|**ToolTip**<br /><br /> **属性**|<xref:System.Windows.Controls.GridView.ColumnHeaderToolTip%2A>|不适用|<xref:System.Windows.FrameworkElement.ToolTip%2A>|  
|**页眉模板**<br /><br /> **属性**|<xref:System.Windows.Controls.GridView.ColumnHeaderTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.GridView.ColumnHeaderTemplateSelector%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A>|<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A>|  
|**样式属性**|<xref:System.Windows.Controls.GridView.ColumnHeaderContainerStyle%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A>|<xref:System.Windows.FrameworkElement.Style%2A>|  
  
 <sup>1</sup>对于**“标头模板属性”**，如果您同时设置模板属性和模板选择器属性，则模板属性具有更高的优先级。  例如，如果同时设置了 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 和 <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A> 属性，则 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 属性具有更高的优先级。  
  
## 请参阅  
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)