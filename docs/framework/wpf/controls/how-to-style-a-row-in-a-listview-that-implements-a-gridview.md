---
title: "如何：为实现 GridView 的 ListView 中的行设置样式 | Microsoft Docs"
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
  - "GridView 控件，设置行样式"
  - "在实现 GridView 的 ListView 中设置行样式"
  - "使用 Gridview 设置行样式的 ListView 控件"
ms.assetid: 2e406ba2-70a0-4e62-841f-0934859de76e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：为实现 GridView 的 ListView 中的行设置样式
此示例演示如何设置样式中的行<xref:System.Windows.Controls.ListView>实现控件<xref:System.Windows.Controls.GridView><xref:System.Windows.Controls.ListView.View%2A>模式。  
  
## <a name="example"></a>示例  
 你可以设置样式中的某一行<xref:System.Windows.Controls.ListView>通过设置<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>上<xref:System.Windows.Controls.ListView>控件。 将表示为其项的样式设置<xref:System.Windows.Controls.ListViewItem>对象。 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>引用<xref:System.Windows.Controls.ControlTemplate>用于显示行内容的对象。  
  
 完整示例，下面的示例从提取的显示歌曲信息存储在集合[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]数据库。 每首歌曲在数据库中的具有评级字段，此字段的值指定如何显示歌曲信息的行。  
  
 下面的示例演示如何定义<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>为<xref:System.Windows.Controls.ListViewItem>这些对象表示在歌曲集合中的歌曲。 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>引用<xref:System.Windows.Controls.ControlTemplate>指定如何显示歌曲信息的行的对象。  
  
 [!code-xml[ListViewItemStyleSnippet#ItemContainerStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#itemcontainerstyle)]  
  
 下面的示例演示<xref:System.Windows.Controls.ControlTemplate> ，它将文本字符串`"Strongly Recommended"`到的行。 此模板中引用<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>并显示当歌曲的分级具有的值为 5 （五个）。 <xref:System.Windows.Controls.ControlTemplate>包括<xref:System.Windows.Controls.GridViewRowPresenter>对象定义的列中的行的内容布局<xref:System.Windows.Controls.GridView>视图模式。  
  
 [!code-xml[ListViewItemStyleSnippet#ControlTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#controltemplate)]  
  
 下面的示例定义<xref:System.Windows.Controls.GridView>。  
  
 [!code-xml[ListViewItemStyleSnippet#GridView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#gridview)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [操作指南主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [样式和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)