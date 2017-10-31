---
title: "How to: Implement a Client of the Event-based Asynchronous Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "components [.NET Framework], asynchronous"
  - "AsyncOperation class"
  - "threading [Windows Forms], asynchronous features"
  - "AsyncCompletedEventArgs class"
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Implement a Client of the Event-based Asynchronous Pattern
下面的代码示例演示如何使用符合 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md) 的组件。  此示例的窗体使用[How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)中介绍的  `PrimeNumberCalculator` 组件。  
  
 当运行使用此示例的项目时，您将看到一个带有一个网格和两个按钮（**“启动新任务”**和**“取消”**）的“Prime Number Calculator”窗体。  您可以连续单击**“启动新任务”**按钮数次。每单击一次，异步操作都会开始一次计算，来确定随机生成的测试数字是不是质数。  窗体将定期显示进度和增量结果。  给每个操作分配一个唯一的任务 ID。  计算的结果显示在**“结果”**列中；如果测试数字不是质数，则将它标记为**“合数”**，并显示它的第一个约数。  
  
 可使用**“取消”**按钮取消任何挂起的操作。  可以作出多个选择。  
  
> [!NOTE]
>  大多数数字不是质数。  如果在完成几个操作后没有找到质数，则只需启动更多的任务，最终您会找到一些质数的。  
  
## 示例  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#10)]  
  
## 请参阅  
 <xref:System.ComponentModel.AsyncOperation>   
 <xref:System.ComponentModel.AsyncOperationManager>   
 <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>