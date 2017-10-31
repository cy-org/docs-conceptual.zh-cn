---
title: "Windows 窗体控件中的多线程处理 | Microsoft Docs"
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
  - "BackgroundWorker 组件"
  - "BeginInvoke 方法"
  - "线程处理 [Windows 窗体], 控件"
ms.assetid: c311d652-0f26-45fa-bdcc-b1615d73ce4e
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Windows 窗体控件中的多线程处理
在很多应用程序中，通过在另一个线程上执行耗时的操作，可以让用户界面 \(UI\) 提高响应能力。  可以用很多工具来让 Windows 窗体控件多线程化，包括 <xref:System.Threading> 命名空间、<xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=fullName> 方法和 `BackgroundWorker` 组件。  
  
> [!NOTE]
>  `BackgroundWorker` 组件可以在 <xref:System.Threading> 命名空间和 <xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=fullName> 方法中替换和添加功能；但是，也可以选择保留这些功能以备向后兼容和将来使用。  有关更多信息，请参见 [BackgroundWorker 组件概述](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md)。  
  
## 本节内容  
 [如何：对 Windows 窗体控件进行线程安全调用](../../../../docs/framework/winforms/controls/how-to-make-thread-safe-calls-to-windows-forms-controls.md)  
 显示如何对 Windows 窗体控件进行线程安全调用。  
  
 [如何：使用后台线程搜索文件](../../../../docs/framework/winforms/controls/how-to-use-a-background-thread-to-search-for-files.md)  
 显示如何使用 <xref:System.Threading> 命名空间和 <xref:System.Windows.Forms.Control.BeginInvoke%2A> 方法来异步搜索文件。  
  
## 参考  
 <xref:System.ComponentModel.BackgroundWorker>  
 介绍用于封装辅助线程以执行异步操作的组件。  
  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>  
 介绍如何异步加载声音。  
  
 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>  
 介绍如何异步加载图像。  
  
## 相关章节  
 [如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 显示如何用 <xref:System.ComponentModel.BackgroundWorker> 组件来执行耗时的操作。  
  
 [BackgroundWorker 组件概述](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md)  
 提供一些主题，描述了如何使用 <xref:System.ComponentModel.BackgroundWorker> 组件来执行异步操作。