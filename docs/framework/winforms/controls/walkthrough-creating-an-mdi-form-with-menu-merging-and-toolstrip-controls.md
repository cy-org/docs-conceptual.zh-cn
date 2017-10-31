---
title: "演练：创建具有菜单合并功能和 ToolStrip 控件的 MDI 窗体 | Microsoft Docs"
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
  - "MDI 窗体"
  - "MDI 窗体, 创建"
  - "MDI 窗体, 演练"
  - "MDI, 创建窗体"
  - "多文档界面窗体"
  - "工具栏 [Windows 窗体]"
  - "ToolStrip 控件 [Windows 窗体]"
  - "ToolStripPanel 控件 [Windows 窗体]"
ms.assetid: fbab4221-74af-42d0-bbf4-3c97f7b2e544
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 演练：创建具有菜单合并功能和 ToolStrip 控件的 MDI 窗体
<xref:System.Windows.Forms?displayProperty=fullName> 命名空间支持多文档界面 \(MDI\) 应用程序，<xref:System.Windows.Forms.MenuStrip> 控件支持菜单合并。  MDI 窗体还可支持 <xref:System.Windows.Forms.ToolStrip> 控件。  
  
 本演练演示如何将 <xref:System.Windows.Forms.ToolStripPanel> 控件用于 MDI 窗体。  该窗体还支持与子菜单的菜单合并。  本演练演示了以下任务：  
  
-   创建 Windows 窗体项目。  
  
-   创建窗体的主菜单。  菜单的实际名称将有所不同。  
  
-   将 <xref:System.Windows.Forms.ToolStripPanel> 控件添加到**“工具箱”**中。  
  
-   创建子窗体。  
  
-   按 Z 顺序排列 <xref:System.Windows.Forms.ToolStripPanel> 控件。  
  
 完成这些步骤之后，您会得到一个支持菜单合并和可移动 <xref:System.Windows.Forms.ToolStrip> 控件的 MDI 窗体。  
  
 若要将本主题中的代码作为一个单独的清单进行复制，请参见 [如何：创建合并了菜单并具有 ToolStrip 控件的 MDI 窗体](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足以在安装了 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 的计算机上创建和运行 Windows 窗体应用程序项目的权限。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建名为“MdiForm”的 Windows 应用程序项目。  
  
     有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在 Windows 窗体设计器中，选择该窗体。  
  
3.  在“属性”窗口中，将 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 的值设置为 `true`。  
  
## 创建主菜单  
 父 MDI 窗体包含主菜单。  主菜单有一个名为**“窗口”**的菜单项。  使用**“窗口”**菜单项，可以创建子窗体。  来自子窗体的菜单项将合并到主菜单中。  
  
#### 创建主菜单  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.MenuStrip> 控件拖动到窗体上。  
  
2.  向 <xref:System.Windows.Forms.MenuStrip> 控件添加一个 <xref:System.Windows.Forms.ToolStripMenuItem>，并将其命名为“窗口”。  
  
3.  选择 <xref:System.Windows.Forms.MenuStrip> 控件。  
  
4.  在“属性”窗口中，将 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 属性的值设置为 `ToolStripMenuItem1`。  
  
5.  向**“窗口”**菜单项添加一个子项，并将其命名为“新建”。  
  
6.  在“属性”窗口中，单击**“事件”**。  
  
7.  双击 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。  
  
     Windows 窗体设计器为 <xref:System.Windows.Forms.ToolStripItem.Click> 事件生成一个事件处理程序。  
  
8.  将下面的代码插入到事件处理程序中。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#2)]  
  
## 将 ToolStripPanel 控件添加到工具箱中  
 将 <xref:System.Windows.Forms.MenuStrip> 控件用于 MDI 窗体时，必须具有 <xref:System.Windows.Forms.ToolStripPanel> 控件。  必须在**“工具箱”**中添加 <xref:System.Windows.Forms.ToolStripPanel> 控件，以便在 Windows 窗体设计器中构建 MDI 窗体。  
  
#### 将 ToolStripPanel 控件添加到工具箱中  
  
1.  打开**“工具箱”**并单击**“所有 Windows 窗体”**选项卡，以显示可用的 Windows 窗体控件。  
  
2.  单击右键打开快捷菜单，再选择**“选择项”**。  
  
3.  在**“选择工具箱项”**对话框中，向下滚动**“名称”**列，直到找到**“ToolStripPanel”**。  
  
4.  选择**“ToolStripPanel”**旁边的复选框并单击**“确定”**。  
  
     <xref:System.Windows.Forms.ToolStripPanel> 控件将出现在**“工具箱”**中。  
  
## 创建子窗体  
 在此过程中，您将定义一个单独的子窗体类，其中包含它自己的 <xref:System.Windows.Forms.MenuStrip> 控件。  此窗体的菜单项将与父窗体的菜单项合并。  
  
#### 定义子窗体  
  
1.  向项目中添加一个名为 `ChildForm` 的新窗体。  
  
     有关更多信息，请参见 [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/zh-cn/3d7bb25f-fd90-47cf-9378-fa0d764686c1)。  
  
2.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.MenuStrip> 控件拖动到该子窗体上。  
  
3.  单击 <xref:System.Windows.Forms.MenuStrip> 控件的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“编辑项”**。  
  
4.  在**“项集合编辑器”**对话框中，向子菜单中添加一个名为 ChildMenuItem 的新 <xref:System.Windows.Forms.ToolStripMenuItem>。  
  
     有关更多信息，请参见 [ToolStrip Items Collection Editor](http://msdn.microsoft.com/zh-cn/e681f3ab-94ba-4b2b-ac64-1dfad46caa25)。  
  
## 测试窗体  
  
#### 测试窗体  
  
1.  按 F5 编译并运行窗体。  
  
2.  单击**“窗口”**菜单项打开菜单，然后单击**“新建”**。  
  
     在该窗体的 MDI 工作区中将创建一个新的子窗体。  该子窗体的菜单将与主菜单合并。  
  
3.  关闭子窗体。  
  
     该子窗体的菜单从主菜单中移除。  
  
4.  单击**“新建”**若干次。  
  
     因为指定了 <xref:System.Windows.Forms.MenuStrip> 控件的 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 属性，所以**“窗口”**菜单项下会自动列出子窗体。  
  
## 添加 ToolStrip 支持  
 在此过程中，将向 MDI 父窗体添加四个 <xref:System.Windows.Forms.ToolStrip> 控件。  每个 <xref:System.Windows.Forms.ToolStrip> 控件均被添加到停靠于窗体边缘的一个 <xref:System.Windows.Forms.ToolStripPanel> 控件中。  
  
#### 向 MDI 父窗体添加 ToolStrip 控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.ToolStripPanel> 控件拖动到窗体上。  
  
2.  选择了 <xref:System.Windows.Forms.ToolStripPanel> 控件之后，在**“工具箱”**中双击 <xref:System.Windows.Forms.ToolStrip> 控件。  
  
     在 <xref:System.Windows.Forms.ToolStripPanel> 控件中会创建一个 <xref:System.Windows.Forms.ToolStrip> 控件。  
  
3.  选择 <xref:System.Windows.Forms.ToolStripPanel> 控件。  
  
4.  在“属性”窗口中，将控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性值更改为 <xref:System.Windows.Forms.DockStyle>。  
  
     <xref:System.Windows.Forms.ToolStripPanel> 控件将停靠于窗体的左侧，位于主菜单的下方。  调整 MDI 工作区的大小以容纳该 <xref:System.Windows.Forms.ToolStripPanel> 控件。  
  
5.  重复步骤 1 到 4。  
  
     将新的 <xref:System.Windows.Forms.ToolStripPanel> 控件停靠在窗体的顶部。  
  
     <xref:System.Windows.Forms.ToolStripPanel> 控件停靠于主菜单的下方，但位于第一个 <xref:System.Windows.Forms.ToolStripPanel> 控件的右侧。  此步骤说明 Z 顺序对于正确放置 <xref:System.Windows.Forms.ToolStripPanel> 控件的重要性。  
  
6.  重复步骤 1 到步骤 4 以另外添加两个 <xref:System.Windows.Forms.ToolStripPanel> 控件。  
  
     将这两个新的 <xref:System.Windows.Forms.ToolStripPanel> 控件分别停靠于窗体的右侧和底部。  
  
## 按照 Z 顺序排列 ToolStripPanel 控件  
 <xref:System.Windows.Forms.ToolStripPanel> 控件在 MDI 窗体上的停靠位置由该控件在 Z 顺序中的位置确定。  在“文档大纲”窗口中可以方便地排列控件的 Z 顺序。  
  
#### 按照 Z 顺序排列 ToolStripPanel 控件  
  
1.  单击**“视图”**菜单中的**“其他窗口”**，再选择**“文档大纲”**。  
  
     在上面的过程中，<xref:System.Windows.Forms.ToolStripPanel> 控件的排列是非标准排列。  这是因为 Z 顺序不正确。  请使用“文档大纲”窗口更改控件的 Z 顺序。  
  
2.  在“文档大纲”窗口中，选择**“ToolStripPanel4”**。  
  
3.  重复单击向下箭头按钮，直到将**“ToolStripPanel4”**置于列表底部。  
  
     **“ToolStripPanel4”**控件被停靠于窗体的底部，位于其他控件的下方。  
  
4.  选择**“ToolStripPanel2”**。  
  
5.  单击向下箭头一次，将控件定位在列表中的第三列。  
  
     **“ToolStripPanel2”**控件停靠于窗体的顶部，位于主菜单之下，其他控件之上。  
  
6.  在**“文档大纲”**窗口中选择不同的控件并将它们移动到 Z 顺序中的不同位置。  请注意 Z 顺序对放置停靠控件的影响。  使用 Ctrl\-Z 或**“编辑”**菜单中的**“撤消”**来撤消所做的更改。  
  
## 检查点  
  
#### 测试窗体  
  
1.  按 F5 编译并运行窗体。  
  
2.  单击 <xref:System.Windows.Forms.ToolStrip> 控件的手柄并将控件拖动到窗体中的其他位置。  
  
     可以将 <xref:System.Windows.Forms.ToolStrip> 控件从一个 <xref:System.Windows.Forms.ToolStripPanel> 控件拖动到另一个控件。  
  
## 后续步骤  
 在本演练中，您已经创建了包含 <xref:System.Windows.Forms.ToolStrip> 控件和菜单合并功能的 MDI 父窗体。  <xref:System.Windows.Forms.ToolStrip> 系列控件有很多其他用途：  
  
-   使用 <xref:System.Windows.Forms.ContextMenuStrip> 来创建控件的快捷菜单。  有关更多信息，请参见 [ContextMenu 组件概述](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md)。  
  
-   创建一个自动填充有标准菜单的窗体。  有关更多信息，请参见 [演练：向窗体提供标准菜单项](../../../../docs/framework/winforms/controls/walkthrough-providing-standard-menu-items-to-a-form.md)。  
  
-   赋予 <xref:System.Windows.Forms.ToolStrip> 控件专业的外观。  有关更多信息，请参见 [如何：为应用程序设置 ToolStrip 呈现程序](../../../../docs/framework/winforms/controls/how-to-set-the-toolstrip-renderer-for-an-application.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [如何：将 MenuStrip 插入 MDI 下拉菜单](../../../../docs/framework/winforms/controls/how-to-insert-a-menustrip-into-an-mdi-drop-down-menu-windows-forms.md)   
 [ToolStrip 控件](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)