---
title: "ToolStrip 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "Toolstrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "工具栏 [Windows 窗体]"
  - "工具栏 [Windows 窗体], Windows 窗体的新增功能"
  - "ToolStrip 控件 [Windows 窗体], 关于 ToolStrip 控件"
  - "新增功能 [Windows 窗体], 工具栏"
ms.assetid: 81d067ed-297c-4dad-90de-1bcac15336ec
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# ToolStrip 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ToolStrip> 控件及其关联类提供一个公共框架，用于将用户界面元素组合到工具栏、状态栏和菜单中。  <xref:System.Windows.Forms.ToolStrip> 控件提供丰富的设计时体验，包括就地激活和编辑、自定义布局和漂浮（即工具栏共享水平或垂直空间的能力）。  
  
 尽管 <xref:System.Windows.Forms.ToolStrip> 替换了早期版本的控件并添加了功能，但是仍可以在需要时选择保留 <xref:System.Windows.Forms.ToolBar> 以备向后兼容和将来使用。  
  
## ToolStrip 控件的功能  
 使用 <xref:System.Windows.Forms.ToolStrip> 控件可以：  
  
-   在各容器之间显示公共用户界面。  
  
-   创建易于自定义的常用工具栏，让这些工具栏支持高级用户界面和布局功能，如停靠、漂浮、带文本和图像的按钮、下拉按钮和控件、“溢出”按钮和 <xref:System.Windows.Forms.ToolStrip> 项的运行时重新排序。  
  
-   支持溢出和运行时项重新排序。  如果 <xref:System.Windows.Forms.ToolStrip> 没有足够空间显示界面项，溢出功能会将它们移到下拉菜单中。  
  
-   通过通用呈现模型支持操作系统的典型外观和行为。  
  
-   对所有容器和包含的项进行事件的一致性处理，处理方式与其他控件的事件相同。  
  
-   将项从一个 <xref:System.Windows.Forms.ToolStrip> 拖到另一个 <xref:System.Windows.Forms.ToolStrip> 内。  
  
-   使用 <xref:System.Windows.Forms.ToolStripDropDown> 中的高级布局创建下拉控件及用户界面类型编辑器。  
  
 通过使用 <xref:System.Windows.Forms.ToolStripControlHost> 类来使用 <xref:System.Windows.Forms.ToolStrip> 中的其他控件，并为它们获取 <xref:System.Windows.Forms.ToolStrip> 功能。  
  
 通过使用 <xref:System.Windows.Forms.ToolStripRenderer>、<xref:System.Windows.Forms.ToolStripProfessionalRenderer> 和 <xref:System.Windows.Forms.ToolStripManager> 以及 <xref:System.Windows.Forms.ToolStripRenderMode> 枚举和 <xref:System.Windows.Forms.ToolStripManagerRenderMode> 枚举，可以扩展此功能并修改外观和行为。  
  
 <xref:System.Windows.Forms.ToolStrip> 控件为高度可配置的、可扩展的控件，它提供了许多属性、方法和事件，可用来自定义外观和行为。  以下为一些值得注意的成员：  
  
### 重要的 ToolStrip 成员  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.ToolStrip.Dock%2A>|获取或设置 <xref:System.Windows.Forms.ToolStrip> 停靠在父容器的哪一边缘。|  
|<xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A>|获取或设置一个值，让该值指示拖放和项重新排序是否专门由 <xref:System.Windows.Forms.ToolStrip> 类进行处理。|  
|<xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>|获取或设置一个值，让该值指示 <xref:System.Windows.Forms.ToolStrip> 如何对其项进行布局。|  
|<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>|获取或设置是将 <xref:System.Windows.Forms.ToolStripItem> 附加到 <xref:System.Windows.Forms.ToolStrip>，附加到 <xref:System.Windows.Forms.ToolStripOverflowButton>，还是让它在这两者之间浮动。|  
|<xref:System.Windows.Forms.ToolStrip.IsDropDown%2A>|获取一个值，该值指示单击 <xref:System.Windows.Forms.ToolStripItem> 时，<xref:System.Windows.Forms.ToolStripItem> 是否显示下拉列表中的其他项。|  
|<xref:System.Windows.Forms.ToolStrip.OverflowButton%2A>|获取 <xref:System.Windows.Forms.ToolStripItem>，它是启用了溢出的 <xref:System.Windows.Forms.ToolStrip> 的“溢出”按钮。|  
|<xref:System.Windows.Forms.ToolStrip.Renderer%2A>|获取或设置一个 <xref:System.Windows.Forms.ToolStripRenderer>，用于自定义 <xref:System.Windows.Forms.ToolStrip> 的外观和行为（外观）。|  
|<xref:System.Windows.Forms.ToolStrip.RenderMode%2A>|获取或设置要应用于 <xref:System.Windows.Forms.ToolStrip> 的绘制样式。|  
|<xref:System.Windows.Forms.ToolStrip.RendererChanged>|当 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 属性更改时引发。|  
  
 通过使用多个伴随类可以实现 <xref:System.Windows.Forms.ToolStrip> 控件的灵活性。  以下为一些最值得注意的伴随类：  
  
### 重要的 ToolStrip 伴随类  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.MenuStrip>|替换 <xref:System.Windows.Forms.MainMenu> 类并添加功能。|  
|<xref:System.Windows.Forms.StatusStrip>|替换 <xref:System.Windows.Forms.StatusBar> 类并添加功能。|  
|<xref:System.Windows.Forms.ContextMenuStrip>|替换 <xref:System.Windows.Forms.ContextMenu> 类并添加功能。|  
|<xref:System.Windows.Forms.ToolStripItem>|抽象基类，它管理 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.ToolStripControlHost> 或 <xref:System.Windows.Forms.ToolStripDropDown> 可以包含的所有元素的事件和布局。|  
|<xref:System.Windows.Forms.ToolStripContainer>|提供一个容器，在该容器中窗体的每一侧均带有一个面板，面板中的控件可以按多种方式排列。|  
|<xref:System.Windows.Forms.ToolStripRenderer>|处理 <xref:System.Windows.Forms.ToolStrip> 对象的绘制功能。|  
|<xref:System.Windows.Forms.ToolStripProfessionalRenderer>|提供 Microsoft Office 样式的外观。|  
|<xref:System.Windows.Forms.ToolStripManager>|控制 <xref:System.Windows.Forms.ToolStrip> 的呈现和漂浮，以及 <xref:System.Windows.Forms.MenuStrip>、<xref:System.Windows.Forms.ToolStripDropDownMenu> 和 <xref:System.Windows.Forms.ToolStripMenuItem> 对象的合并。|  
|<xref:System.Windows.Forms.ToolStripManagerRenderMode>|指定应用于窗体中的多个 <xref:System.Windows.Forms.ToolStrip> 对象的绘制样式（自定义、Windows XP 或 Microsoft Office Professional）。|  
|<xref:System.Windows.Forms.ToolStripRenderMode>|指定应用于窗体中的一个 <xref:System.Windows.Forms.ToolStrip> 对象的绘制样式（自定义、Windows XP 或 Microsoft Office Professional）。|  
|<xref:System.Windows.Forms.ToolStripControlHost>|承载不是明确的 <xref:System.Windows.Forms.ToolStrip> 控件、但您需要为其提供 <xref:System.Windows.Forms.ToolStrip> 功能的其他控件。|  
|<xref:System.Windows.Forms.ToolStripItemPlacement>|指定是在主 <xref:System.Windows.Forms.ToolStrip> 中对 <xref:System.Windows.Forms.ToolStripItem> 进行布局，是在溢出 <xref:System.Windows.Forms.ToolStrip> 中对它进行布局，还是都不进行布局。|  
  
 有关更多信息，请参见[ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)和 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripDropDown>