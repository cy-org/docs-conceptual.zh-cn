---
title: "演练：创建具有专业样式的 ToolStrip 控件 | Microsoft Docs"
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
  - "工具栏 [Windows 窗体], 演练"
  - "ToolStrip 控件 [Windows 窗体], 创建具有专业风格的控件"
  - "ToolStripProfessionalRenderer 类 [Windows 窗体]"
  - "ToolStripRenderer 类 [Windows 窗体]"
ms.assetid: b52339ae-f1d3-494e-996e-eb455614098a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 演练：创建具有专业样式的 ToolStrip 控件
可以为应用程序的 <xref:System.Windows.Forms.ToolStrip> 控件提供专业的外观和行为，方法是编写从 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 类型派生的您自己的类。  
  
 本演练演示如何使用 <xref:System.Windows.Forms.ToolStrip> 控件创建类似于 Microsoft® Outlook® 提供的**“导航窗格”**的复合控件。  本演练演示了以下任务：  
  
-   创建一个 Windows 控件库项目。  
  
-   设计 StackView 控件。  
  
-   实现自定义呈现器。  
  
 完成后，您将拥有可重用的自定义客户端控件，该控件具有 Microsoft Office® XP 控件的专业外观。  
  
 若要将本主题中的代码复制为单个列表，请参见[如何：创建具有专业样式的 ToolStrip 控件](../../../../docs/framework/winforms/controls/how-to-create-a-professionally-styled-toolstrip-control.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足以在安装了 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 的计算机上创建和运行 Windows 窗体应用程序项目的权限。  
  
## 创建 Windows 控件库项目  
 第一步是创建控件库项目。  
  
#### 创建控件库项目  
  
1.  创建一个名为 `StackViewLibrary` 的新的 Windows 控件库项目。  
  
2.  在**“解决方案资源管理器”**中，通过删除名为“UserControl1.cs”或“UserControl1.vb”的源文件来删除项目的默认控件，具体删除哪个源文件取决于您选择的语言。  
  
     有关更多信息，请参见[NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/zh-cn/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73)。  
  
3.  向**“StackViewLibrary”**项目添加新的 <xref:System.Windows.Forms.UserControl> 项。  将新源文件的基名称命名为 `StackView`。  
  
## 设计 StackView 控件  
 `StackView` 控件是具有一个子 <xref:System.Windows.Forms.ToolStrip> 控件的复合控件。  有关复合控件的更多信息，请参见 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)。  
  
#### 设计 StackView 控件  
  
1.  将 <xref:System.Windows.Forms.ToolStrip> 控件从**“工具箱”**中拖动到设计图面。  
  
2.  在**“属性”**窗口中，根据下表设置 <xref:System.Windows.Forms.ToolStrip> 控件的属性。  
  
    |属性|值|  
    |--------|-------|  
    |名称|`stackStrip`|  
    |CanOverflow|`false`|  
    |Dock|<xref:System.Windows.Forms.DockStyle>|  
    |字体|`Tahoma, 10pt, style=Bold`|  
    |GripStyle|<xref:System.Windows.Forms.ToolStripGripStyle>|  
    |LayoutStyle|<xref:System.Windows.Forms.ToolStripLayoutStyle>|  
    |填充|`0, 7, 0, 0`|  
    |RenderMode|<xref:System.Windows.Forms.ToolStripRenderMode>|  
  
3.  在 Windows 窗体设计器中，单击 <xref:System.Windows.Forms.ToolStrip> 控件的**“添加”**按钮并向 `stackStrip` 控件添加一个 <xref:System.Windows.Forms.ToolStripButton>。  
  
4.  在**“属性”**窗口中，根据下表设置 <xref:System.Windows.Forms.ToolStripButton> 控件的属性。  
  
    |属性|值|  
    |--------|-------|  
    |名称|`mailStackButton`|  
    |CheckOnClick|true|  
    |CheckState|<xref:System.Windows.Forms.CheckState>|  
    |DisplayStyle|<xref:System.Windows.Forms.ToolStripItemDisplayStyle>|  
    |ImageAlign|<xref:System.Drawing.ContentAlignment>|  
    |ImageScaling|<xref:System.Windows.Forms.ToolStripItemImageScaling>|  
    |ImageTransparentColor|`238, 238, 238`|  
    |Margin|`0, 0, 0, 0`|  
    |填充|`3, 3, 3, 3`|  
    |Text|邮件|  
    |TextAlign|<xref:System.Drawing.ContentAlignment>|  
  
5.  对于另外三个 <xref:System.Windows.Forms.ToolStripButton> 控件，请重复步骤 7。  
  
     为控件 `calendarStackButton`、`contactsStackButton` 和 `tasksStackButton` 命名。  将 <xref:System.Windows.Forms.Control.Text%2A> 属性值分别设置为“日历”、“联系人”和“任务”。  
  
## 处理事件  
 为使 `StackView` 控件正常运行，有两个事件非常重要。  处理 <xref:System.Windows.Forms.UserControl.Load> 事件可正确定位控件。  处理每个 <xref:System.Windows.Forms.ToolStripButton> 的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件可使 `StackView` 控件的状态行为类似于 <xref:System.Windows.Forms.RadioButton> 控件。  
  
#### 处理事件  
  
1.  在 Windows 窗体设计器中，选择 `StackView` 控件。  
  
2.  在**“属性”**窗口中，单击**“事件”**。  
  
3.  双击 Load 事件以生成 `StackView_Load` 事件处理程序。  
  
4.  在 `StackView_Load` 事件处理程序中，复制并粘贴下面的代码。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#3)]  
  
5.  在 Windows 窗体设计器中，选择 `mailStackButton` 控件。  
  
6.  在**“属性”**窗口中，单击**“事件”**。  
  
7.  双击“Click”事件。  
  
     Windows 窗体设计器将生成 `mailStackButton_Click` 事件处理程序。  
  
8.  将 `mailStackButton_Click` 事件处理程序重命名为 `stackButton_Click`。  
  
     有关更多信息，请参见[How to: Rename an Identifier \(Visual Basic\)](http://msdn.microsoft.com/zh-cn/e5a5edf8-3dba-4119-81f4-fc2aba180e0c)。  
  
9. 将下面的代码插入到 `stackButton_Click` 事件处理程序中。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#4)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#4)]  
  
10. 在 Windows 窗体设计器中，选择 `calendarStackButton` 控件。  
  
11. 在**“属性”**窗口中，将“Click”事件设置为 `stackButton_Click` 事件处理程序。  
  
12. 对 `contactsStackButton` 和 `tasksStackButton` 控件重复步骤 10 和 11。  
  
## 定义图标  
 每个 `StackView` 按钮都有一个关联的图标。  为方便起见，每个图标都表示为以 Base64 编码的字符串，在根据该字符串创建 <xref:System.Drawing.Bitmap> 之前，将反序列化该字符串。  在生产环境中，位图数据将作为资源存储，图标将显示在 Windows 窗体设计器中。  有关更多信息，请参见[How to: Add Background Images to Windows Forms](http://msdn.microsoft.com/zh-cn/7a509ba2-055c-4ae6-b88a-54625c6d9aff)。  
  
#### 定义图标  
  
1.  在代码编辑器中，将以下代码插入到 `StackView` 类定义中。  此代码初始化 <xref:System.Windows.Forms.ToolStripButton> 图标的位图。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#2)]  
  
2.  在 `StackView` 类构造函数中添加对 `InitializeImages` 方法的调用。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## 实现自定义呈现器  
 通过实现从 <xref:System.Windows.Forms.ToolStripRenderer> 类中派生的类，可以自定义 `StackView` 控件的大多数元素。  在此过程中，将会实现 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 类，该类用于自定义手柄并绘制 <xref:System.Windows.Forms.ToolStripButton> 控件的渐变背景。  
  
#### 实现自定义呈现器  
  
1.  将下面的代码插入到 `StackView` 控件定义中。  
  
     这是 `StackRenderer` 类的定义，该定义重写了 <xref:System.Windows.Forms.ToolStripRenderer.RenderGrip>、<xref:System.Windows.Forms.ToolStripRenderer.RenderToolStripBorder> 和 <xref:System.Windows.Forms.ToolStripRenderer.RenderButtonBackground> 方法以产生自定义外观。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#10)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#10)]  
  
2.  在 `StackView` 控件的构造函数中创建 `StackRenderer` 类的新实例，并将此实例分配给 `stackStrip` 控件的 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 属性。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## 测试 StackView 控件  
 `StackView` 控件从 <xref:System.Windows.Forms.UserControl> 类中派生。  因此，可以使用**“UserControl 测试容器”**测试控件。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
#### 测试 StackView 控件  
  
1.  按 F5 以生成项目并启动**“UserControl 测试容器”**。  
  
2.  将指针移到 `StackView` 控件的按钮上方，然后单击任一按钮以查看其选定状态的外观。  
  
## 后续步骤  
 在本演练中，您已经创建了具有 Office XP 控件专业外观的可重用自定义客户端控件。  <xref:System.Windows.Forms.ToolStrip> 系列控件有很多其他用途：  
  
-   使用 <xref:System.Windows.Forms.ContextMenuStrip> 来创建控件的快捷菜单。  有关更多信息，请参见 [ContextMenu 组件概述](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md)。  
  
-   创建一个自动填充有标准菜单的窗体。  有关更多信息，请参见 [演练：向窗体提供标准菜单项](../../../../docs/framework/winforms/controls/walkthrough-providing-standard-menu-items-to-a-form.md)。  
  
-   创建包含停靠的 <xref:System.Windows.Forms.ToolStrip> 控件的多文档界面 \(MDI\) 窗体。  有关更多信息，请参见[如何：创建合并了菜单并具有 ToolStrip 控件的 MDI 窗体](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [ToolStrip 控件](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)   
 [如何：向窗体提供标准菜单项](../../../../docs/framework/winforms/controls/how-to-provide-standard-menu-items-to-a-form.md)