---
title: "StatusBar 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "StatusBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "状态栏"
  - "StatusBar 控件 [Windows 窗体], 关于 StatusBar 控件"
ms.assetid: b7b9852c-633d-4416-bb2e-94852b989c6c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# StatusBar 控件概述（Windows 窗体）
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip> 和 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件取代了 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体 [StatusBar 控件](../../../../docs/framework/winforms/controls/statusbar-control-windows-forms.md)在窗体上用作一个通常显示在窗口底部的区域，应用程序可在其中显示各种状态信息。  <xref:System.Windows.Forms.StatusBar> 控件可以有状态栏面板（用于显示文本或图标以指示状态）或一系列动画图标（用于指示某个进程正在工作，例如，表示正在保存文档的 [!INCLUDE[ofprword](../../../../includes/ofprword-md.md)]）。  
  
## 使用 StatusBar 控件  
 在鼠标滚动到超链接时，Internet Explorer 使用状态栏指示某个页面的 URL；[!INCLUDE[ofprword](../../../../includes/ofprword-md.md)] 为您提供有关页位置、节位置和编辑模式（如改写和修订跟踪）的信息；[!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 使用状态栏提供区分上下文的信息，如告诉您如何操纵可停靠的窗口，使其停靠或浮动。  
  
 通过将 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 属性设置为 `false`（默认值）并将状态栏的 <xref:System.Windows.Forms.StatusBar.Text%2A> 属性设置为希望出现在状态栏中的文本，可在状态栏中显示一条消息。  您可以将状态栏分成多个面板来显示多种类型的信息，方法是将 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 属性设置为 `true` 并使用 <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection> 的 <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection.Add%2A> 方法。  
  
## 请参阅  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [如何：确定 Windows 窗体 StatusBar 控件中被单击的面板](../../../../docs/framework/winforms/controls/determine-which-panel-wf-statusbar-control-was-clicked.md)