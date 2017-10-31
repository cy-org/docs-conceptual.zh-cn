---
title: "在 Windows 窗体 MenuStrip 控件中合并菜单项 | Microsoft Docs"
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
  - "MenuStrip, 合并"
  - "合并, 一般概念"
ms.assetid: 95e113ba-f362-4dda-8a76-6d95ddc45cee
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 在 Windows 窗体 MenuStrip 控件中合并菜单项
如果具有多文档界面 \(MDI\) 应用程序，就能将菜单项或整个菜单从子窗体合并到父窗体的菜单中。  
  
 本主题描述的基本概念涉及在 MDI 应用程序中合并菜单项。  
  
## 一般概念  
 合并过程涉及目标控件和源控件：  
  
-   目标控件是要在其中合并菜单项的主窗体或 MDI 父窗体上的 <xref:System.Windows.Forms.MenuStrip> 控件。  
  
-   源控件是 MDI 子窗体上的 <xref:System.Windows.Forms.MenuStrip> 控件，该子窗体包含了要合并到目标菜单的菜单项。  
  
 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 属性标识将用当前 MDI 父窗体的 MDI 子窗体标题来填充其下拉列表的菜单项。  例如，您通常会在**“窗口”**菜单上列出当前打开的 MDI 子窗体。  
  
 <xref:System.Windows.Forms.ToolStripMenuItem.IsMdiWindowListEntry%2A> 属性标识哪些菜单项来自 MDI 子窗体上的 <xref:System.Windows.Forms.MenuStrip>。  
  
 可以手动或自动合并菜单项。  两种方法的菜单项合并方式相同，但合并的激活方式不同，本主题后面的“手动合并”和“自动合并”部分分别论述了这一点。  不论是手动合并还是自动合并，每个合并操作都会影响下一个合并操作。  
  
 <xref:System.Windows.Forms.MenuStrip> 合并将菜单项从一个 <xref:System.Windows.Forms.ToolStrip> 移动到另一个，而不像 <xref:System.Windows.Forms.MainMenu> 的情况那样进行克隆。  
  
## MergeAction 值  
 使用 <xref:System.Windows.Forms.MergeAction> 属性在源 <xref:System.Windows.Forms.MenuStrip> 中对菜单项设置合并操作。  
  
 下表描述了可用合并操作的含义和典型用法。  
  
|MergeAction 值|说明|典型使用|  
|-------------------|--------|----------|  
|<xref:System.Windows.Forms.MergeAction>|（默认）将源项添加到目标项集合的末尾。|程序的某个部分激活时，将菜单项添加到菜单末尾。|  
|<xref:System.Windows.Forms.MergeAction>|将源项添加到目标项的集合中，添加位置由源项上设置的 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 属性指定。|当程序的某些部分激活时，将菜单项添加到菜单的中间或开头。<br /><br /> 如果两个菜单项的 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 值相同，将以相反顺序添加。  适当设置 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 以保持原始顺序。|  
|<xref:System.Windows.Forms.MergeAction>|查找文本匹配（找不到就用 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 值），然后用源菜单项替换匹配目标菜单项。|用执行不同操作但名称相同的源菜单项替换目标菜单项。|  
|<xref:System.Windows.Forms.MergeAction>|查找文本匹配（找不到就用 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 值），然后将所有下拉项从源添加到目标。|生成将菜单项插入或添加到子菜单或者将菜单项从子菜单移除的菜单结构。  例如，可以将菜单项从 MDI 子窗体添加到主 <xref:System.Windows.Forms.MenuStrip>**“另存为”**菜单。<br /><br /> <xref:System.Windows.Forms.MergeAction> 允许在不执行任何操作的情况下在菜单结构中导航。  它提供了一种评估后续项的方式。|  
|<xref:System.Windows.Forms.MergeAction>|查找文本匹配（找不到就用 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 值），然后将项从目标中移除。|将菜单项从目标 <xref:System.Windows.Forms.MenuStrip> 中移除。|  
  
## 手动合并  
 只有 <xref:System.Windows.Forms.MenuStrip> 控件参与自动合并。  要组合其他控件（例如 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件）的项，必须根据需要调用代码中的 <xref:System.Windows.Forms.ToolStripManager.Merge%2A> 和 <xref:System.Windows.Forms.ToolStripManager.RevertMerge%2A> 方法，以对其进行手动合并。  
  
## 自动合并  
 可以通过激活源窗体对 MDI 应用程序使用自动合并。  要在 MDI 应用程序中使用 <xref:System.Windows.Forms.MenuStrip>，需要将 <xref:System.Windows.Forms.Form.MainMenuStrip%2A> 属性设置为目标 <xref:System.Windows.Forms.MenuStrip>，使得对源 <xref:System.Windows.Forms.MenuStrip> 执行的合并操作反映在目标 <xref:System.Windows.Forms.MenuStrip> 中。  
  
 可以通过激活 MDI 源上的 <xref:System.Windows.Forms.MenuStrip> 来触发自动合并。  源 <xref:System.Windows.Forms.MenuStrip> 在激活时将被合并到 MDI 目标中。  当新窗体变为活动状态时，将在上一个窗体上恢复合并，并在新窗体上触发合并。  可以根据需要在每个 <xref:System.Windows.Forms.ToolStripItem> 上设置 <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> 属性并在每个 <xref:System.Windows.Forms.MenuStrip> 上设置 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 属性，从而控制此行为。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripManager>   
 <xref:System.Windows.Forms.MenuStrip>   
 [MenuStrip 控件](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [如何：使用 MenuStrip 创建 MDI 窗口列表](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)   
 [如何：为 MDI 应用程序设置自动菜单合并](../../../../docs/framework/winforms/controls/how-to-set-up-automatic-menu-merging-for-mdi-applications.md)