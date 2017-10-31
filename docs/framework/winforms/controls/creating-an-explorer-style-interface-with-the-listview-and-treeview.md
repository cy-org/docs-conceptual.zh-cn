---
title: "演练：使用设计器创建带有 ListView 和 TreeView 控件的资源管理器样式的界面 | Microsoft Docs"
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
  - "资源管理器样式的应用程序"
  - "资源管理器样式的应用程序, 演练"
  - "ListView 控件 [Windows 窗体], 资源管理器样式界面"
  - "ListView 控件 [Windows 窗体], 资源管理器样式界面"
  - "ListView 控件 [Windows 窗体], 与 TreeView 控件一起使用"
  - "TreeView 控件 [Windows 窗体], 与 ListView 控件一起使用"
  - "TreeView 控件 [Windows 窗体], 用于资源管理器样式界面"
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 演练：使用设计器创建带有 ListView 和 TreeView 控件的资源管理器样式的界面
Visual Studio 的一个优点是能够在短时间内创建具有专业级外观的 Windows 窗体应用程序。  通常情况下，创建一个带有 <xref:System.Windows.Forms.ListView> 和 <xref:System.Windows.Forms.TreeView> 控件的用户界面 \(UI\)，该界面类似于 Windows 操作系统的 Windows 资源管理器。  Windows 资源管理器显示了用户计算机上的文件和文件夹的层次结构。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建包含 ListView 和 TreeView 控件的窗体  
  
1.  在**“文件”**菜单上指向**“新建”**，再单击**“项目”**。  
  
2.  在**“新建项目”**对话框中，请执行以下操作：  
  
    1.  在类别中选择**“Visual Basic”**或**“Visual C\#”**。  
  
    2.  在模板列表中，选择**“Windows 窗体应用程序”**。  
  
3.  单击**“确定”**。  随即便会创建一个新的 Windows 窗体项目。  
  
4.  向该窗体添加一个 <xref:System.Windows.Forms.SplitContainer> 控件，并将其 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
5.  向该窗体中添加一个名为 `imageList1` 的 <xref:System.Windows.Forms.ImageList>，然后使用“属性”窗口按所列顺序添加两个图像：一个文件夹图像和一个文档图像。  
  
6.  向该窗体添加一个名为 `treeview1` 的 <xref:System.Windows.Forms.TreeView> 控件，将其置于 <xref:System.Windows.Forms.SplitContainer> 控件的左侧。  在 `treeView1` 的“属性”窗口中，执行以下操作：  
  
    1.  将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
    2.  将 <xref:System.Windows.Forms.TreeView.ImageList%2A> 属性设置为 `imagelist1`。  
  
7.  向该窗体中添加一个名为 `listView1` 的 <xref:System.Windows.Forms.ListView> 控件，将其置于 <xref:System.Windows.Forms.SplitContainer> 控件的右侧。  在 `listview1` 的“属性”窗口中，执行以下操作：  
  
    1.  将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
    2.  将 <xref:System.Windows.Forms.ListView.View%2A> 属性设置为 <xref:System.Windows.Forms.View>。  
  
    3.  单击 <xref:System.Windows.Forms.ListView.Columns%2A> 属性中的椭圆 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)，以打开 ColumnHeader 集合编辑器。添加三列，并将其 <xref:System.Windows.Forms.ColumnHeader.Text%2A> 属性分别设置为 `Name`、`Type` 和 `Last Modified`。  单击**“确定”**关闭对话框。  
  
    4.  将 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 属性设置为 `imageList1`。  
  
8.  实现代码以便将节点和子节点填充到 <xref:System.Windows.Forms.TreeView> 中。  将该代码添加到 `Form1` 类中。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]  
  
9. 由于以前的代码使用 System.IO 命名空间，因此需要在窗体顶部添加 using 或 import 语句。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]  
  
10. 在窗体的构造函数或 <xref:System.Windows.Forms.Form.Load> 事件处理方法中，调用上一步中的设置方法。  将该代码添加到窗体构造函数中。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]  
  
11. 处理 `treeview1` 的 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 事件，实现代码以便在单击某个节点时，用该节点的内容来填充 `listview1`。  将该代码添加到 `Form1` 类中。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]  
  
     如果使用的是 C\#，请确保将 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 事件与其事件处理方法相关联。  将该代码添加到窗体构造函数中。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]  
  
## 测试应用程序  
 现在可以测试窗体，以确保其行为与预期相同。  
  
#### 测试窗体  
  
-   按 F5 运行该应用程序。  
  
     您将看到一个包含 <xref:System.Windows.Forms.TreeView> 控件的拆分窗体，该窗体左侧显示您的项目目录，右侧是分为三列的 <xref:System.Windows.Forms.ListView> 控件。  选择目录节点可以遍历 <xref:System.Windows.Forms.TreeView>，而 <xref:System.Windows.Forms.ListView> 中将填充选定目录的内容。  
  
## 后续步骤  
 本应用程序举例说明了一种结合使用 <xref:System.Windows.Forms.TreeView> 和 <xref:System.Windows.Forms.ListView> 控件的方式。  有关这些控件的更多信息，请参见下列主题：  
  
-   [如何：向 TreeView 或 ListView 控件添加自定义信息（Windows 窗体）](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)  
  
-   [如何：向 ListView 控件添加搜索功能](../../../../docs/framework/winforms/controls/how-to-add-search-capabilities-to-a-listview-control.md)  
  
-   [如何：将快捷菜单附加到 TreeView 节点](../../../../docs/framework/winforms/controls/how-to-attach-a-shortcut-menu-to-a-treeview-node.md)  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.TreeView>   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [如何：添加和删除 Windows 窗体 TreeView 控件中的节点](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)   
 [如何：使用 Windows 窗体 ListView 控件添加和移除项](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [如何：向 Windows 窗体 ListView 控件中添加列](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)