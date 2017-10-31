---
title: "如何：设置 Windows 窗体 TreeView 控件的图标 | Microsoft Docs"
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
  - "图标, 为 TreeView 控件设置"
  - "ImageList 组件 [Windows 窗体], 添加图像"
  - "TreeView 控件中的树节点, 图标"
  - "TreeView 控件 [Windows 窗体], 节点图标"
ms.assetid: c14ddcc0-e5a6-4c21-a2d5-6799fd491781
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：设置 Windows 窗体 TreeView 控件的图标
Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件可在每个节点旁显示图标。  图标紧挨着节点文本的左侧。  若要显示这些图标，必须使树视图与 <xref:System.Windows.Forms.ImageList> 控件相关联。  有关图像列表的更多信息，请参见 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) 和 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)。  
  
> [!NOTE]
>  当应用程序调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 时，Microsoft .NET Framework 1.1 版中的一个 bug 会使图像无法显示在 <xref:System.Windows.Forms.TreeView> 节点上。  作为此 Bug 的一种解决方法，可以在调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 之后立即调用 `Main` 方法中的 <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName>。  此 Bug 在 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 中修复。  
  
### 在树视图中显示图像  
  
1.  设置 <xref:System.Windows.Forms.TreeView> 控件的 <xref:System.Windows.Forms.TreeView.ImageList%2A> 属性为想要使用的现有 <xref:System.Windows.Forms.ImageList> 控件。  
  
     这些属性可在设计器中使用“属性”窗口进行设置，也可在代码中设置。  
  
    ```vb  
    TreeView1.ImageList = ImageList1  
  
    ```  
  
    ```csharp  
    treeView1.ImageList = imageList1;  
  
    ```  
  
    ```cpp  
    treeView1->ImageList = imageList1;  
    ```  
  
2.  设置节点的 <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> 和 <xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> 属性。  <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> 属性确定正常和展开状态下的节点显示的图像， <xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> 属性确定选定状态下的节点显示的图像。  
  
     这些属性可在代码中设置，或在“树节点编辑器”中设置。  若要打开“树节点编辑器”，请单击“属性”窗口中 <xref:System.Windows.Forms.TreeView.Nodes%2A> 属性旁边的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
    ```vb  
    ' (Assumes that ImageList1 contains at least two images and  
    ' the TreeView control contains a selected image.)  
    TreeView1.SelectedNode.ImageIndex = 0  
    TreeView1.SelectedNode.SelectedImageIndex = 1  
  
    ```  
  
    ```csharp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1.SelectedNode.ImageIndex = 0;  
    treeView1.SelectedNode.SelectedImageIndex = 1;  
  
    ```  
  
    ```cpp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1->SelectedNode->ImageIndex = 0;  
    treeView1->SelectedNode->SelectedImageIndex = 1;  
    ```  
  
## 请参阅  
 [TreeView 控件概述](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [如何：添加和删除 Windows 窗体 TreeView 控件中的节点](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)   
 [如何：循环访问 Windows 窗体 TreeView 控件的所有节点](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [如何：确定被单击的 TreeView 节点](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)