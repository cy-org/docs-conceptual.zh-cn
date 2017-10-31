---
title: "如何：使用设计器禁用 ToolStripMenuItem | Microsoft Docs"
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
  - "菜单项, 禁用"
  - "菜单, 禁用项"
  - "MenuStrip 控件 [Windows 窗体], 在设计器中禁用菜单项"
  - "ToolStripMenuItems, 在设计器中禁用"
ms.assetid: 985e311e-7d67-4205-b5a3-d045b68a4a03
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用设计器禁用 ToolStripMenuItem
可通过启用或禁用响应用户操作的菜单项来限制或放宽用户可发出的命令。  菜单项创建完后是默认启用的，但是这可以通过 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性进行调整。  可在设计时在**“属性”**窗口中使用此属性，也可通过编程方式在代码中进行设置。  有关更多信息，请参见[如何：禁用 ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时禁用菜单项  
  
1.  在窗体上选定菜单项以后，将 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性设置为 `false`。  
  
    > [!TIP]
    >  禁用菜单中的第一个或顶层菜单项将导致禁用包含在该菜单中的所有菜单项。  同样，禁用包含子菜单项的菜单项也会禁用这些子菜单项。  如果给定菜单上的所有命令对于用户都不可用，则隐藏并且禁用整个菜单是一种良好的编程方法，因为它显示的是干净的用户界面。  应该同时隐藏和禁用菜单，因为仅靠隐藏无法防止通过快捷键访问菜单命令。  将顶层菜单项的 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 属性设置为 `false` 以隐藏整个菜单。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [如何：隐藏 ToolStripMenuItem](../../../../docs/framework/winforms/controls/how-to-hide-toolstripmenuitems.md)   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)