---
title: "AutoResetEvent | Microsoft Docs"
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
  - "threading [.NET Framework], AutoResetEvent class"
  - "AutoResetEvent class"
ms.assetid: 6d39c48d-6b37-4a9b-8631-f2924cfd9c18
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# AutoResetEvent
<xref:System.Threading.AutoResetEvent> 类表示一个本地等待处理事件，在释放了单个等待线程以后，该事件会在终止时自动重置。  该类表示它的基类（即 <xref:System.Threading.EventWaitHandle>）的特殊情况。  有关自动重置事件的使用和功能，请参见 [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) 概念文档。  
  
 在释放了单个等待线程以后，系统会自动将一个 <xref:System.Threading.AutoResetEvent> 对象重置为非终止。  如果没有任何线程在等待，则该事件对象的状态将保持已发信号的状态。  <xref:System.Threading.AutoResetEvent> 对应于 Win32 `CreateEvent` 调用，它对 `bManualReset` 参数指定 `false`。  
  
 有关使用 <xref:System.Threading.AutoResetEvent> 的示例，请参见[监视器](../Topic/Monitors.md)。  
  
## 请参阅  
 <xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.Monitor>   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)