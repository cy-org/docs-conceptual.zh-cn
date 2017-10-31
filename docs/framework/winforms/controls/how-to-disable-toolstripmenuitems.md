---
title: "如何：禁用 ToolStripMenuItems | Microsoft Docs"
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
  - "禁用菜单项"
  - "菜单项, 禁用"
  - "菜单项, 启用"
  - "菜单, 禁用菜单项"
  - "ToolStripMenuItems, 禁用"
  - "ToolStripMenuItems, 启用"
ms.assetid: bcc1da84-50fd-41d2-8475-103b581d5654
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：禁用 ToolStripMenuItems
可通过启用或禁用响应用户操作的菜单项来限制或放宽用户可发出的命令。  菜单项创建完后是默认启用的，但是这可以通过 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性进行调整。  可在设计时在**“属性”**窗口中使用此属性，也可通过编程方式在代码中进行设置。  
  
### 以编程方式禁用菜单项  
  
-   在设置菜单项属性的方法内，添加将 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性设置为 `false` 的代码。  
  
    ```vb  
    MenuItem1.Enabled = False  
    ```  
  
    ```csharp  
    menuItem1.Enabled = false;  
    ```  
  
    ```cpp  
    menuItem1->Enabled = false;  
    ```  
  
    > [!TIP]
    >  禁用菜单中的第一个或顶层菜单项将隐藏包含在该菜单中的所有菜单项，但不会禁用它们。  同样，禁用包含子菜单项的菜单项也会隐藏这些子菜单项，但不会禁用它们。  如果给定菜单上的所有命令对于用户都不可用，则隐藏并且禁用整个菜单是一种良好的编程方法，因为它显示的是干净的用户界面。  应该隐藏和禁用菜单，并禁用该菜单中的每个项和子菜单项，因为仅通过隐藏不能防止他人使用快捷键访问菜单命令。  将顶层菜单项的 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 属性设置为 `false` 以隐藏整个菜单。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [如何：隐藏 ToolStripMenuItem](../../../../docs/framework/winforms/controls/how-to-hide-toolstripmenuitems.md)   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)