---
title: "如何：使用设计器用 Windows 窗体 ListView 控件添加和移除项 | Microsoft Docs"
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
  - "ListView 控件 [Windows 窗体], 添加列表项"
  - "ListView 控件 [Windows 窗体], 填充"
ms.assetid: 217611ee-fd11-4d39-9a54-a37c3e781be1
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用设计器用 Windows 窗体 ListView 控件添加和移除项
向 Windows 窗体 <xref:System.Windows.Forms.ListView> 控件中添加项的过程主要包括：指定项以及为其分配属性。  可在任何时候添加或移除列表项。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.ListView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 使用设计器添加或移除项  
  
1.  选择 <xref:System.Windows.Forms.ListView> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.ListView.Items%2A> 属性旁的**“省略号”**\(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮。  
  
     出现**“ListViewItem 集合编辑器”**。  
  
3.  若要添加项，请单击**“添加”**按钮。  然后可以设置新项的属性，如 <xref:System.Windows.Forms.ListView.Text%2A> 和 <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> 属性。  
  
4.  若要移除某项，请选择该项并单击**“移除”**按钮。  
  
## 请参阅  
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [如何：使用 Windows 窗体 ListView 控件在列中显示子项](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [如何：显示 Windows 窗体 ListView 控件的图标](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [如何：对 Windows 窗体 ListView 控件中的项进行分组](../../../../docs/framework/winforms/controls/how-to-group-items-in-a-windows-forms-listview-control.md)