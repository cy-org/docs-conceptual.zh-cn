---
title: "如何：使用 GridViewRowPresenter 来显示数据 | Microsoft Docs"
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
  - "使用 GridViewRowPresenter 显示数据"
  - "GridViewRowPresenter"
ms.assetid: bdb785a5-a262-44d5-a517-ea14383e5f70
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 GridViewRowPresenter 来显示数据
此示例演示如何使用 <xref:System.Windows.Controls.GridViewRowPresenter> 和 <xref:System.Windows.Controls.GridViewHeaderRowPresenter> 对象在列中显示数据。  
  
## 示例  
 下面的示例演示如何指定一个用 <xref:System.Windows.Controls.GridViewRowPresenter> 和 <xref:System.Windows.Controls.GridViewHeaderRowPresenter> 对象来显示 <xref:System.DateTime> 对象的 <xref:System.DateTime.DayOfWeek%2A> 和 <xref:System.DateTime.Year%2A> 的 <xref:System.Windows.Controls.GridViewColumnCollection>。  此示例还为 <xref:System.Windows.Controls.GridViewColumn> 的 <xref:System.Windows.Controls.GridViewColumn.Header%2A> 定义了 <xref:System.Windows.Style>。  
  
 [!code-xml[GridViewRowPresenterSample#GridViewRowPresenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewRowPresenterSample/CS/Window1.xaml#gridviewrowpresenter)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GridViewHeaderRowPresenter>   
 <xref:System.Windows.Controls.GridViewRowPresenter>   
 <xref:System.Windows.Controls.GridViewColumnCollection>   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)