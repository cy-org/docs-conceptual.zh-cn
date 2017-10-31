---
title: "如何：选择 Windows 窗体 ListView 控件中的项 | Microsoft Docs"
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
  - "列表视图, 选择项"
  - "列表, 选择项"
  - "ListView 控件 [Windows 窗体], 选择项"
  - "选择, 在列表视图中"
ms.assetid: ddea918e-1ddf-47f4-bd09-1e9b4c9d0c39
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：选择 Windows 窗体 ListView 控件中的项
此示例演示如何用编程方式在 Windows 窗体 <xref:System.Windows.Forms.ListView> 控件中选择项。  以编程方式选择项不会自动将焦点更改到 <xref:System.Windows.Forms.ListView> 控件。  因此，在选择项时通常还需要将项设置为焦点项。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.ListView.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListView.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/VB/form1.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   一个名为 `listView1` 的 <xref:System.Windows.Forms.ListView> 控件，其中至少包含一项。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 命名空间的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListViewItem.Selected%2A?displayProperty=fullName>