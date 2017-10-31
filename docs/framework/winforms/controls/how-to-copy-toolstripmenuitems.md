---
title: "如何：复制 ToolStripMenuItem | Microsoft Docs"
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
  - "菜单项, 复制和粘贴"
  - "MenuStrip 控件 [Windows 窗体], 排列项"
  - "ToolStripMenuItem, 复制和粘贴"
ms.assetid: 17ef4207-e92e-4db2-b648-27246e6517ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：复制 ToolStripMenuItem
在设计时，你可以将整个顶级菜单及其子菜单项复制到 <xref:System.Windows.Forms.MenuStrip> 上的其他位置。 还可以复制顶级菜单之间的单个菜单项或在菜单中更改菜单项的位置。  
  
### 若要将顶级菜单及其子菜单项复制到另一个顶级位置  
  
1.  左键单击想要复制的菜单并按 CTRL\+C，或右键单击该菜单，并从快捷菜单选择“复制”。  
  
2.  左键单击预期新位置之后的顶级菜单并按 CTRL\+V，或右键单击预期新位置之前的顶级菜单项，并从快捷菜单选择“粘贴”。  
  
     复制的菜单将插入到所选顶级菜单之前。  
  
### 若要将顶级菜单及其子菜单项复制到一个下拉位置  
  
1.  左键单击想要移动的菜单并按 CTRL\+C，或右键单击该菜单，并从快捷菜单选择“复制”。  
  
2.  在目标顶级菜单中，左键单击预期新位置上方的子菜单项并按 CTRL\+V，或右键单击目标新位置上方的子菜单项，并从快捷菜单选择“粘贴”。  
  
     复制的菜单将插入到所选子菜单项之前。  
  
### 若要将子菜单项复制到另一菜单  
  
1.  左键单击想要复制的子菜单项并按 CTRL\+C，或右键单击该子菜单项，并从快捷菜单选择“复制”。  
  
2.  左键单击将包含你所剪切的子菜单项的菜单。  
  
3.  左键单击预期新位置之前的子菜单项并按 CTRL\+V，或右键单击预期新位置之前的子菜单项，并从快捷菜单选择“粘贴”。  
  
     复制的子菜单项将插入到所选子菜单项之前。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)