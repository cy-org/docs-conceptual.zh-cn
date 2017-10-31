---
title: "BackgroundWorker 组件概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "BackgroundWorker"
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
ms.assetid: 64e9b3ab-7443-4a77-ab17-b8b8c0cb3f62
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# BackgroundWorker 组件概述
许多经常执行的操作可能需要很长的执行时间。  例如：  
  
-   图像下载  
  
-   Web 服务调用  
  
-   文件下载和上载（包括点对点应用程序）  
  
-   复杂的本地计算  
  
-   数据库事务  
  
-   本地磁盘访问（相对于内存访问来说其速度很慢）  
  
 类似这样的操作可能导致用户界面在操作运行时挂起。  如果你需要能进行响应的 UI，而且面临与这类操作相关的长时间延迟，<xref:System.ComponentModel.BackgroundWorker> 组件可以提供一种方便的解决方案。  
  
 使用 <xref:System.ComponentModel.BackgroundWorker> 组件，你可以在不同于应用程序的主 UI 线程的另一线程上异步（“在后台”）执行耗时的操作。  若要使用 <xref:System.ComponentModel.BackgroundWorker>，只需要告诉该组件要在后台执行的耗时的辅助方法，然后调用 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 方法。  在辅助方法以异步方式运行的同时，你的调用线程将继续正常运行。  该方法运行完毕后，<xref:System.ComponentModel.BackgroundWorker> 通过引发 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 事件（可选择包含操作结果）可向调用线程发出警报。  
  
 **“组件”**选项卡的**“工具箱”**中提供了 <xref:System.ComponentModel.BackgroundWorker> 组件。  若要向窗体添加 <xref:System.ComponentModel.BackgroundWorker>，请将 <xref:System.ComponentModel.BackgroundWorker> 组件拖到窗体上。  该组件出现在组件栏中，而其属性出现在**“属性”**窗口中。  
  
 若要启动异步操作，请使用 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 方法。  <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 采用一个可选 `object` 参数，该参数可用于将变量传递给辅助方法。  <xref:System.ComponentModel.BackgroundWorker> 类公开 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件，你的辅助线程通过 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序附加到该事件。  
  
 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序采用一个 <xref:System.ComponentModel.DoWorkEventArgs> 参数，该参数具有 <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> 属性。  此属性接收来自 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 的参数，并可以传递给 <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序中调用的辅助方法。  以下示例显示了如何分配名为 `ComputeFibonacci` 的辅助方法的结果。  该示例摘自 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md) 中一个较大的示例。  
  
 [!code-cpp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
 [!code-csharp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
 [!code-vb[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
 有关使用事件处理程序的详细信息，请参阅[事件](../../../../docs/standard/events/index.md)。  
  
> [!CAUTION]
>  使用任何一种多线程都可能引起极为严重和复杂的 Bug。  在实现任何一种使用多线程处理的解决方案之前，请先参考[Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md)。  
  
 有关使用 <xref:System.ComponentModel.BackgroundWorker> 类的详细信息，请参阅[如何：在后台运行操作](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)。  
  
## 请参阅  
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/zh-cn/c731a50c-09c1-4468-9646-54c86b75d269)   
 [如何：实现使用后台操作的窗体](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)