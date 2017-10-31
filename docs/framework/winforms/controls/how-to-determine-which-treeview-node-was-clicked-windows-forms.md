---
title: "如何：确定被单击的 TreeView 节点（Windows 窗体） | Microsoft Docs"
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
  - "TreeNode"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "示例 [Windows 窗体], TreeView 控件"
  - "TreeView 控件中的树节点, 确定所单击的节点"
  - "TreeView 控件 [Windows 窗体], 确定所单击的节点"
ms.assetid: 06a4a191-d918-42af-9f49-956c93eff261
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：确定被单击的 TreeView 节点（Windows 窗体）
使用 Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件时，一个常见的任务是确定单击了哪个节点，并相应地予以响应。  
  
### 确定单击了哪个 TreeView 节点  
  
1.  使用 <xref:System.EventArgs> 对象返回对已单击节点对象的引用。  
  
2.  通过检查 <xref:System.Windows.Forms.TreeViewEventArgs> 类（它包含与事件有关的数据）来确定单击了哪个节点。  
  
    ```vb  
    Private Sub TreeView1_AfterSelect(ByVal sender As System.Object, _  
    ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       ' Determine by checking the Node property of the TreeViewEventArgs.  
       MessageBox.Show(e.Node.Text)  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,   
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       // Determine by checking the Text property.  
       MessageBox.Show(e.Node.Text);  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          // Determine by checking the Text property.  
          MessageBox::Show(e->Node->Text);  
       }  
    ```  
  
    > [!NOTE]
    >  或者，可以使用 <xref:System.Windows.Forms.Control.MouseDown> 或 <xref:System.Windows.Forms.Control.MouseUp> 事件的 <xref:System.Windows.Forms.MouseEventArgs>，获得单击处的 <xref:System.Drawing.Point> 的 <xref:System.Drawing.Point.X%2A> 和 <xref:System.Drawing.Point.Y%2A> 坐标值。  然后，使用 <xref:System.Windows.Forms.TreeView> 控件的 <xref:System.Windows.Forms.TreeView.GetNodeAt%2A> 方法确定单击了哪个节点。  
  
## 请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)