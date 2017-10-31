---
title: "如何：使用设计器用 Windows 窗体 TreeView 控件添加和移除节点 | Microsoft Docs"
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
  - "示例 [Windows 窗体], TreeView 控件"
  - "TreeView 控件中的树节点"
  - "TreeView 控件 [Windows 窗体], 添加节点"
  - "TreeView 控件 [Windows 窗体], 移除节点"
ms.assetid: 35bf1750-045e-4ec5-97cb-b47b0dbdaa2c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用设计器用 Windows 窗体 TreeView 控件添加和移除节点
因为 Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件以层次结构的方式显示节点，所以在添加节点时必须注意哪个节点是它的父节点。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.TreeView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中添加或移除节点  
  
1.  选择 <xref:System.Windows.Forms.TreeView> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.TreeView.Nodes%2A> 属性旁的**“省略号”**\(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮。  
  
     显示**“树节点编辑器”**。  
  
3.  若要添加节点，必须存在根节点；如果不存在根节点，必须先单击**“添加根”**按钮添加一个根节点。  然后，就可通过选择根节点或任何其他节点并单击**“添加子级”**按钮来添加子节点。  
  
4.  若要删除节点，请选择要删除的节点，然后单击**“删除”**按钮。  
  
## 请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [TreeView 控件概述](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [如何：设置 Windows 窗体 TreeView 控件的图标](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md)   
 [如何：循环访问 Windows 窗体 TreeView 控件的所有节点](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [如何：确定被单击的 TreeView 节点](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)