---
title: "如何：添加和删除 Windows 窗体 TreeView 控件中的节点 | Microsoft Docs"
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
  - "示例 [Windows 窗体], TreeView 控件"
  - "TreeView 控件中的树节点"
  - "TreeView 控件 [Windows 窗体], 添加节点"
  - "TreeView 控件 [Windows 窗体], 移除节点"
ms.assetid: de1b82db-4905-449a-9f59-af271a6b6673
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：添加和删除 Windows 窗体 TreeView 控件中的节点
Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件将顶级节点存储在其 <xref:System.Windows.Forms.TreeView.Nodes%2A> 集合中。  每个 <xref:System.Windows.Forms.TreeNode> 自身还有一个用来存储其子节点的 <xref:System.Windows.Forms.TreeNode.Nodes%2A> 集合。  这两个集合属性都属于 <xref:System.Windows.Forms.TreeNodeCollection> 类型，提供标准集合成员，使您可以在节点层次结构的单个层次上添加、移除和重新排列节点。  
  
### 以编程方式添加节点  
  
1.  使用树视图 <xref:System.Windows.Forms.TreeView.Nodes%2A> 属性的 <xref:System.Windows.Forms.TreeNodeCollection.Add%2A> 方法。  
  
    ```vb  
    ' Adds new node as a child node of the currently selected node.  
    Dim newNode As TreeNode = New TreeNode("Text for new node")  
    TreeView1.SelectedNode.Nodes.Add(newNode)  
  
    ```  
  
    ```csharp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode newNode = new TreeNode("Text for new node");  
    treeView1.SelectedNode.Nodes.Add(newNode);  
  
    ```  
  
    ```cpp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode ^ newNode = new TreeNode("Text for new node");  
    treeView1->SelectedNode->Nodes->Add(newNode);  
    ```  
  
### 以编程方式移除节点  
  
1.  使用树视图 <xref:System.Windows.Forms.TreeView.Nodes%2A> 属性的 <xref:System.Windows.Forms.TreeNodeCollection.Remove%2A> 方法移除单个节点，或使用 <xref:System.Windows.Forms.TreeNodeCollection.Clear%2A> 方法清除所有节点。  
  
    ```vb  
    ' Removes currently selected node, or root if nothing is selected.  
    TreeView1.Nodes.Remove(TreeView1.SelectedNode)  
    ' Clears all nodes.  
    TreeView1.Nodes.Clear()  
  
    ```  
  
    ```csharp  
    // Removes currently selected node, or root if nothing   
    // is selected.  
    treeView1.Nodes.Remove(treeView1.SelectedNode);  
    // Clears all nodes.  
    TreeView1.Nodes.Clear();  
  
    ```  
  
    ```cpp  
    // Removes currently selected node, or root if nothing  
    // is selected.  
    treeView1->Nodes->Remove(treeView1->SelectedNode);  
    // Clears all nodes.  
    treeView1->Nodes->Clear();  
    ```  
  
## 请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [TreeView 控件概述](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [如何：设置 Windows 窗体 TreeView 控件的图标](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md)   
 [如何：循环访问 Windows 窗体 TreeView 控件的所有节点](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [如何：确定被单击的 TreeView 节点](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)