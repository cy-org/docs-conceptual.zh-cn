---
title: "ListView 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ListView"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "列表视图"
  - "列表"
  - "ListView 控件 [Windows 窗体], 关于 ListView 控件"
ms.assetid: c9ef56c1-3bb1-4101-9f4e-e95e720f2756
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# ListView 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ListView> 控件显示了带图标的项的列表。  可使用列表视图创建类似于 Windows 资源管理器右窗格的用户界面。  该控件具有四种视图模式：“LargeIcon”、“SmallIcon”、“List”和“Details”。  
  
## 使用 ListView 控件可以执行的操作  
  
> [!NOTE]
>  平铺是一种附加视图模式，只能在 Windows XP 和 Windows Server 2003 操作系统上使用。  有关更多信息，请参见 [如何：在 Windows 窗体 ListView 控件中启用平铺视图](../../../../docs/framework/winforms/controls/how-to-enable-tile-view-in-a-windows-forms-listview-control.md)。  
  
 大图标视图模式在项文本旁显示大图标；如果控件足够大，则项显示在多列中。  小图标视图模式除显示小图标外，其他方面与大图标视图模式相同。  列表视图模式显示小图标，但总是显示在单列中。  “Details”视图模式在多列中显示项。  有关详细信息，请参见[如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)。  视图模式取决于 <xref:System.Windows.Forms.ListView.View%2A> 属性。  所有视图模式都可显示图像列表中的图像。  有关详细信息，请参见[如何：显示 Windows 窗体 ListView 控件的图标](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)。  
  
 下表列出了一些 <xref:System.Windows.Forms.ListView> 成员以及这些成员适用于的视图。  
  
|ListView 成员|视图|  
|-----------------|--------|  
|<xref:System.Windows.Forms.ListView.Alignment%2A> 属性|<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.AutoArrange%2A> 属性|<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.AutoResizeColumn%2A> 方法|<xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.Columns%2A> 属性|<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.DrawSubItem> 事件|<xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.FindItemWithText%2A> 方法|<xref:System.Windows.Forms.View>、<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.FindNearestItem%2A> 方法|<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.GetItemAt%2A> 方法|<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
|<xref:System.Windows.Forms.ListView.Groups%2A> 属性|除 <xref:System.Windows.Forms.View> 之外的所有视图|  
|<xref:System.Windows.Forms.ListView.HeaderStyle%2A> 属性|<xref:System.Windows.Forms.View>.|  
|<xref:System.Windows.Forms.ListView.InsertionMark%2A> 属性|<xref:System.Windows.Forms.View>、<xref:System.Windows.Forms.View> 或 <xref:System.Windows.Forms.View>|  
  
 <xref:System.Windows.Forms.ListView> 控件的主要属性是 <xref:System.Windows.Forms.ListView.Items%2A>，该属性包含该控件显示的项。  <xref:System.Windows.Forms.ListView.SelectedItems%2A> 属性包含控件中当前选定项的集合。  如果将 <xref:System.Windows.Forms.ListView.MultiSelect%2A> 属性设置为 `true`，则用户可选择多项，例如，同时将若干项拖放到另一个控件中。  如果将 <xref:System.Windows.Forms.ListView.CheckBoxes%2A> 属性设置为 `true`，<xref:System.Windows.Forms.ListView> 控件可以显示这些项旁的复选框。  
  
 <xref:System.Windows.Forms.ListView.Activation%2A> 属性可以确定用户激活列表中的某项时必须执行的操作类型：选项有 <xref:System.Windows.Forms.ItemActivation>、 <xref:System.Windows.Forms.ItemActivation> 和 <xref:System.Windows.Forms.ItemActivation>。  执行 <xref:System.Windows.Forms.ItemActivation> 激活时，需要通过一次单击来激活该项。  执行 <xref:System.Windows.Forms.ItemActivation> 激活时，要求用户通过双击来激活该项；一次单击可以更改该项文本的颜色。  执行 <xref:System.Windows.Forms.ItemActivation> 激活时，要求用户通过双击来激活某项，但是该项的外观不会发生更改。  
  
 此外，<xref:System.Windows.Forms.ListView> 控件还支持 Windows XP 平台中可用的可视样式和其他功能，包括分组、平铺视图和插入标记。  有关更多信息，请参见 [Windows XP Features and Windows Forms Controls](http://msdn.microsoft.com/zh-cn/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0)。  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [如何：显示 Windows 窗体 ListView 控件的图标](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [如何：使用 Windows 窗体 ListView 控件在列中显示子项](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [如何：选择 Windows 窗体 ListView 控件中的项](../../../../docs/framework/winforms/controls/how-to-select-an-item-in-the-windows-forms-listview-control.md)   
 [如何：对 Windows 窗体 ListView 控件中的项进行分组](../../../../docs/framework/winforms/controls/how-to-group-items-in-a-windows-forms-listview-control.md)   
 [如何：在 Windows 窗体 ListView 控件中显示插入标记](../../../../docs/framework/winforms/controls/how-to-display-an-insertion-mark-in-a-windows-forms-listview-control.md)   
 [如何：向 ListView 控件添加搜索功能](../../../../docs/framework/winforms/controls/how-to-add-search-capabilities-to-a-listview-control.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [如何：用 Windows 窗体创建多窗格用户界面](../../../../docs/framework/winforms/controls/how-to-create-a-multipane-user-interface-with-windows-forms.md)