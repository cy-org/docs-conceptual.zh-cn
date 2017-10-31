---
title: "MainMenu 组件概述（Windows 窗体） | Microsoft Docs"
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
  - "MenuItem"
  - "MainMenu"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "MainMenu 控件 [Windows 窗体], 关于 MainMenu 控件"
  - "菜单"
ms.assetid: b41cc5a3-cc59-4996-aa3c-8dd9c17d3c90
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# MainMenu 组件概述（Windows 窗体）
> [!IMPORTANT]
>  尽管 <xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 取代了早期版本的 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 控件并添加了功能，但是，可以选择保留 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 以实现向后兼容并供将来使用。  
  
 Windows 窗体 <xref:System.Windows.Forms.MainMenu> 组件在运行时显示一个菜单。  主菜单的所有子菜单和单个项均为 <xref:System.Windows.Forms.MenuItem> 对象。  
  
## 主要属性  
 通过将 <xref:System.Windows.Forms.MenuItem.DefaultItem%2A> 属性设置为 `true`，可以将某菜单项指定为默认项。  单击菜单时，默认项以粗体文本显示。  菜单项的 <xref:System.Windows.Forms.MenuItem.Checked%2A> 属性为 `true` 或 `false`，它指示是否选定了该菜单项。  菜单项的 <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> 属性会自定义选定项的外观：如果 <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> 设置为 `true`，则该项旁边出现一个单选按钮；如果 <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> 设置为 `false`，则该项旁边出现一个选中标记。  
  
## 请参阅  
 <xref:System.Windows.Forms.MainMenu>   
 <xref:System.Windows.Forms.Menu>   
 <xref:System.Windows.Forms.MenuItem>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)