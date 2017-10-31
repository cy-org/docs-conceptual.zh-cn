---
title: "ContextMenu 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "ContextMenu"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "上下文菜单, ContextMenu 组件"
  - "ContextMenu 组件 [Windows 窗体], 关于 ContextMenu 组件"
  - "快捷菜单, ContextMenu 组件"
ms.assetid: 49d6398f-d3c4-4679-84fa-1de07b68b05e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# ContextMenu 组件概述（Windows 窗体）
> [!IMPORTANT]
>  尽管 <xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 取代了早期版本的 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 控件并添加了功能，但是，可以选择保留 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 以实现向后兼容并供将来使用。  
  
 通过使用 Windows 窗体的 <xref:System.Windows.Forms.ContextMenu> 组件，您可以针对与所选对象相关联的常用命令为用户提供易于访问的快捷菜单。  快捷菜单项常常是在应用程序其他位置出现的主菜单项的子集。  用户通常可以单击鼠标右键来访问快捷菜单。  在 Windows 窗体上，快捷菜单是和控件相关联的。  
  
## 主要属性  
 可以使快捷菜单与控件相关联，方法是将控件的 <xref:System.Windows.Forms.Control.ContextMenu%2A> 属性设置为 <xref:System.Windows.Forms.ContextMenu> 组件。  单个快捷菜单可以与多个控件相关联，但每个控件只能有一个快捷菜单。  
  
 <xref:System.Windows.Forms.ContextMenu> 组件的 key 属性是 <xref:System.Windows.Forms.Menu.MenuItems%2A> 属性。  您可以添加菜单项，方法是以编程方式创建 <xref:System.Windows.Forms.MenuItem> 对象并将它们添加到快捷菜单的 <xref:System.Windows.Forms.Menu.MenuItemCollection> 中。  鉴于快捷菜单中的项通常取自其他菜单，向快捷菜单中添加项的最常用方法是复制这些项。  
  
## 请参阅  
 <xref:System.Windows.Forms.ContextMenu>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>