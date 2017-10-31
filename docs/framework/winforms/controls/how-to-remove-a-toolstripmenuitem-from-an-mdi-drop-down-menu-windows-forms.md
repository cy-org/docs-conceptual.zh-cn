---
title: "如何：从 MDI 下拉菜单移除 ToolStripMenuItem（Windows 窗体） | Microsoft Docs"
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
  - "菜单项, 从 MDI 下拉菜单中移除"
  - "MenuStrip 控件 [Windows 窗体], 合并"
  - "MenuStrip 控件 [Windows 窗体], 移除"
ms.assetid: bdafe60d-82ee-45bc-97fe-eeefca6e54c1
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：从 MDI 下拉菜单移除 ToolStripMenuItem（Windows 窗体）
在某些应用程序中，多文档界面 \(MDI\) 子窗口的类型可能与 MDI 父窗口的类型不同。  例如，MDI 父窗口可能为电子表格，而 MDI 子窗口可能为图表。  在这种情况下，您需要在不同类型的 MDI 子窗口被激活时，用 MDI 子窗口的菜单内容更新 MDI 父窗口的菜单内容。  
  
 下面的过程使用 <xref:System.Windows.Forms.Form.IsMdiContainer%2A>、<xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>、<xref:System.Windows.Forms.MergeAction> 和 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 属性从 MDI 父菜单的下拉部分移除菜单项。  关闭 MDI 子窗口会将移除的菜单项还原到 MDI 父菜单中。  
  
### 从 MDI 下拉菜单移除 MenuStrip  
  
1.  创建一个窗体并将其 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 属性设置为 `true`。  
  
2.  将一个 <xref:System.Windows.Forms.MenuStrip> 添加到 `Form1` 中并将 <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 属性设置为 `true`。  
  
3.  将顶级菜单项添加到 `Form1`<xref:System.Windows.Forms.MenuStrip> 并将其 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为 `&File`。  
  
4.  将三个子菜单项添加到 `&File` 菜单项中，并将它们的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&Open`、`&Import from` 和 `E&xit`。  
  
5.  将两个子菜单项添加到 `&Import from` 子菜单项，并将它们的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&Word` 和 `&Excel`。  
  
6.  将一个窗体添加到项目中，添加 <xref:System.Windows.Forms.MenuStrip> 到窗体中，并将 `Form2`<xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 属性设置为 `true`。  
  
7.  将顶级菜单项添加到 `Form2`<xref:System.Windows.Forms.MenuStrip> 并将其 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性设置为 `&File`。  
  
8.  将 `&Import from` 子菜单项添加到 `Form2` 的 `&File` 菜单，并将 `&Word` 子菜单项添加到 `&File` 菜单。  
  
9. 设置 `Form2` 菜单项的 <xref:System.Windows.Forms.MergeAction> 和 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 属性，如下表所示。  
  
    |Form2 菜单项|MergeAction 值|MergeIndex 值|  
    |---------------|-------------------|------------------|  
    |文件|MatchOnly|\-1|  
    |导入自|MatchOnly|\-1|  
    |Word|移除|\-1|  
  
10. 在 `Form1`，请创建 `&Open`<xref:System.Windows.Forms.ToolStripMenuItem>的 <xref:System.Windows.Forms.Control.Click> 事件的事件处理程序。  
  
11. 在该事件处理程序内，插入类似于下面代码示例的代码，以创建和显示作为 `Form1` 的 MDI 子级的 `Form2` 新实例：  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
     \[C\#\]  
  
    ```  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
12. 使代码与 `&Open`<xref:System.Windows.Forms.ToolStripMenuItem> 下面的代码示例应用于注册事件处理程序。  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new _  
    System.EventHandler(this.openToolStripMenuItem_Click);  
  
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