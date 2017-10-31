---
title: "ToolStrip 技术摘要 | Microsoft Docs"
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
  - "菜单 [Windows 窗体], 技术摘要"
  - "状态栏, 技术摘要"
  - "工具栏 [Windows 窗体], 技术摘要"
  - "ToolStrip 控件 [Windows 窗体], 技术摘要"
ms.assetid: e8d61973-7af9-429f-9df5-05a899c15a7b
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# ToolStrip 技术摘要
本主题概述了 `ToolStrip` 控件及支持其使用的类的相关信息。  
  
 `ToolStrip` 控件及其关联的类提供完整的解决方案用于创建工具栏、状态栏和菜单。  
  
## 命名空间  
 <xref:System.Windows.Forms?displayProperty=fullName>  
  
## 背景  
 借助 `ToolStrip` 控件及其关联的类，可创建外观和行为一致且专业的高级工具栏功能。  与以前的控件相比，`ToolStrip` 控件和类提供了以下改进：  
  
-   更加一致的事件模型。  
  
-   更加一致的设计时行为，包含任务列表和项集合编辑器。  
  
-   具有 `ToolStripManager` 和 `ToolStripRenderer` 的自定义呈现。  
  
-   具有 `ToolStripContainer` 和 `ToolStripPanel` 的内置漂浮（停靠时共享工具区域中的水平或垂直空间）。  
  
-   在设计时和运行时重新排列具有 <xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A> 属性的项。  
  
-   借助 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 属性将项重新定位到溢出菜单。  
  
-   可借助 `ToolStripContainer`、`ToolStripPanel` 和 `ToolStripContentPanel` 完全配置控件位置。  
  
-   使用 `ToolStripControlHost` 承载 `ToolStrip`、传统或自定义控件。  
  
-   使用 `ToolStripPanel` 合并 `ToolStrip` 控件。  
  
 `ToolStrip` 是 `MenuStrip`、`ContextMenuStrip` 和 `StatusStrip` 的可扩展基类。  这些控件是继承常见行为和事件处理的 <xref:System.Windows.Forms.ToolStripItem> 容器，已经过扩展以使每个实现均处理适合的行为。  下表列出了从 <xref:System.Windows.Forms.ToolStripItem> 派生的控件。  基础 `ToolStrip` 类处理这些控件的绘制、用户输入和拖放事件。  
  
 `ToolStrip`、`MenuStrip`、`ContextMenuStrip` 和 `StatusStrip` 控件替换以前的工具栏、菜单、快捷菜单和状态栏控件（尽管这些控件将保留用于向后兼容）。  
  
## ToolStrip 类简介  
 下表列出了按技术范围分组的 ToolStrip 类。  
  
|技术范围|类|  
|----------|-------|  
|工具栏、状态和菜单容器|<xref:System.Windows.Forms.ToolStrip><br /><br /> <xref:System.Windows.Forms.MenuStrip><br /><br /> <xref:System.Windows.Forms.ContextMenuStrip><br /><br /> <xref:System.Windows.Forms.StatusStrip><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownMenu>|  
|ToolStrip 项|<xref:System.Windows.Forms.ToolStripLabel><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownItem><br /><br /> <xref:System.Windows.Forms.ToolStripMenuItem><br /><br /> <xref:System.Windows.Forms.ToolStripButton><br /><br /> <xref:System.Windows.Forms.ToolStripStatusLabel><br /><br /> <xref:System.Windows.Forms.ToolStripSeparator><br /><br /> <xref:System.Windows.Forms.ToolStripControlHost><br /><br /> <xref:System.Windows.Forms.ToolStripComboBox><br /><br /> <xref:System.Windows.Forms.ToolStripTextBox><br /><br /> <xref:System.Windows.Forms.ToolStripProgressBar><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownButton><br /><br /> <xref:System.Windows.Forms.ToolStripSplitButton>|  
|位置|<xref:System.Windows.Forms.ToolStripContainer><br /><br /> <xref:System.Windows.Forms.ToolStripContentPanel><br /><br /> <xref:System.Windows.Forms.ToolStripPanel>|  
|演示和呈现|<xref:System.Windows.Forms.ToolStripManager><br /><br /> <xref:System.Windows.Forms.ToolStripRenderer><br /><br /> <xref:System.Windows.Forms.ToolStripProfessionalRenderer><br /><br /> <xref:System.Windows.Forms.ToolStripRenderMode><br /><br /> <xref:System.Windows.Forms.ToolStripManagerRenderMode>|  
  
## ToolStrip 设计时功能  
 <xref:System.Windows.Forms.ToolStrip> 系列的控件提供了一组丰富的工具和模板，用于就地编辑和定义用户界面基础，以便快速创建工作应用程序。  
  
### 任务对话框  
 在 Visual Studio 中，单击设计器中控件上的智能标记会显示任务列表，用于方便访问很多常用命令。  
  
-   [“MenuStrip 任务”对话框](http://msdn.microsoft.com/library/ms233645\(v=vs.110\))  
  
-   [“ToolStrip 任务”对话框](http://msdn.microsoft.com/library/ms233648\(v=vs.110\))  
  
-   [“ContextMenuStrip 任务”对话框](http://msdn.microsoft.com/library/ms233646\(v=vs.110\))  
  
-   [“StatusStrip 任务”对话框](http://msdn.microsoft.com/library/ms233642\(v=vs.110\))  
  
-   [“ToolStripContainer 任务”对话框](http://msdn.microsoft.com/library/ms233647\(v=vs.110\))  
  
### 项集合编辑器  
 在 Visual Studio 中，当单击任务列表上的“编辑项目”或在快捷菜单中右键单击控件并选择“编辑项目”时，将显示控件的集合编辑器。  集合编辑器用于添加、删除和重新排序控件中所包含的项。  还可以查看和更改控件及其内含项的属性。  
  
-   [MenuStrip 项集合编辑器](http://msdn.microsoft.com/library/ms233625\(v=vs.110\))  
  
-   [StatusStrip 项集合编辑器](http://msdn.microsoft.com/library/ms233631\(v=vs.110\))  
  
-   [ContextMenuStrip 项集合编辑器](http://msdn.microsoft.com/library/ms233641\(v=vs.110\))  
  
-   [ToolStrip 项集合编辑器](http://msdn.microsoft.com/library/ms233643\(v=vs.110\))  
  
## 承载控件  
 <xref:System.Windows.Forms.ToolStripControlHost> 类为 <xref:System.Windows.Forms.ToolStripComboBox>、<xref:System.Windows.Forms.ToolStripTextBox> 和 <xref:System.Windows.Forms.ToolStripProgressBar> 控件提供了内置包装。  还可以在 <xref:System.Windows.Forms.ToolStripControlHost> 中承载任何其他现有控件或 COM 控件。  
  
 有关控件承载的示例，请参阅[如何：使用 ToolStripControlHost 包装 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-wrap-a-windows-forms-control-with-toolstripcontrolhost.md)。  
  
## 呈现  
 <xref:System.Windows.Forms.ToolStrip> 类实现明显不同于其他 Windows 窗体控件的呈现方案。  借助此方案，可轻松地应用样式和主题。  
  
 若要将样式应用到 <xref:System.Windows.Forms.ToolStrip> 及其内含的所有 <xref:System.Windows.Forms.ToolStripItem> 对象，无需处理每一项的 <xref:System.Windows.Forms.ToolStripItem.Paint> 事件。  而是将 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 属性设置为其中一个 <xref:System.Windows.Forms.ToolStripRenderMode> 值，而不是 <xref:System.Windows.Forms.ToolStripRenderMode>。  或者，可将 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 直接设置为从 <xref:System.Windows.Forms.ToolStripRenderer> 类继承的任意类。  设置此属性将自动设置 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>。  
  
 可以通过将 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 设置为 <xref:System.Windows.Forms.ToolStripRenderMode> 并将 <xref:System.Windows.Forms.ToolStripManager.RenderMode%2A> 或 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A> 属性分别设置为想要的 <xref:System.Windows.Forms.ToolStripManagerRenderMode> 或 <xref:System.Windows.Forms.ToolStripRenderer> 值，可以将同一样式应用到同一应用程序中的多个 <xref:System.Windows.Forms.ToolStrip> 对象中。  
  
 有关呈现的示例，请参阅[如何：在 Windows 窗体中为 ToolStrip 控件创建和设置自定义呈现器](../../../../docs/framework/winforms/controls/create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)。  
  
## 样式和主题  
 <xref:System.Windows.Forms.ToolStrip> 和关联的类提供一种了支持视觉样式和自定义外观且无需重写每个项的 <xref:System.Windows.Forms.ToolStripItem.OnPaint%2A> 方法的简单方式。  使用 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A><xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 和 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 属性。  
  
## 漂浮和停靠  
 可以飘浮、停靠或绝对定位 <xref:System.Windows.Forms.ToolStrip> 控件。  <xref:System.Windows.Forms.ToolStrip> 项由容器的 <xref:System.Windows.Forms.ToolStrip.LayoutEngine%2A> 进行布局。  
  
 *漂流*指工具栏共享水平或垂直空间的功能。  Windows 窗体可具有 <xref:System.Windows.Forms.ToolStripContainer>，其中窗体的左侧、右侧、顶部和底部均带有用于定位和漂浮 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件的面板。  如果将多个 <xref:System.Windows.Forms.ToolStrip> 控件放置在 <xref:System.Windows.Forms.ToolStripContainer> 左侧或右侧，它们会垂直堆叠。  如果将其放置在 <xref:System.Windows.Forms.ToolStripContainer> 顶部或底部，则水平堆叠。  可使用 <xref:System.Windows.Forms.ToolStripContainer> 的中央 <xref:System.Windows.Forms.ToolStripContentPanel> 将传统控件放置在窗体上。  
  
 任何或所有 <xref:System.Windows.Forms.ToolStripContainer> 控件都可在设计时选择且可删除。  <xref:System.Windows.Forms.ToolStripContainer> 可扩展、可折叠的，并可调整大小适应其包含的控件。  
  
 *停靠*指定控件在窗体左侧、右侧、顶部或底部的简单位置。  
  
 相对于停靠，漂浮的优势是 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件可与其他控件共享水平和垂直空间。  
  
 换用漂浮时，大部分的 <xref:System.Windows.Forms.ToolStrip> 控件可与其他控件一样停靠在窗体。  还可以通过将其从 <xref:System.Windows.Forms.ToolStripContainer> 移除并将 `Dock` 属性设置为 `None` 自由指定 <xref:System.Windows.Forms.ToolStrip> 控件在窗体上的位置，或者可通过设置各自的 <xref:System.Windows.Forms.Control.Location%2A> 属性指定它的绝对位置。  请参阅[如何：将 ToolStrip 从 ToolStripContainer 移到窗体上](../../../../docs/framework/winforms/controls/how-to-move-a-toolstrip-out-of-a-toolstripcontainer-onto-a-form.md).  
  
 为提高灵活性（特别是对于多文档界面 \(MDI\) 应用程序）或者在无需使用 <xref:System.Windows.Forms.ToolStripContainer> 的情况下，请使用一个或多个 <xref:System.Windows.Forms.ToolStripPanel> 控件。  <xref:System.Windows.Forms.ToolStripPanel> 提供可停靠空间，用于定位和漂浮 <xref:System.Windows.Forms.ToolStrip> 控件（而不是传统控件）。  默认情况下，<xref:System.Windows.Forms.ToolStripPanel> 不会显示在设计器的“工具箱”中，但可以右键单击“工具箱”将它放在此处，然后单击“选择项”。  与任何其他类一样，也可以编程方式访问 <xref:System.Windows.Forms.ToolStripPanel>。  
  
 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.StatusStrip> 允许项溢出。  这与这些项在 Microsoft Office 工具栏中的操作方式很类似。  
  
## 请参阅  
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)