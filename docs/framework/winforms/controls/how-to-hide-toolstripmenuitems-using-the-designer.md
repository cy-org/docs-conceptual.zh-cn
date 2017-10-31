---
title: "如何：使用设计器隐藏 ToolStripMenuItem | Microsoft Docs"
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
  - "菜单项, 隐藏"
  - "MenuStrip 控件 [Windows 窗体], 在设计器中隐藏菜单项"
  - "ToolStripMenuItems, 在设计器中隐藏菜单项"
ms.assetid: 8f1b057e-3d8a-4f11-88df-935f7b29a836
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用设计器隐藏 ToolStripMenuItem
隐藏菜单项是控制应用程序的用户界面 \(UI\) 和限制用户命令的一种方法。  通常，当菜单上的所有菜单项都不可用时，需要隐藏整个菜单。  这能减少对用户的干扰。  此外，可能需要隐藏并禁用菜单或菜单项，因为仅通过隐藏不能防止用户使用快捷键访问菜单命令。  有关禁用菜单项的更多信息，请参见 [如何：使用设计器禁用 ToolStripMenuItem](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems-using-the-designer.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 隐藏顶级菜单及其子菜单项  
  
1.  选择顶级菜单项并将其 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 或 <xref:System.Windows.Forms.ToolStripItem.Available%2A> 属性设置为 `false`。  
  
     隐藏了顶级菜单项后，该菜单内的所有菜单项也会被隐藏。  将 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 设置为 `false` 之后，如果在 <xref:System.Windows.Forms.MenuStrip> 以外的地方单击，整个顶级菜单项及其子菜单项就会从窗体中消失，从而显示出操作的运行时效果。  若要在设计时显示隐藏的顶级菜单项，请单击**“文档大纲”**的**“组件栏”**中的 <xref:System.Windows.Forms.MenuStrip>，或者单击属性网格的顶部。  
  
> [!NOTE]
>  除了合并方案中的多文档界面 \(MDI\) 子菜单，一般不隐藏整个菜单。  
  
### 隐藏子菜单项  
  
1.  选择子菜单项并将其 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 属性设置为 `false`。  
  
     隐藏一个子菜单项后，在设计时该项在窗体上仍是可见的，因此，可以容易地选择该项以进行其他工作。  实际上，该项将在运行时隐藏。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripItem.Visible%2A>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>   
 <xref:System.Windows.Forms.ToolStripItem.Available%2A>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Overflow%2A>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)   
 [如何：使用设计器禁用 ToolStripMenuItem](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems-using-the-designer.md)