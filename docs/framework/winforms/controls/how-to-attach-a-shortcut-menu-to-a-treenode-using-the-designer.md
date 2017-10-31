---
title: "如何：使用设计器将快捷菜单附加到 TreeNode | Microsoft Docs"
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
  - "快捷菜单, 附加到 TreeNode"
  - "TreeNode, 使用设计器附加快捷方式菜单"
ms.assetid: 8e45e184-1313-4f8f-90ff-2cd5789b2268
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用设计器将快捷菜单附加到 TreeNode
Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件显示一个节点层次结构，类似于 Windows 操作系统中 Windows 资源管理器左窗格中显示的文件和文件夹。  通过设置 <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> 属性，可以在用户右击 <xref:System.Windows.Forms.TreeView> 控件时向其提供区分上下文的操作。  通过将 <xref:System.Windows.Forms.ContextMenuStrip> 组件与单个 <xref:System.Windows.Forms.TreeNode> 项关联，可向 <xref:System.Windows.Forms.TreeView> 控件添加自定义级别的快捷菜单功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时将快捷菜单与 TreeNode 关联  
  
1.  向窗体添加 <xref:System.Windows.Forms.TreeView> 控件，然后按需要向 <xref:System.Windows.Forms.TreeView> 添加节点。  有关更多信息，请参见 [如何：添加和删除 Windows 窗体 TreeView 控件中的节点](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)。  
  
2.  向窗体添加 <xref:System.Windows.Forms.ContextMenuStrip> 组件，然后向快捷菜单中添加菜单项，快捷菜单表示您希望在运行时可用的节点级操作。  有关更多信息，请参见 [如何：向 ContextMenuStrip 添加菜单项](../../../../docs/framework/winforms/controls/how-to-add-menu-items-to-a-contextmenustrip.md)。  
  
3.  重新打开 <xref:System.Windows.Forms.TreeView> 控件的**“TreeNodeEditor”**对话框，选择要编辑的节点，并将其 <xref:System.Windows.Forms.ContextMenuStrip> 属性设置为要所添加的快捷菜单。  
  
4.  设置此属性后，右击该节点时将显示该快捷菜单。  
  
     另外，您需要编写处理这些菜单项的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件的代码。  
  
## 请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [TreeView 控件概述](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [ContextMenuStrip 控件](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)