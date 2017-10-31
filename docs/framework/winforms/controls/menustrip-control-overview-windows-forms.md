---
title: "MenuStrip 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "MenuStrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "菜单, 创建"
  - "MenuStrip 控件 [Windows 窗体], 关于 MenuStrip 控件"
ms.assetid: f45516e5-bf01-4468-b851-d45f4c33c055
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# MenuStrip 控件概述（Windows 窗体）
菜单通过存放按照一般主题分组的命令将功能公开给用户。  
  
 <xref:System.Windows.Forms.MenuStrip> 控件是此版本的 Visual Studio 和 .NET Framework 中的新功能。  使用该控件，可以轻松创建 Microsoft Office 中那样的菜单。  
  
 <xref:System.Windows.Forms.MenuStrip> 控件支持多文档界面 \(MDI\) 和菜单合并、工具提示和溢出。  您可以通过添加访问键、快捷键、选中标记、图像和分隔条，来增强菜单的可用性和可读性。  
  
 <xref:System.Windows.Forms.MenuStrip> 控件取代了 <xref:System.Windows.Forms.MainMenu> 控件并向其中添加了功能；但是也可选择保留 <xref:System.Windows.Forms.MainMenu> 控件以备向后兼容和将来使用。  
  
## MenuStrip 控件的使用方式  
 使用 <xref:System.Windows.Forms.MenuStrip> 控件可以：  
  
-   创建支持高级用户界面和布局功能的易自定义的常用菜单，例如文本和图像排序和对齐、拖放操作、MDI、溢出和访问菜单命令的其他模式。  
  
-   支持操作系统的典型外观和行为。  
  
-   对所有容器和包含的项进行事件的一致性处理，处理方式与其他控件的事件相同。  
  
 下表显示了 <xref:System.Windows.Forms.MenuStrip> 和关联类的一些特别重要的属性。  
  
|属性|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A>|获取或设置用于显示 MDI 子窗体列表的 <xref:System.Windows.Forms.ToolStripMenuItem>。|  
|<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A?displayProperty=fullName>|获取或设置 MDI 应用程序中子菜单与父菜单合并的方式。|  
|<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A?displayProperty=fullName>|获取或设置 MDI 应用程序的菜单中合并项的位置。|  
|<xref:System.Windows.Forms.Form.IsMdiContainer%2A?displayProperty=fullName>|获取或设置一个值，该值指示窗体是否为 MDI 子窗体的容器。|  
|<xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A>|获取或设置一个值，该值指示是否为 <xref:System.Windows.Forms.MenuStrip> 显示工具提示。|  
|<xref:System.Windows.Forms.MenuStrip.CanOverflow%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.MenuStrip> 是否支持溢出功能。|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>|获取或设置与 <xref:System.Windows.Forms.ToolStripMenuItem> 关联的快捷键。|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>|获取或设置一个值，该值指示与 <xref:System.Windows.Forms.ToolStripMenuItem> 关联的快捷键是否显示在 <xref:System.Windows.Forms.ToolStripMenuItem> 旁边。|  
  
 下表显示了重要的 <xref:System.Windows.Forms.MenuStrip> 伴生类。  
  
|类|说明|  
|-------|--------|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|表示 <xref:System.Windows.Forms.MenuStrip> 或 <xref:System.Windows.Forms.ContextMenuStrip> 上显示的可选选项。|  
|<xref:System.Windows.Forms.ContextMenuStrip>|表示快捷菜单。|  
|<xref:System.Windows.Forms.ToolStripDropDown>|表示当用户单击 <xref:System.Windows.Forms.ToolStripDropDownButton> 或较高级菜单项时，使用户可以从列表中选择单个项的控件。|  
|<xref:System.Windows.Forms.ToolStripDropDownItem>|为派生自 <xref:System.Windows.Forms.ToolStripItem> 的控件提供基本功能，当单击控件时显示下拉项。|  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripDropDown>