---
title: "如何：使用 Windows 窗体 ListView 控件在列中显示子项 | Microsoft Docs"
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
  - "详细信息视图"
  - "列表项"
  - "ListView 控件 [Windows 窗体], 添加 ListSubItems"
  - "子项"
ms.assetid: e465f044-cde7-4fd9-a687-788a73a0f554
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用 Windows 窗体 ListView 控件在列中显示子项
Windows 窗体 <xref:System.Windows.Forms.ListView> 控件可为“详细信息视图”中的每一项显示附加文本或子项。  第一列显示项文本，例如雇员编号。  第二、第三及随后的列显示第一、第二及随后的关联子项。  
  
### 将子项添加到列表项中  
  
1.  添加所需的任何列。  由于第一列要显示项的 <xref:System.Windows.Forms.ListView.Text%2A> 属性，需要的列数应比子项多一个。  有关添加列的更多信息，请参见 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)。  
  
2.  调用由项的 <xref:System.Windows.Forms.ListViewItem.SubItems%2A> 属性返回的集合的 <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection.Add%2A> 方法。  下面的代码实例为一个列表项设置职员姓名和部门。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#61)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#61)]  
  
## 请参阅  
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [如何：显示 Windows 窗体 ListView 控件的图标](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)