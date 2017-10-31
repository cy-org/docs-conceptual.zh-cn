---
title: "如何：使用 GridView 显示 ListView 内容 | Microsoft Docs"
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
  - "GridView, 显示 ListView 内容"
  - "ListView 控件, 使用 GridView 显示内容"
ms.assetid: 5bc1e767-ab46-4f14-bd41-3d5d39e1d000
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 GridView 显示 ListView 内容
本示例演示如何为 <xref:System.Windows.Controls.ListView> 控件定义 <xref:System.Windows.Controls.GridView> 查看模式。  
  
## 示例  
 通过指定 <xref:System.Windows.Controls.GridViewColumn> 对象，您可以定义 <xref:System.Windows.Controls.GridView> 的查看模式。  下面的示例演示如何定义绑定到为 <xref:System.Windows.Controls.ListView> 控件指定的数据内容的 <xref:System.Windows.Controls.GridViewColumn> 对象。  此 <xref:System.Windows.Controls.GridView> 示例指定三个 <xref:System.Windows.Controls.GridViewColumn> 对象，它们分别映射到设置为 <xref:System.Windows.Controls.ListView> 控件的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 的 `EmployeeInfoDataSource` 的 `FirstName`、`LastName` 和 `EmployeeNumber` 字段。  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 下图显示了此示例的显示效果。  
  
 ![具有 GridView 输出的 ListView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
## 请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)