---
title: "TabControl 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "TabControl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "属性页, Windows 窗体"
  - "选项卡页, 关于选项卡页"
  - "TabControl 控件 [Windows 窗体], 关于 TabControl 控件"
  - "Windows 窗体对话框, 选项卡"
ms.assetid: 2b4ea784-a39d-463c-81d8-af74ce068476
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# TabControl 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.TabControl> 显示多个选项卡，这些选项卡类似于笔记本中的分隔卡或档案柜文件夹集中的标签。  选项卡中可包含图片和其他控件。  您可以使用该选项卡控件来生成多页对话框，这种对话框在 Windows 操作系统中的许多地方（例如控制面板的“显示”属性中）都可以找到。  此外，<xref:System.Windows.Forms.TabControl> 还可以用来创建用于设置一组相关属性的属性页。  
  
## 使用 TabControl  
 <xref:System.Windows.Forms.TabControl> 的最重要的属性是 <xref:System.Windows.Forms.TabControl.TabPages%2A>，该属性包含单独的选项卡。  每一个单独的选项卡都是一个 <xref:System.Windows.Forms.TabPage> 对象。  单击选项卡时，将为该 <xref:System.Windows.Forms.TabPage> 对象引发 <xref:System.Windows.Forms.Control.Click> 事件。  
  
## 请参阅  
 <xref:System.Windows.Forms.TabControl>   
 [TabControl 控件](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)   
 [如何：更改 Windows 窗体 TabControl 的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)   
 [如何：将控件添加到选项卡页](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [如何：使用 Windows 窗体 TabControl 添加和移除选项卡](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)   
 [如何：禁用选项卡页](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [Windows 窗体中的对话框](../../../../docs/framework/winforms/dialog-boxes-in-windows-forms.md)