---
title: "如何：为 MDI 应用程序设置自动菜单合并 | Microsoft Docs"
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
  - "合并, 自动菜单"
ms.assetid: 55e32cad-1141-4a56-aa33-d9543ca3d393
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：为 MDI 应用程序设置自动菜单合并
下面的过程描述了使用 <xref:System.Windows.Forms.MenuStrip> 在多文档界面 \(MDI\) 应用程序中设置自动合并的基本步骤。  
  
### 设置自动菜单合并  
  
1.  通过将 MDI 父窗体的 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 属性设置为 `true` 来创建 MDI 父窗体。  
  
2.  向 MDI 父窗体添加 <xref:System.Windows.Forms.MenuStrip>，将其 <xref:System.Windows.Forms.Form.MainMenuStrip%2A> 属性设置为 <xref:System.Windows.Forms.MenuStrip>。  
  
3.  创建一个 MDI 子窗体，并将其 <xref:System.Windows.Forms.Form.MdiParent%2A> 属性设置为父窗体的名称。  
  
4.  向 MDI 子窗体添加一个 <xref:System.Windows.Forms.MenuStrip>。  
  
5.  在子窗体中，将 <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 属性设置为 `false`。  
  
6.  在要合并到父窗体的 <xref:System.Windows.Forms.MenuStrip> 中的子窗体处于活动状态时，将菜单项添加到该子窗体的 <xref:System.Windows.Forms.MenuStrip> 中。  
  
7.  在子窗体 <xref:System.Windows.Forms.MenuStrip> 中使用菜单项上的 <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> 属性，以控制其合并到目标窗体的方式。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)