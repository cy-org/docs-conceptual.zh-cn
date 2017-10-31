---
title: "Timers | Microsoft Docs"
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
  - "threading [.NET Framework], timers"
  - "timers, about timers"
ms.assetid: 7091500d-be18-499b-a942-95366ce185e5
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Timers
计时器是使您能够指定要在指定时间调用的委托的轻量对象。  线程池中的线程执行等待操作。  
  
 使用 <xref:System.Threading.Timer?displayProperty=fullName> 类是非常简单的。  需要创建一个 **Timer**，将 <xref:System.Threading.TimerCallback> 委托传递给回调方法；还需要创建一个表示将被传递给回调的状态的对象，以及初始引发时间和表示回调调用之间的时间段的时间。  若要取消挂起的计时器，请调用 **Timer.Dispose** 函数。  
  
> [!NOTE]
>  有两个其他计时器类。  <xref:System.Windows.Forms.Timer?displayProperty=fullName> 类是使用可视化设计器的控件，旨在用于用户界面上下文中；它对用户界面线程引发事件。  <xref:System.Timers.Timer?displayProperty=fullName> 类派生自 <xref:System.ComponentModel.Component>，所以它可与可视化设计器一同使用；它还引发事件，但对 <xref:System.Threading.ThreadPool> 线程引发这些事件。  <xref:System.Threading.Timer?displayProperty=fullName> 类对 <xref:System.Threading.ThreadPool> 线程进行回调，并且根本不使用事件模型。  它还为回调方法提供状态对象，而其他计时器则不提供。  它是极度轻量级的。  
  
 下面的代码示例启动一个计时器，该计时器在一秒（1000 毫秒）后启动，每秒增加一个刻度，直到按下**“Enter”**键。  包含对计时器的引用的变量是类级别字段，以确保计时器在运行期间不会被垃圾回收。  有关主动垃圾回收的更多信息，请参见 <xref:System.GC.KeepAlive%2A>。  
  
 [!code-cpp[System.Threading.Timer#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.Timer/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.Timer#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.Timer/CS/source2.cs#2)]
 [!code-vb[System.Threading.Timer#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.Timer/VB/source2.vb#2)]  
  
## 请参阅  
 <xref:System.Threading.Timer>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)