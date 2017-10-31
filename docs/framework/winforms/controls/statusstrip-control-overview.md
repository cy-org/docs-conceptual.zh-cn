---
title: "StatusStrip 控件概述 | Microsoft Docs"
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
  - "StatusStrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "状态栏, 关于状态栏"
  - "StatusStrip 控件 [Windows 窗体], 关于 StatusStrip 控件"
ms.assetid: c0d9bcbb-f8b8-46ef-bae2-4146b8c8ce99
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# StatusStrip 控件概述
<xref:System.Windows.Forms.StatusStrip> 控件将显示有关在 <xref:System.Windows.Forms.Form> 上查看的对象、对象组件的信息或应用程序内与该对象操作相关的上下文信息。  通常，<xref:System.Windows.Forms.StatusStrip> 控件由 <xref:System.Windows.Forms.ToolStripStatusLabel> 对象组成，每个对象将显示文本、图标或两者都有。  <xref:System.Windows.Forms.StatusStrip> 也可以包括 <xref:System.Windows.Forms.ToolStripDropDownButton>、<xref:System.Windows.Forms.ToolStripSplitButton> 和 <xref:System.Windows.Forms.ToolStripProgressBar> 控件。  
  
 默认 <xref:System.Windows.Forms.StatusStrip> 没有面板。  若要将面板添加到 <xref:System.Windows.Forms.StatusStrip>，则使用 <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A?displayProperty=fullName> 方法。  
  
 广泛支持用于处理 <xref:System.Windows.Forms.StatusStrip> 项目和 Visual Studio 中的常见命令。  
  
 另请参阅 [StatusStrip 项目集合编辑器](http://msdn.microsoft.com/library/ms233631%20\(v=vs.110\))，[StatusStrip 任务对话框](http://msdn.microsoft.com/library/ms233642%20\(v=vs.110\))。  
  
 尽管 <xref:System.Windows.Forms.StatusStrip> 替换并扩展了早期版本的 <xref:System.Windows.Forms.StatusBar> 控件，但也可以选择保留 <xref:System.Windows.Forms.StatusBar> 以备向后兼容性和将来使用。  
  
### 重要 StatusStrip 成员  
  
|名称|描述|  
|--------|--------|  
|<xref:System.Windows.Forms.StatusStrip.CanOverflow%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.StatusStrip> 是否支持溢出功能。|  
|<xref:System.Windows.Forms.StatusStrip.Stretch%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.StatusStrip> 是否在其 <xref:System.Windows.Forms.ToolStripContainer> 中从一端拉伸到了另一端。|  
  
### 重要 StatusStrip 伴随类  
  
|名称|描述|  
|--------|--------|  
|<xref:System.Windows.Forms.ToolStripStatusLabel>|表示 <xref:System.Windows.Forms.StatusStrip> 控件中的一个面板。|  
|<xref:System.Windows.Forms.ToolStripDropDownButton>|显示一个相关联的 <xref:System.Windows.Forms.ToolStripDropDown>，用户可以从中选择单个项目。|  
|<xref:System.Windows.Forms.ToolStripSplitButton>|表示一个两部分的控件，其中包括一个标准按钮和一个下拉菜单。|  
|<xref:System.Windows.Forms.ToolStripProgressBar>|显示进程的完成状态。|  
  
## 请参阅  
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>