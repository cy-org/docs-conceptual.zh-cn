---
title: "Latency Modes | Microsoft Docs"
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
  - "garbage collection, intrusiveness"
  - "garbage collection, latency modes"
ms.assetid: 96278bb7-6eab-4612-8594-ceebfc887d81
caps.latest.revision: 41
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 41
---
# Latency Modes
若要回收对象，垃圾回收器必须停止应用程序中所有正在执行的线程。  在某些情况下（例如当应用程序检索数据或显示内容时），关键时刻可能发生完整的垃圾回收，从而妨碍性能。  可以通过将 <xref:System.Runtime.GCSettings.LatencyMode%2A?displayProperty=fullName> 属性设置为其中一个 <xref:System.Runtime.GCLatencyMode?displayProperty=fullName> 值来调节垃圾回收的干扰。  
  
 延迟指垃圾回收干扰应用程序的时间。  在低延迟期间，垃圾回收对正在回收的对象保守性更强、干扰性更弱。  <xref:System.Runtime.GCLatencyMode?displayProperty=fullName> 枚举提供两种低延迟设置：  
  
-   <xref:System.Runtime.GCLatencyMode> 禁止第 2 代集合，仅执行第 0 代和第 1 代集合。  只能在短时间内使用。  在更长时间内，如果系统处于内存压力下，垃圾回收器将触发一次回收，这样会暂时暂停应用程序并中断对时间要求很急的操作。  此设置仅对工作站垃圾回收可用。  
  
-   <xref:System.Runtime.GCLatencyMode> 禁止前景第 2 代回收，仅执行第 0 代、第 1 代和背景第 2 代回收。  它可以长时间使用，并对工作站和服务器垃圾回收都可用。  如果[并发垃圾回收](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)已禁用，则无法使用此设置。  
  
 在低延迟期间，除非发生以下情况，否则禁止第 2 代回收：  
  
-   系统收到操作系统的低内存通知。  
  
-   应用程序代码通过调用 <xref:System.GC.Collect%2A?displayProperty=fullName> 方法并将 `generation` 参数指定为 2 来包含回收。  
  
 下表列出了使用 <xref:System.Runtime.GCLatencyMode> 值的应用程序方案。  
  
|延迟模式|应用程序方案|  
|----------|------------|  
|<xref:System.Runtime.GCLatencyMode>|对于不具有 UI 或服务器端操作的应用程序。<br /><br /> 当[并发垃圾回收](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)禁用时，这是默认模式。|  
|<xref:System.Runtime.GCLatencyMode>|对于具有 UI 的大多数应用程序。<br /><br /> 当[并发垃圾回收](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)启用时，这是默认模式。|  
|<xref:System.Runtime.GCLatencyMode>|对于具有短期时效性操作（操作期间垃圾回收器的干扰可能会引起中断）的应用程序。  例如执行动画呈现或数据采集函数的应用程序。|  
|<xref:System.Runtime.GCLatencyMode>|适用于在有限但有可能更长的时间内具有时效性操作并且在此期间垃圾回收器中断具有破环性的应用程序。  例如，需要随着交易时间内的市场数据变化做出快速响应的应用程序。<br /><br /> 此模式会比其他模式产生更大的托管堆大小。  由于它不压缩托管堆，因此可能产生更多碎片。  确保有足够的可用内存。|  
  
## 低延迟使用指南  
 使用 <xref:System.Runtime.GCLatencyMode> 模式时，请参考以下指南：  
  
-   尽可能地缩短低延迟时段。  
  
-   避免在低延迟时段分配大量内存。  由于垃圾回收回收的对象较少可能出现低内存通知。  
  
-   在低延迟模式下，最大限度减少分配次数，尤其是大型对象堆和固定对象上的分配。  
  
-   知道可以分配的线程。  由于 <xref:System.Runtime.GCSettings.LatencyMode%2A> 属性设置属于进程范围的设置，因此可以在可分配的任何线程上生成 <xref:System.OutOfMemoryException>。  
  
-   使低延迟代码在受约束的执行区域中换行（有关详细信息，请参阅[受约束的执行区域](../../../docs/framework/performance/constrained-execution-regions.md)）。  
  
-   在低延迟期间，可以通过调用 <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%29?displayProperty=fullName> 方法强制进行第 2 代回收。  
  
## 请参阅  
 <xref:System.GC?displayProperty=fullName>   
 [被动回收](../../../docs/standard/garbage-collection/induced.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)