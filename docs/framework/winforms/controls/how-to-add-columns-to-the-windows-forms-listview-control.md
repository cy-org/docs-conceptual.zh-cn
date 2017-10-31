---
title: "如何：向 Windows 窗体 ListView 控件中添加列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 添加到 ListView 控件"
  - "列表视图, 添加列"
  - "ListView 控件 [Windows 窗体], 添加列标题"
ms.assetid: 79174274-12ee-4a5d-80db-6ec02976d010
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：向 Windows 窗体 ListView 控件中添加列
在“详细信息”视图中，<xref:System.Windows.Forms.ListView> 控件可以为每个列表项显示多个列。  可使用这些列向用户显示每个列表项若干类型的信息。  例如，文件列表可以显示文件名、文件类型、大小和文件最近一次修改的日期。  有关在创建列后对列进行填充的信息，请参见 [如何：使用 Windows 窗体 ListView 控件在列中显示子项](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)。  
  
### 以编程方式添加列  
  
1.  将该控件的 <xref:System.Windows.Forms.ListView.View%2A> 属性设置为 <xref:System.Windows.Forms.View>。  
  
2.  使用列表视图 <xref:System.Windows.Forms.ListView.Columns%2A> 属性的 <xref:System.Windows.Forms.ListView.ColumnHeaderCollection.Add%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#31)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)