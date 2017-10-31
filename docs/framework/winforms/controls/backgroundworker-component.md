---
title: "BackgroundWorker 组件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "异步模式"
  - "后台操作"
  - "背景任务"
  - "BackgroundWorker 组件"
  - "组件 [Windows 窗体], 异步"
  - "窗体, 后台操作"
  - "窗体, 多线程处理"
  - "线程处理 [Windows 窗体], 后台操作"
ms.assetid: bef7b0ab-ce57-475a-a2d6-fb8a702a9417
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# BackgroundWorker 组件
`BackgroundWorker` 组件使窗体或控件能够异步运行操作。  
  
## 本节内容  
 [BackgroundWorker 组件概述](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md)  
 描述 `BackgroundWorker` 组件，该组件让您能够在应用程序的主要 UI 线程以外的其他线程上异步（“在后台”）执行耗时的操作。  
  
 [演练：在后台运行操作](../../../../docs/framework/winforms/controls/walkthrough-running-an-operation-in-the-background.md)  
 演示如何在设计器中使用 `BackgroundWorker` 组件在单独的线程上运行耗时的操作。  
  
 [如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 演示如何使用 `BackgroundWorker` 组件在单独的线程上运行耗时的操作。  
  
 [演练：实现一个使用后台操作的窗体](../../../../docs/framework/winforms/controls/walkthrough-implementing-a-form-that-uses-a-background-operation.md)  
 使用可异步执行数学运算的设计器创建应用程序。  
  
 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)  
 创建可异步执行数学运算的应用程序。  
  
 [如何：在后台下载文件](../../../../docs/framework/winforms/controls/how-to-download-a-file-in-the-background.md)  
 演示如何使用 `BackgroundWorker` 组件在单独的线程上下载文件。  
  
## 参考  
 <xref:System.ComponentModel.BackgroundWorker>  
 描述该类并提供指向其所有成员的链接。  
  
 <xref:System.ComponentModel.RunWorkerCompletedEventArgs>  
 描述为 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件保留数据的类型。  
  
 <xref:System.ComponentModel.ProgressChangedEventArgs>  
 描述为 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件保留数据的类型。  
  
## 相关章节  
 [Event\-based Asynchronous Pattern Overview](../../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 描述异步模式如何在隐藏多线程设计中固有的许多复杂问题的同时，发挥多线程应用程序的优点。