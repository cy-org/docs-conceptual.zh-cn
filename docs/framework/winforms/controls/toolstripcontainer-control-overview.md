---
title: "ToolStripContainer 控件概述 | Microsoft Docs"
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
  - "ToolStripContainer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "工具栏 [Windows 窗体], 内置漂浮"
  - "ToolStripContainer 控件 [Windows 窗体], 关于 ToolStripContainer 控件"
ms.assetid: c7d63bff-64e2-4a63-bd89-d31bc96dacb8
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# ToolStripContainer 控件概述
在 <xref:System.Windows.Forms.ToolStripContainer> 的左侧、右侧、顶部和底部都有用来放置和漂浮 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件的面板。  如果将多个 <xref:System.Windows.Forms.ToolStrip> 控件放在 <xref:System.Windows.Forms.ToolStripContainer> 的左边或右边，这些控件会垂直重叠；  如果将这些控件放在 <xref:System.Windows.Forms.ToolStripContainer> 的顶部或底部，则会水平重叠。  使用 <xref:System.Windows.Forms.ToolStripContainer> 的中心 <xref:System.Windows.Forms.ToolStripContentPanel> 可以在窗体上放置传统控件。  
  
 任意或所有 <xref:System.Windows.Forms.ToolStripContainer> 控件均可在设计时直接选择；这些控件中的任何一个或所有这些控件均可删除。  <xref:System.Windows.Forms.ToolStripContainer> 的每个面板都是可扩展和可折叠的，并且可以用它包含的控件来调整大小。  
  
### 重要的 ToolStripContainer 成员  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.ToolStripContainer.BottomToolStripPanel%2A>|获取 <xref:System.Windows.Forms.ToolStripContainer> 的底部面板。|  
|<xref:System.Windows.Forms.ToolStripContainer.BottomToolStripPanelVisible%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.ToolStripContainer> 的底部面板是否可见。|  
|<xref:System.Windows.Forms.ToolStripContainer.LeftToolStripPanel%2A>|获取 <xref:System.Windows.Forms.ToolStripContainer> 的左面板。|  
|<xref:System.Windows.Forms.ToolStripContainer.LeftToolStripPanelVisible%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.ToolStripContainer> 的左面板是否可见。|  
|<xref:System.Windows.Forms.ToolStripContainer.RightToolStripPanel%2A>|获取 <xref:System.Windows.Forms.ToolStripContainer> 的右面板。|  
|<xref:System.Windows.Forms.ToolStripContainer.RightToolStripPanelVisible%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.ToolStripContainer> 的右面板是否可见。|  
|<xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanel%2A>|获取 <xref:System.Windows.Forms.ToolStripContainer> 的顶部面板。|  
|<xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanelVisible%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.ToolStripContainer> 的顶部面板是否可见。|  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripContainer>   
 <xref:System.Windows.Forms.ToolStripContentPanel>