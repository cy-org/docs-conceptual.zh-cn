---
title: "如何：显示 Windows 窗体 ListView 控件的图标 | Microsoft Docs"
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
  - "图标, 为 ListView 控件显示"
  - "ImageList 组件 [Windows 窗体], 使用 ListView 控件"
  - "列表视图, 显示图标"
  - "列表, 显示图标"
  - "ListView 控件 [Windows 窗体], 显示图标"
ms.assetid: 9d577542-8595-429b-99e5-078770ec9d35
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：显示 Windows 窗体 ListView 控件的图标
Windows 窗体 <xref:System.Windows.Forms.ListView> 控件可显示三个图像列表中的图标。  “List”视图、“Details”视图和“SmallIcon”视图显示 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 属性中指定的图像列表里的图像。  “LargeIcon”视图显示 <xref:System.Windows.Forms.ListView.LargeImageList%2A> 属性中指定的图像列表里的图像。  列表视图还可在大图标或小图标旁显示 <xref:System.Windows.Forms.ListView.StateImageList%2A> 属性中设置的一组附加图标。  有关图像列表的更多信息，请参见 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) 和 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)。  
  
### 在列表视图中显示图像  
  
1.  将相应的属性（<xref:System.Windows.Forms.ListView.SmallImageList%2A>、<xref:System.Windows.Forms.ListView.LargeImageList%2A> 或 <xref:System.Windows.Forms.ListView.StateImageList%2A>）设置为想要使用的现有 <xref:System.Windows.Forms.ImageList> 组件。  
  
     这些属性可在设计器中使用“属性”窗口进行设置，也可在代码中设置。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#41)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#41)]  
  
2.  为每个具有关联图标的列表项设置 <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> 或 <xref:System.Windows.Forms.ListViewItem.StateImageIndex%2A> 属性。  
  
     这些属性可在代码中设置，或在**“ListViewItem 集合编辑器”**中进行设置。  若要打开**“ListViewItem 集合编辑器”**，请在**“属性”**窗口中，单击 <xref:System.Windows.Forms.ListView.Items%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#42)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#42)]  
  
## 请参阅  
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)