---
title: "如何：使用 Windows 窗体 ListView 控件添加和移除项 | Microsoft Docs"
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
  - "列表视图, 添加列表项"
  - "ListView 控件 [Windows 窗体], 添加列表项"
  - "ListView 控件 [Windows 窗体], 填充"
ms.assetid: 1b35a80a-edd8-495f-a807-a28c4aae52c6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 ListView 控件添加和移除项
向 Windows 窗体 <xref:System.Windows.Forms.ListView> 控件中添加项的过程主要包括：指定项以及为其分配属性。  可在任何时候添加或移除列表项。  
  
### 以编程方式添加项  
  
1.  使用 <xref:System.Windows.Forms.ListView.Items%2A> 属性的 <xref:System.Windows.Forms.ListView.ListViewItemCollection.Add%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#11)]  
  
### 以编程方式移除项  
  
1.  使用 <xref:System.Windows.Forms.ListView.Items%2A> 属性的 <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> 或 <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> 方法。  <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> 方法移除一项，而 <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> 方法移除列表中的所有项。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#12)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)