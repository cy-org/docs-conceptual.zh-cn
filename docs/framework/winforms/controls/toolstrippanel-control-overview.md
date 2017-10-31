---
title: "ToolStripPanel 控件概述 | Microsoft Docs"
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
  - "ToolStripPanel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "工具栏 [Windows 窗体]"
  - "ToolStripPanel 控件 [Windows 窗体], 关于 ToolStripPanel 控件"
ms.assetid: ce54a60c-5eba-4b4c-bd77-cf0748a666cc
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# ToolStripPanel 控件概述
<xref:System.Windows.Forms.ToolStripPanel> 为放置和漂浮 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件提供了单一区域。  取决于 <xref:System.Windows.Forms.ToolStripPanel> 的 <xref:System.Windows.Forms.ToolStripPanelRow.Orientation%2A>，多个 <xref:System.Windows.Forms.ToolStrip> 控件将垂直或水平堆放。  
  
### 重要的 ToolStripPanel 成员  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.ToolStripPanel.Orientation%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.ToolStripPanel> 是水平方向还是垂直方向。|  
|<xref:System.Windows.Forms.ToolStripPanel.Renderer%2A>|获取或设置用来自定义 <xref:System.Windows.Forms.ToolStripPanel> 的外观的 <xref:System.Windows.Forms.ToolStripRenderer>。|  
|<xref:System.Windows.Forms.ToolStripPanel.RenderMode%2A>|获取或设置要应用于 <xref:System.Windows.Forms.ToolStripPanel> 的绘制样式。|  
|<xref:System.Windows.Forms.ToolStripPanel.RowMargin%2A>|获取或设置 <xref:System.Windows.Forms.ToolStripPanelRow> 和 <xref:System.Windows.Forms.ToolStripPanel> 之间的间距（以像素为单位）。|  
|<xref:System.Windows.Forms.ToolStripPanel.Rows%2A>|获取此 <xref:System.Windows.Forms.ToolStripPanel> 中的 <xref:System.Windows.Forms.ToolStripPanelRow>。|  
|<xref:System.Windows.Forms.ToolStripPanel.Join%2A>|将 <xref:System.Windows.Forms.ToolStrip> 添加到 <xref:System.Windows.Forms.ToolStripPanel>。|  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripContainer>   
 <xref:System.Windows.Forms.ToolStripContentPanel>   
 [ToolStrip Sample](http://msdn.microsoft.com/zh-cn/b7352439-184a-4a3a-b2ad-07465d3af9ed)