---
title: "如何：在 Windows 窗体中管理 ToolStrip 溢出 | Microsoft Docs"
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
  - "CanOverflow 属性"
  - "示例 [Windows 窗体], 工具栏"
  - "Overflow 属性"
  - "工具栏 [Windows 窗体], 管理溢出"
  - "ToolStrip 控件 [Windows 窗体], 管理溢出"
ms.assetid: fa10e0ad-4cbf-4c0d-9082-359c2f855d4e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：在 Windows 窗体中管理 ToolStrip 溢出
当 <xref:System.Windows.Forms.ToolStrip> 控件上的所有项超出已分配的空间时，可以对 <xref:System.Windows.Forms.ToolStrip> 启用溢出功能，并确定特定 <xref:System.Windows.Forms.ToolStripItem> 的溢出行为。  
  
 当您将 <xref:System.Windows.Forms.ToolStripItem>（比已分配的空间需要更多的空间）添加到已给定窗体当前大小的 <xref:System.Windows.Forms.ToolStrip> 时，<xref:System.Windows.Forms.ToolStripOverflowButton> 会自动显示在 <xref:System.Windows.Forms.ToolStrip> 上。  <xref:System.Windows.Forms.ToolStripOverflowButton> 将显示，并且启用溢出的项将会移到下拉溢出菜单中。  这使您可以自定义和按照优先顺序排列 <xref:System.Windows.Forms.ToolStrip> 项适合不同窗体大小的方式。  当这些项发生溢出时，也可以通过使用 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 和 <xref:System.Windows.Forms.ToolStripOverflow.DisplayedItems%2A?displayProperty=fullName> 属性以及 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 事件来更改这些项的外观。  如果在设计时或运行时扩大窗体，则在主 <xref:System.Windows.Forms.ToolStrip> 上可以显示更多的 <xref:System.Windows.Forms.ToolStripItem>，<xref:System.Windows.Forms.ToolStripOverflowButton> 甚至可能不会出现，直到您减小窗体的大小。  
  
### 对 ToolStrip 控件启用溢出  
  
-   请确保，<xref:System.Windows.Forms.ToolStrip> 的 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 属性没有设置为 `false`。  默认值为 `True`。  
  
     当 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 为 `True`（默认情况下）时，如果 <xref:System.Windows.Forms.ToolStripItem> 的内容超出 <xref:System.Windows.Forms.ToolStrip> 的水平宽度或 <xref:System.Windows.Forms.ToolStrip> 的垂直高度，<xref:System.Windows.Forms.ToolStripItem> 将被送入下拉溢出菜单。  
  
### 指定特定 ToolStripItem 的溢出行为  
  
-   将 <xref:System.Windows.Forms.ToolStripItem> 的 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 属性设置为所需的值。  可能值有：`Always`、`Never` 和 `AsNeeded`。  默认值是 `AsNeeded`。  
  
    ```vb  
    toolStripTextBox1.Overflow = _  
    System.Windows.Forms.ToolStripItemOverflow.Never  
  
    ```  
  
    ```csharp  
    toolStripTextBox1.Overflow = _  
    System.Windows.Forms.ToolStripItemOverflow.Never;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripOverflowButton>   
 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A>   
 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)