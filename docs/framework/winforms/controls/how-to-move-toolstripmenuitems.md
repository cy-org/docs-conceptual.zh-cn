---
title: "如何：移动 ToolStripMenuItem | Microsoft Docs"
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
  - "菜单项, 剪切和粘贴"
  - "菜单项, 拖放"
  - "菜单项, 移动"
  - "菜单, 排列项"
  - "MenuStrip 控件 [Windows 窗体], 排列项"
  - "ToolStripMenuItems, 剪切和粘贴"
  - "ToolStripMenuItems, 拖放"
  - "ToolStripMenuItems, 移动"
ms.assetid: cab9e03e-4edd-4c25-b3e3-bd1edc602bd9
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：移动 ToolStripMenuItem
在设计时，可以将整个顶级菜单及其菜单项移动至 <xref:System.Windows.Forms.MenuStrip> 上的不同位置。  还可以在顶级菜单之间移动个别菜单项或在菜单内部更改菜单项的位置。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 将顶级菜单及其菜单项移动到另一个顶级位置  
  
1.  在要移动的菜单上单击并按住鼠标左键。  
  
2.  将插入点拖动到目标新位置之前的顶级菜单，并释放鼠标左键。  
  
     选定菜单将移动到插入点右侧。  
  
### 将顶级菜单及其菜单项移动到下拉位置  
  
1.  左击要移动的菜单，然后按 Ctrl\+X，或者右击菜单然后从快捷菜单中选择**“剪切”**。  
  
2.  在目标顶级菜单中左击目标新位置上方的菜单项，再按 Ctrl\+V，或者右击目标新位置上方的菜单项，再从快捷菜单中选择**“粘贴”**。  
  
     所剪切的菜单将插入到选定菜单项之后。  
  
### 使用项集合编辑器在菜单内移动菜单项  
  
1.  右击包含要移动的菜单项的菜单。  
  
2.  在快捷菜单上，选择**“编辑下拉菜单项”**。  
  
3.  在**“项集合编辑器”**中左击要移动的菜单项。  
  
4.  单击向上键和向下键，在菜单内移动菜单项。  
  
5.  单击**“确定”**。  
  
### 使用键盘在菜单内移动菜单项  
  
1.  按住 Alt 键。  
  
2.  在要移动的菜单项上单击并按住鼠标左键。  
  
3.  将菜单项拖至新位置，然后释放鼠标左键。  
  
### 将菜单项移到另一个菜单  
  
1.  左击要移动的菜单项，然后按 Ctrl\+X，或者右击菜单项，然后从快捷菜单中选择**“剪切”**。  
  
2.  左击将包含所剪切的菜单项的菜单。  
  
3.  左击目标新位置之前的菜单项，再按 Ctrl\+V，或者右击目标新位置之前的菜单项，再从快捷菜单中选择**“粘贴”**。  
  
     所剪切的菜单项将插入到选定菜单项之后。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)