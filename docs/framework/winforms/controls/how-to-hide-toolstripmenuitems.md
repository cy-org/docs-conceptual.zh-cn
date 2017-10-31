---
title: "如何：隐藏 ToolStripMenuItem | Microsoft Docs"
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
  - "隐藏菜单项"
  - "菜单项, 隐藏"
  - "菜单, 隐藏菜单项"
  - "MenuStrip 控件 [Windows 窗体], 隐藏菜单项"
  - "ToolStripMenuItems, 隐藏"
ms.assetid: 418a768f-808a-44cd-8cef-f4e161883621
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：隐藏 ToolStripMenuItem
隐藏菜单项是控制应用程序的用户界面和限制用户命令的一种方法。  通常，当菜单上的所有菜单项都不可用时，需要隐藏整个菜单。  这能减少对用户的干扰。  此外，可能需要隐藏并禁用菜单或菜单项，因为仅通过隐藏不能防止用户使用快捷键访问菜单命令。  
  
### 以编程方式隐藏任意菜单项  
  
-   在设置菜单项的属性的方法内，添加将 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 属性设置为 `false` 的代码。  
  
    ```vb  
    MenuItem3.Visible = False  
  
    ```  
  
    ```csharp  
    menuItem3.Visible = false;  
  
    ```  
  
    ```cpp  
    menuItem3->Visible = false;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripItem.Visible%2A>   
 <xref:System.Windows.Forms.MenuStrip>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)   
 [如何：禁用 ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems.md)