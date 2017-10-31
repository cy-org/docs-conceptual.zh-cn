---
title: "ProgressBar 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "ProgressBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "进度控件, 关于进度控件"
  - "ProgressBar 控件 [Windows 窗体], 关于 ProgressBar 控件"
ms.assetid: a05d9cba-3a6a-4f8f-94b8-8ec12799fb80
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# ProgressBar 控件概述（Windows 窗体）
> [!IMPORTANT]
>  <xref:System.Windows.Forms.ToolStripProgressBar> 控件取代了 <xref:System.Windows.Forms.ProgressBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ProgressBar> 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体 <xref:System.Windows.Forms.ProgressBar> 控件通过在水平条中显示适当数目的矩形来指示进程的进度。  进程完成时，进度栏被填满。  进度栏通常用于帮助用户了解等待一项进程（如加载大文件）完成所需的时间。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ProgressBar> 控件在窗体上只能水平放置。  
  
## 主要属性和方法  
 <xref:System.Windows.Forms.ProgressBar> 控件的主要属性有 <xref:System.Windows.Forms.ProgressBar.Value%2A>、<xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A>。  <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 属性设置进度栏可以显示的最大值和最小值。  <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性表示操作过程中已完成的进度。  因为控件中显示的进度栏由块构成，所以 <xref:System.Windows.Forms.ProgressBar> 控件显示的值只是约等于 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性的当前值。  根据 <xref:System.Windows.Forms.ProgressBar> 控件的大小，<xref:System.Windows.Forms.ProgressBar.Value%2A> 属性确定何时显示下一个块。  
  
 更新当前进度值的最常用方法是编写代码来设置 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性。  在加载大文件的例子中，可将最大值设置为以 KB 为单位的文件大小。  例如，如果 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 属性设置为 100、<xref:System.Windows.Forms.ProgressBar.Minimum%2A> 属性设置为 10 并且 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性设置为 50，则将显示 5 个矩形。  这是可以显示的数目的一半。  
  
 但是，除直接设置 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性外，还有其他方法可以修改 <xref:System.Windows.Forms.ProgressBar> 控件显示的值。  <xref:System.Windows.Forms.ProgressBar.Step%2A> 属性可以用于指定 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性递增的值。  然后，调用 <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> 方法来递增该值。  若要更改增量值，您可以使用 <xref:System.Windows.Forms.ProgressBar.Increment%2A> 方法并指定 <xref:System.Windows.Forms.ProgressBar.Value%2A> 属性递增的值。  
  
 另一个以图形方式使用户了解当前操作情况的控件是 <xref:System.Windows.Forms.StatusBar> 控件。  
  
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip> 和 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件取代了 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件以实现向后兼容并供将来使用。  
  
## 请参阅  
 <xref:System.Windows.Forms.ProgressBar>   
 [ProgressBar 控件](../../../../docs/framework/winforms/controls/progressbar-control-windows-forms.md)