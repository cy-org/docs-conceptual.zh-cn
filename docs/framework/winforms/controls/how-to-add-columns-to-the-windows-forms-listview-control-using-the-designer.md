---
title: "如何：使用设计器向 Windows 窗体 ListView 控件添加列 | Microsoft Docs"
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
  - "ListView 控件 [Windows 窗体], 添加列标题"
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用设计器向 Windows 窗体 ListView 控件添加列
Windows 窗体 <xref:System.Windows.Forms.ListView> 控件在位于**“详细信息”**视图中时，可为每个列表项显示多列。  可使用这些列显示关于各个列表项的若干种信息。  例如，文件列表可以显示文件名、文件类型、大小和文件最近一次修改的日期。  有关在创建列后对列进行填充的信息，请参见 [如何：使用 Windows 窗体 ListView 控件在列中显示子项](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.ListView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中添加列  
  
1.  在**“属性”**窗口中，将该控件的 <xref:System.Windows.Forms.ListView.View%2A> 属性设置为 <xref:System.Windows.Forms.View>。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.ListView.Columns%2A> 属性旁的**“省略号”**按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
     出现**“ColumnHeader 集合编辑器”**。  
  
3.  使用**“添加”**按钮添加新列。  然后可以选择列标题并设置其文本（列的标题文字）、文本对齐方式和宽度。  
  
## 请参阅  
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [如何：使用 Windows 窗体 ListView 控件在列中显示子项](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [如何：显示 Windows 窗体 ListView 控件的图标](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)