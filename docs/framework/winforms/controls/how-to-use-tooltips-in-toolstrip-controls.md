---
title: "如何：在 ToolStrip 控件中使用工具提示 | Microsoft Docs"
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
  - "工具栏 [Windows 窗体], 添加工具提示"
  - "ToolStrip 控件 [Windows 窗体], 添加工具提示"
  - "工具提示 [Windows 窗体], 添加"
ms.assetid: c5d86024-a7c5-44ee-8b3f-2daf53d80d3e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在 ToolStrip 控件中使用工具提示
通过将控件的 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> 属性设置为 `true`，可以显示所需 <xref:System.Windows.Forms.ToolStrip> 控件的 <xref:System.Windows.Forms.ToolTip>。  
  
### 显示工具提示  
  
-   将控件的 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> 属性设置为 `true`。  
  
     <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A?displayProperty=fullName> 的默认值为 `true`，<xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A?displayProperty=fullName> 和 <xref:System.Windows.Forms.StatusStrip.ShowItemToolTips%2A?displayProperty=fullName> 的默认值为 `false`。  
  
### 使用 ToolStripButton 工具提示文本的 ToolTipText 属性  
  
1.  将该按钮的 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> 属性设置为 `true`。  
  
2.  将该按钮的 <xref:System.Windows.Forms.ToolStripButton.AutoToolTip%2A?displayProperty=fullName> 属性设置为 `false`。  
  
     默认情况下，<xref:System.Windows.Forms.ToolStripButton>、<xref:System.Windows.Forms.ToolStripDropDownButton> 和 <xref:System.Windows.Forms.ToolStripSplitButton> 的 `AutoToolTip` 属性为 `true`。  
  
     默认情况下，<xref:System.Windows.Forms.ToolStripButton> 使用 <xref:System.Windows.Forms.ToolTip> 文本的 `Text` 属性。  通过该过程显示 <xref:System.Windows.Forms.ToolStripButton> <xref:System.Windows.Forms.ToolTip> 中的自定义文本。  
  
> [!NOTE]
>  如果将 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 或 <xref:System.Windows.Forms.ToolStripItemDisplayStyle>，则按钮上不会出现任何文本，但仍会出现工具提示。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A>   
 <xref:System.Windows.Forms.ToolStripButton>   
 <xref:System.Windows.Forms.ToolStripDropDownButton>   
 <xref:System.Windows.Forms.ToolStripSplitButton>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)