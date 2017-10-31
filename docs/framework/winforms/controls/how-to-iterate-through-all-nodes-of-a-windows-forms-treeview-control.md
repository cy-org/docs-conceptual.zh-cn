---
title: "如何：循环访问 Windows 窗体 TreeView 控件的所有节点 | Microsoft Docs"
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
  - "TreeView 控件中的树节点, 循环访问"
  - "TreeView 控件 [Windows 窗体], 循环访问节点"
ms.assetid: 427f8928-ebcf-4beb-887f-695b905d5134
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：循环访问 Windows 窗体 TreeView 控件的所有节点
为了对节点值执行某种运算，查看 Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件中的每个节点有时是很有用的。  利用递归过程（C\# 和 C\+\+ 中为递归方法）可完成此操作，该过程循环访问每个树集合中的每个节点。  
  
 树视图中的每个 <xref:System.Windows.Forms.TreeNode> 对象都具有可用于定位树视图的属性：<xref:System.Windows.Forms.TreeNode.FirstNode%2A>、<xref:System.Windows.Forms.TreeNode.LastNode%2A>、<xref:System.Windows.Forms.TreeNode.NextNode%2A>、<xref:System.Windows.Forms.TreeNode.PrevNode%2A> 以及 <xref:System.Windows.Forms.TreeNode.Parent%2A>。  <xref:System.Windows.Forms.TreeNode.Parent%2A> 属性值是当前节点的父节点。  当前节点如果有子节点，则子节点将列在它的 <xref:System.Windows.Forms.TreeNode.Nodes%2A> 属性中。  <xref:System.Windows.Forms.TreeView> 控件本身具有 <xref:System.Windows.Forms.TreeView.TopNode%2A> 属性，该属性是整个树视图的根节点。  
  
### 循环访问 TreeView 控件的所有节点  
  
1.  创建测试每个节点的递归过程（C\# 和 C\+\+ 中为递归方法）。  
  
2.  调用该过程。  
  
     下面的示例演示如何打印每个 <xref:System.Windows.Forms.TreeNode> 对象的 <xref:System.Windows.Forms.TreeNode.Text%2A> 属性：  
  
    ```vb  
    Private Sub PrintRecursive(ByVal n As TreeNode)  
       System.Diagnostics.Debug.WriteLine(n.Text)  
       MessageBox.Show(n.Text)  
       Dim aNode As TreeNode  
       For Each aNode In n.Nodes  
          PrintRecursive(aNode)  
       Next  
    End Sub  
  
    ' Call the procedure using the top nodes of the treeview.  
    Private Sub CallRecursive(ByVal aTreeView As TreeView)  
       Dim n As TreeNode  
       For Each n In aTreeView.Nodes  
          PrintRecursive(n)  
       Next  
    End Sub  
  
    ```  
  
    ```csharp  
    private void PrintRecursive(TreeNode treeNode)  
    {  
       // Print the node.  
       System.Diagnostics.Debug.WriteLine(treeNode.Text);  
       MessageBox.Show(treeNode.Text);  
       // Print each node recursively.  
       foreach (TreeNode tn in treeNode.Nodes)  
       {  
          PrintRecursive(tn);  
       }  
    }  
  
    // Call the procedure using the TreeView.  
    private void CallRecursive(TreeView treeView)  
    {  
       // Print each node recursively.  
       TreeNodeCollection nodes = treeView.Nodes;  
       foreach (TreeNode n in nodes)  
       {  
          PrintRecursive(n);  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void PrintRecursive( TreeNode^ treeNode )  
       {  
          // Print the node.  
          System::Diagnostics::Debug::WriteLine( treeNode->Text );  
          MessageBox::Show( treeNode->Text );  
  
          // Print each node recursively.  
          System::Collections::IEnumerator^ myNodes = (safe_cast<System::Collections::IEnumerable^>(treeNode->Nodes))->GetEnumerator();  
          try  
          {  
             while ( myNodes->MoveNext() )  
             {  
                TreeNode^ tn = safe_cast<TreeNode^>(myNodes->Current);  
                PrintRecursive( tn );  
             }  
          }  
          finally  
          {  
             IDisposable^ disposable = dynamic_cast<System::IDisposable^>(myNodes);  
             if ( disposable != nullptr )  
                      disposable->Dispose();  
          }  
       }  
  
       // Call the procedure using the TreeView.  
       void CallRecursive( TreeView^ treeView )  
       {  
          // Print each node recursively.  
          TreeNodeCollection^ nodes = treeView->Nodes;  
          System::Collections::IEnumerator^ myNodes = (safe_cast<System::Collections::IEnumerable^>(nodes))->GetEnumerator();  
          try  
          {  
             while ( myNodes->MoveNext() )  
             {  
                TreeNode^ n = safe_cast<TreeNode^>(myNodes->Current);  
                PrintRecursive( n );  
             }  
          }  
          finally  
          {  
             IDisposable^ disposable = dynamic_cast<System::IDisposable^>(myNodes);  
             if ( disposable != nullptr )  
                      disposable->Dispose();  
          }  
       }  
    ```  
  
## 请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [递归过程](../Topic/Recursive%20Procedures%20\(Visual%20Basic\).md)