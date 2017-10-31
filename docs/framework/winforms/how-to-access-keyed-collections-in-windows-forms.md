---
title: "如何：在 Windows 窗体中访问键控集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "集合, 使用键访问"
  - "键控集合 [Windows 窗体]"
ms.assetid: b9b79b8b-d9bf-4f8c-b9d6-9578bc3219d3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在 Windows 窗体中访问键控集合
-   可以通过键来访问单个集合项。  此功能已添加到通常由 Windows 窗体应用程序使用的许多集合类中。  下面的列表显示具有可访问键控集合的一些集合类。  
  
-   <xref:System.Windows.Forms.ListView.ListViewItemCollection>  
  
-   <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection>  
  
-   <xref:System.Windows.Forms.Control.ControlCollection>  
  
-   <xref:System.Windows.Forms.TabControl.TabPageCollection>  
  
-   <xref:System.Windows.Forms.TreeNodeCollection>  
  
 与集合中的项关联的键通常是该项的名称。  下面的过程演示如何使用集合类执行常规任务。  
  
### 查找焦点并为控件集合中的嵌套控件设置焦点  
  
-   使用 <xref:System.Windows.Forms.Control.ControlCollection.Find%2A> 和 <xref:System.Windows.Forms.Control.Focus%2A> 方法来指定控件名称，以查找并设置焦点。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#1)]  
  
### 访问图像集合中的图像  
  
-   使用 <xref:System.Windows.Forms.ImageList.ImageCollection.Item%2A> 属性指定要访问的图像的名称。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#2)]  
  
### 将选项卡页设置为选定的选项卡  
  
-   同时使用 <xref:System.Windows.Forms.TabControl.SelectedTab%2A> 属性和 <xref:System.Windows.Forms.TabControl.TabPageCollection.Item%2A> 属性来指定要设置为选定选项卡的选项卡页的名称。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#3)]  
  
## 请参阅  
 [Windows 窗体入门](../../../docs/framework/winforms/getting-started-with-windows-forms.md)   
 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)