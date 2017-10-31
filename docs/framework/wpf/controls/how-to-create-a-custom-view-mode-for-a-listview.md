---
title: "如何：为 ListView 创建自定义视图模式 | Microsoft Docs"
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
  - "ListView 控件, 创建自定义视图模式"
ms.assetid: 71077349-eeb9-4344-ab29-b5df96df3314
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：为 ListView 创建自定义视图模式
本示例演示如何为 <xref:System.Windows.Controls.ListView> 控件创建自定义 <xref:System.Windows.Controls.ListView.View%2A> 模式。  
  
## 示例  
 当为 <xref:System.Windows.Controls.ListView> 控件创建自定义视图时，必须使用 <xref:System.Windows.Controls.ViewBase> 类。  下面的示例演示了称为 `PlainView` 的视图模式，它是从 <xref:System.Windows.Controls.ViewBase> 类派生的。  
  
 [!code-csharp[ListViewCustomView#PlainView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/PlainView.cs#plainview)]
 [!code-vb[ListViewCustomView#PlainView](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/plainview.vb#plainview)]  
  
 若要向自定义视图应用样式，应使用 <xref:System.Windows.Style> 类。  下面的示例为 `PlainView` 视图模式定义 <xref:System.Windows.Style>。  在前面的示例中，此样式设置为 <xref:System.Windows.Controls.ViewBase.DefaultStyleKey%2A> 属性的值，该属性是为 `PlainView` 定义的。  
  
 [!code-xml[ListViewCustomView#PlainViewStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Themes/Generic.xaml#plainviewstyle)]  
  
 若要在自定义视图模式下定义数据的布局，应定义 <xref:System.Windows.DataTemplate> 对象。  下面的示例定义一个可用于在 `PlainView` 视图模式下显示数据的 <xref:System.Windows.DataTemplate>。  
  
 [!code-xml[ListViewCustomView#PlainViewDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewdatatemplate)]  
  
 下面的示例演示如何为使用在前面的示例中定义的 <xref:System.Windows.DataTemplate> 的 `PlainView` 视图模式定义 <xref:System.Windows.ResourceKey>。  
  
 [!code-xml[ListViewCustomView#PlainViewtileView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewtileview)]  
  
 如果您将 <xref:System.Windows.Controls.ListView.View%2A> 属性设置为该资源键，则 <xref:System.Windows.Controls.ListView> 控件可以使用自定义视图。  下面的示例演示如何将 `PlainView` 指定为 <xref:System.Windows.Controls.ListView> 的视图模式。  
  
 [!code-csharp[ListViewCustomView#ListViewtileViewmode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml.cs#listviewtileviewmode)]
 [!code-vb[ListViewCustomView#ListViewtileViewmode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/window1.xaml.vb#listviewtileviewmode)]  
  
 有关完整示例，请参见 [ListView with Multiple Views Sample](http://go.microsoft.com/fwlink/?LinkID=160013)（具有多个视图的 ListView 示例）。  
  
## 请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)