---
title: "如何：将快捷菜单附加到 TreeView 节点 | Microsoft Docs"
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
  - "快捷菜单, 添加到 TreeView 控件"
  - "TreeView 控件中的树节点, 快捷菜单"
  - "TreeView 控件 [Windows 窗体], 添加快捷菜单"
ms.assetid: a23c6752-fd8f-44ad-b781-bab37962fc7c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：将快捷菜单附加到 TreeView 节点
Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件以类似于在 Windows 资源管理器左窗格中显示文件和文件夹的方式显示节点的层次结构。  通过设置 <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> 属性，可以在用户右击 <xref:System.Windows.Forms.TreeView> 控件时向其提供区分上下文的操作。  通过将 <xref:System.Windows.Forms.ContextMenuStrip> 组件与单个 <xref:System.Windows.Forms.TreeNode> 项关联，可向 <xref:System.Windows.Forms.TreeView> 控件添加自定义级别的快捷菜单功能。  
  
### 以编程方式将快捷菜单与 TreeNode 关联  
  
1.  用适当的属性设置实例化一个 <xref:System.Windows.Forms.TreeView> 控件，创建一个根 <xref:System.Windows.Forms.TreeNode>，然后添加子节点。  
  
2.  实例化一个 <xref:System.Windows.Forms.ContextMenuStrip> 组件，然后为您要使其在运行时可用的每项操作添加一个 <xref:System.Windows.Forms.ToolStripMenuItem>。  
  
3.  将适当 <xref:System.Windows.Forms.TreeNode> 的 <xref:System.Windows.Forms.TreeNode.ContextMenuStrip%2A> 属性设置为您创建的快捷菜单。  
  
4.  设置此属性后，右击该节点时将显示该快捷菜单。  
  
 下面的代码示例创建与 <xref:System.Windows.Forms.TreeView> 的根 <xref:System.Windows.Forms.TreeNode> 关联的基本 <xref:System.Windows.Forms.TreeView> 和 <xref:System.Windows.Forms.ContextMenuStrip>。  您需要将菜单选项自定义为适合正在开发的 <xref:System.Windows.Forms.TreeView> 的菜单项。  另外，您需要编写处理这些菜单项的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件的代码。  
  
 [!code-cpp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/cpp/Form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/VB/Form1.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Forms.ContextMenuStrip>   
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)