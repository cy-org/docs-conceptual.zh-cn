---
title: "如何：在 Windows 窗体中启用 ToolStrip 项的运行时重新排序 | Microsoft Docs"
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
  - "AllowItemReorder 属性"
  - "示例 [Windows 窗体], 工具栏"
  - "工具栏 [Windows 窗体], 重新排列控件"
  - "ToolStrip 控件 [Windows 窗体], 示例"
  - "ToolStrip 控件 [Windows 窗体], 对项进行重新排序"
ms.assetid: 8480b69a-379f-4dc2-8dcf-365ed93692b2
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 Windows 窗体中启用 ToolStrip 项的运行时重新排序
您可以允许用户重新排列 <xref:System.Windows.Forms.ToolStrip> 中的 <xref:System.Windows.Forms.ToolStripItem> 控件。  
  
### 启用 ToolStripItem 的运行时重新排列  
  
-   将 <xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A> 属性设置为 `true`。  默认情况下，<xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A> 为 `false`。  
  
     运行时，用户按住 Alt 键和鼠标左键可以将 <xref:System.Windows.Forms.ToolStripItem> 拖动到 <xref:System.Windows.Forms.ToolStrip> 中的其他位置。  
  
    ```vb  
    toolStrip1.AllowItemReorder = True  
  
    ```  
  
    ```csharp  
    toolStrip1.AllowItemReorder = true;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)