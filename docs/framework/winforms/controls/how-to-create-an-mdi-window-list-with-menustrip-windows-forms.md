---
title: "如何：使用 MenuStrip 创建 MDI 窗口列表（Windows 窗体） | Microsoft Docs"
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
  - "MDI, 创建窗口列表"
  - "MenuStrip 控件 [Windows 窗体], 创建窗口列表"
ms.assetid: 04fb414b-811f-4a83-aab6-b4a24646dec5
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用 MenuStrip 创建 MDI 窗口列表（Windows 窗体）
使用多文档界面 \(MDI\) 创建能同时打开几个文档并将内容从一个文档复制和粘贴到另一个文档的应用程序。  
  
 该过程演示如何在父窗体的“窗口”菜单上创建所有活动子窗体的列表。  
  
### 在 MenuStrip 上创建 MDI 窗口列表  
  
1.  创建一个窗体并将其 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 属性设置为 `true`。  
  
2.  将一个 <xref:System.Windows.Forms.MenuStrip> 添加到窗体中。  
  
3.  将两个顶级菜单项添加到 <xref:System.Windows.Forms.MenuStrip> 并将其 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为 `&File` 和 `&Window`。  
  
4.  将一个子菜单项添加到 `&File` 菜单项，并将其 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&Open`。  
  
5.  设置 <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 属性设置为 `&Window`<xref:System.Windows.Forms.ToolStripMenuItem>。  
  
6.  将一个窗体添加到项目，并向该窗体添加您需要的控件，例如另一个 <xref:System.Windows.Forms.MenuStrip>。  
  
7.  创建 `&New`<xref:System.Windows.Forms.ToolStripMenuItem>的 <xref:System.Windows.Forms.Control.Click> 事件的事件处理程序。  
  
8.  在该事件处理程序内，插入类似于下列的代码，以创建和显示作为 `Form1` 的 MDI 子级的 `Form2` 新实例：  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As _  
    System.Object, ByVal e As System.EventArgs) Handles _  
    openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
     \[C\#\]  
  
    ```  
    private void newToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
9. 将以下代码在 `&New`<xref:System.Windows.Forms.ToolStripMenuItem> 以注册事件处理程序。  
  
    ```vb  
    Private Sub newToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles newToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.newToolStripMenuItem.Click += new System.EventHandler(this.newToolStripMenuItem_Click);  
  
    ```  
  
## 编译代码  
 此示例需要：  
  
-   名为 `Form1` 和 `Form2` 的两个 <xref:System.Windows.Forms.Form> 控件。  
  
-   位于 `Form1` 上的名为 `menuStrip1` 的 <xref:System.Windows.Forms.MenuStrip> 控件，和位于 `Form2` 上的名为 `menuStrip2` 的 <xref:System.Windows.Forms.MenuStrip> 控件。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [MenuStrip 控件](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)