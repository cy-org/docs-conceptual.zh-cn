---
title: "如何：将 MenuStrip 插入 MDI 下拉菜单（Windows 窗体） | Microsoft Docs"
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
  - "MDI, 合并菜单项"
  - "MenuStrip 控件 [Windows 窗体], 插入"
  - "MenuStrip 控件 [Windows 窗体], 合并"
ms.assetid: 0fad444e-26d9-49af-8860-044d9c10d608
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：将 MenuStrip 插入 MDI 下拉菜单（Windows 窗体）
在某些应用程序中，多文档界面 \(MDI\) 子窗口的类型可能与 MDI 父窗口的类型不同。  例如，MDI 父窗口可能为电子表格，而 MDI 子窗口可能为图表。  在这种情况下，您需要在不同类型的 MDI 子窗口被激活时，用 MDI 子窗口的菜单内容更新 MDI 父窗口的菜单内容。  
  
 下面的过程使用 <xref:System.Windows.Forms.Form.IsMdiContainer%2A>、<xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>、<xref:System.Windows.Forms.MergeAction> 和 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 属性将 MDI 子菜单的一组菜单项插入到 MDI 父菜单的下拉部分。  关闭 MDI 子窗口可以将插入的菜单项从 MDI 父窗口移除。  
  
### 将 MenuStrip 插入到 MDI 下拉菜单中  
  
1.  创建一个窗体并将其 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 属性设置为 `true`。  
  
2.  将一个 <xref:System.Windows.Forms.MenuStrip> 添加到 `Form1` 中并将 <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 属性设置为 `true`。  
  
3.  将顶级菜单项添加到 `Form1` <xref:System.Windows.Forms.MenuStrip> 中，并将其 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为 `&File`。  
  
4.  将三个子菜单项添加到 `&File` 菜单项中，并将它们的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&Open`、`&Import from` 和 `E&xit`。  
  
5.  将两个子菜单项添加到 `&Import from` 子菜单项，并将它们的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&Word` 和 `&Excel`。  
  
6.  将一个窗体添加到项目中，将一个 <xref:System.Windows.Forms.MenuStrip> 添加到该窗体，并将 `Form2` <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 属性设置为 `true`。  
  
7.  将顶级菜单项添加到 `Form2` <xref:System.Windows.Forms.MenuStrip> 中，并将其 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&File`。  
  
8.  将子菜单项按照以下顺序添加到 `Form2` 的 `&File` 菜单：<xref:System.Windows.Forms.ToolStripSeparator>、`&Save`、`&Close` `and Save` 和另一个 <xref:System.Windows.Forms.ToolStripSeparator>。  
  
9. 设置 `Form2` 菜单项的 <xref:System.Windows.Forms.MergeAction> 和 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 属性，如下表所示。  
  
    |Form2 菜单项|MergeAction 值|MergeIndex 值|  
    |---------------|-------------------|------------------|  
    |文件|MatchOnly|\-1|  
    |Separator|Insert|2|  
    |保存|Insert|3|  
    |Save and Close|Insert|4|  
    |Separator|Insert|5|  
  
10. 为 `&Open` <xref:System.Windows.Forms.ToolStripMenuItem> 的 <xref:System.Windows.Forms.Control.Click> 事件创建一个事件处理程序。  
  
11. 在该事件处理程序内，插入类似于下面代码示例的代码，以创建和显示作为 `Form1` 的 MDI 子级的 `Form2` 新实例。  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
12. 将与下面的代码示例类似的代码放置于 `&Open` <xref:System.Windows.Forms.ToolStripMenuItem> 中，以注册事件处理程序。  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new System.EventHandler(this.openToolStripMenuItem_Click);  
  
    ```  
  
## 编译代码  
 此示例需要：  
  
-   名为 `Form1` 和 `Form2` 的两个 <xref:System.Windows.Forms.Form> 控件。  
  
-   位于 `Form1` 上的名为 `menuStrip1` 的 <xref:System.Windows.Forms.MenuStrip> 控件，和位于 `Form2` 上的名为 `menuStrip2` 的 <xref:System.Windows.Forms.MenuStrip> 控件。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)