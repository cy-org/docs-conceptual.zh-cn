---
title: "如何：向 ListView 控件添加搜索功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "列表视图, 启用搜索"
  - "列表, 启用搜索"
  - "ListView 控件 [Windows 窗体], 添加搜索功能"
  - "搜索, 向 ListView 控件添加搜索功能"
ms.assetid: 557782d9-b705-4bab-b496-9938afddac82
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：向 ListView 控件添加搜索功能
在 <xref:System.Windows.Forms.ListView> 控件中使用大型的项列表时，经常会希望向用户提供搜索功能。  <xref:System.Windows.Forms.ListView> 控件以两种不同的方式提供此功能：文本匹配和位置搜索。  
  
 <xref:System.Windows.Forms.ListView.FindItemWithText%2A> 方法允许在处于列表或详细信息视图的 <xref:System.Windows.Forms.ListView> 上执行文本搜索，要求给定搜索字符串和可选起始和结束索引。  而 <xref:System.Windows.Forms.ListView.FindNearestItem%2A> 方法允许在处于图标或平铺视图的 <xref:System.Windows.Forms.ListView> 中查找项，要求给定一组 x 坐标和 y 坐标以及一个搜索方向。  
  
### 使用文本查找项  
  
1.  创建一个 <xref:System.Windows.Forms.ListView>，<xref:System.Windows.Forms.ListView.View%2A> 属性设置为 <xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>，然后用项填充该 <xref:System.Windows.Forms.ListView>。  
  
2.  调用 <xref:System.Windows.Forms.ListView.FindItemWithText%2A> 方法，向其传递要查找的项的文本。  
  
3.  下面的代码示例演示如何创建基本 <xref:System.Windows.Forms.ListView>，用项进行填充并使用由用户输入的文本来在列表中查找项。  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#1)]  
  
### 使用 x 坐标和 y 坐标查找项  
  
1.  创建一个 <xref:System.Windows.Forms.ListView>，<xref:System.Windows.Forms.View> 属性设置为 <xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>，然后用项填充该 <xref:System.Windows.Forms.ListView>。  
  
2.  调用 <xref:System.Windows.Forms.ListView.FindNearestItem%2A> 方法，向其传递所需的 x 坐标和 y 坐标以及要查找的方向。  
  
3.  下面的代码示例演示如何创建基本图标 <xref:System.Windows.Forms.ListView>，用项进行填充和捕获 <xref:System.Windows.Forms.Control.MouseDown> 事件来在向上方向查找最近的项。  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#2)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#2)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListView.FindItemWithText%2A>   
 <xref:System.Windows.Forms.ListView.FindNearestItem%2A>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)