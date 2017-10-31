---
title: "如何：对 Windows 窗体 ListView 控件中的项进行分组 | Microsoft Docs"
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
  - "分组"
  - "组"
  - "组, 在 Windows 窗体控件中"
  - "列表视图, 分组项"
  - "列表, 分组项"
  - "ListView 控件 [Windows 窗体], 分组项"
ms.assetid: 610416a1-8da4-436c-af19-5f19e654769b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：对 Windows 窗体 ListView 控件中的项进行分组
使用 <xref:System.Windows.Forms.ListView> 控件的分组功能可以用分组形式显示相关项组。  在屏幕上，这些组由包含组标题的水平组标头分隔。  可以使用 <xref:System.Windows.Forms.ListView> 组按字母顺序、日期或任何其他逻辑组合对项进行分组，从而简化大型列表的导航。  下图显示了一些分好组的项。  
  
 ![ListView 组](../../../../docs/framework/winforms/controls/media/listviewgroups.gif "ListViewGroups")  
ListView 已分组的项  
  
 若要启用分组，首先必须在设计器中或以编程方式创建一个或多个组。  定义组后，可向组分配 <xref:System.Windows.Forms.ListView> 项。  此外，可以用编程方式将一个组中的项移至另外一个组中。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ListView> 组仅在应用程序调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法时在 [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] 上可用。  在以前的操作系统上，任何与组有关的代码都无效，并且组也不会出现。  有关更多信息，请参见 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=fullName>。  
  
### 添加组  
  
1.  使用 <xref:System.Windows.Forms.ListView.Groups%2A> 集合的 <xref:System.Windows.Forms.ListViewGroupCollection.Add%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#21)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#21)]  
  
### 移除组  
  
1.  使用 <xref:System.Windows.Forms.ListView.Groups%2A> 集合的 <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> 或 <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> 方法。  
  
     <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> 方法可移除单个组，而 <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> 方法可移除列表中的所有组。  
  
    > [!NOTE]
    >  移除某个组时，不会移除该组中的项。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#22)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#22)]  
  
### 向组分配项或在组之间移动项  
  
1.  设置各个项的 <xref:System.Windows.Forms.ListViewItem.Group%2A?displayProperty=fullName> 属性。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#23)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#23)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ListViewGroup>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Windows XP Features and Windows Forms Controls](http://msdn.microsoft.com/zh-cn/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)