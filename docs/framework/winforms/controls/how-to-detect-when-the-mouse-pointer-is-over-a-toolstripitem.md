---
title: "如何：检测鼠标指针何时在 ToolStripItem 上 | Microsoft Docs"
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
  - "鼠标, 检测工具栏上的移动"
  - "工具栏 [Windows 窗体], 检测鼠标移动"
  - "ToolStrip 控件 [Windows 窗体], 检测鼠标移动"
  - "ToolStripItem 类, 检测鼠标移动"
ms.assetid: d38b5082-aba7-4f6c-841b-bd9714e307fd
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：检测鼠标指针何时在 ToolStripItem 上
采用以下过程检测鼠标指针何时在 <xref:System.Windows.Forms.ToolStripItem> 上面。  
  
### 检测指针何时在 ToolStripItem 上面  
  
-   对 <xref:System.Windows.Forms.ToolStripItem.CanSelect%2A> 为 `true` 的项采用 <xref:System.Windows.Forms.ToolStripItem.Selected%2A> 属性。  
  
     这使您不必同步 <xref:System.Windows.Forms.ToolStripItem.MouseEnter> 和 <xref:System.Windows.Forms.ToolStripItem.MouseLeave> 事件。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripItem.Selected%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)