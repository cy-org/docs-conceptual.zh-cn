---
title: "被动回收 | Microsoft Docs"
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
  - "垃圾回收，强制"
ms.assetid: 019008fe-4708-4e65-bebf-04fd9941e149
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# 被动回收
在大多数情况下，垃圾回收器可以确定执行回收的最佳时间，应让其独立运行。  在某些不常发生的情况下，强制回收可以提高应用程序的性能。  在这些情况下，可使用 <xref:System.GC.Collect%2A?displayProperty=fullName> 方法强制垃圾回收，以引发垃圾回收。  
  
 当应用程序代码中某个特定的点上使用的内存量大量减少时，请使用 <xref:System.GC.Collect%2A?displayProperty=fullName> 方法。  例如，如果应用程序使用包含若干个控件的复杂对话框，则在对话框关闭时调用 <xref:System.GC.Collect%2A> 可能会通过立即回收该对话框使用的内存来提高性能。  务必确保应用程序不会过于频繁地引发垃圾回收，否则当垃圾回收器在非最佳时候尝试回收对象时，可能会使性能降低。  您可提供 <xref:System.GCCollectionMode?displayProperty=fullName> 枚举值到 <xref:System.GC.Collect%2A> 方法以仅当集合有效的情况下进行收集，如下一节所述。  
  
## GC 回收模式  
 您可以使用 <xref:System.GC.Collect%2A?displayProperty=fullName> 方法之一重载，它包括 <xref:System.GCCollectionMode> 值用来指定如下所述的强制回收行为。  
  
|`GCCollectionMode` 值|描述|  
|--------------------------|--------|  
|<xref:System.GCCollectionMode>|对 .NET Framework 运行的版本使用默认垃圾回收设置。|  
|<xref:System.GCCollectionMode>|强制立即执行垃圾回收。  这与调用 <xref:System.GC.Collect?displayProperty=fullName> 重载等效。  它导致所有分代的全部阻塞集合。<br /><br /> 通过在强制即时全阻塞垃圾回收之前，将 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName> 属性设置为 <xref:System.Runtime.GCLargeObjectHeapCompactionMode?displayProperty=fullName> 压缩大对象堆。|  
|<xref:System.GCCollectionMode>|使垃圾回收器可以确定当前时间是否是回收对象的最佳时间。<br /><br /> 垃圾回收器可能判定收集效率不够高，因此收集不合理，在这种情况下将返回而不回收对象。|  
  
## 背景或块集合  
 可调用 <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29?displayProperty=fullName> 方法重载以指定是否阻止生成的集合。  执行的集合类型取决于该方法的 `mode` 和 `blocking` 参数的结合。  `mode` 是 <xref:System.GCCollectionMode> 枚举的成员，`blocking` 是 <xref:System.Boolean> 值。  下表总结了 `mode` 和 `blocking` 参数的交互。  
  
|`mode`|`blocking` \= `true`|`blocking` \= `false`|  
|------------|--------------------------|---------------------------|  
|<xref:System.GCCollectionMode> 或 <xref:System.GCCollectionMode>|尽快执行阻塞集合。  如果后台回收正在进行并生成 0 或 1，<xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 方法将立即触发阻止回收，并在则回收完成后返回。  如果后台回收正在进行，并且 `generation` 参数为 2，该方法将等待后台回收结束后触发阻止生成 2 次回收，并返回。|尽快执行集合。  <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 方法请求后台回收，但并不确定；根据环境，阻塞式回收仍可执行。  如果后台回收正在进行，则此方法将立即返回。|  
|<xref:System.GCCollectionMode>|可根据垃圾回收器和 `generation` 参数的状态执行阻塞集合。  垃圾回收器尝试提供最佳性能。|可根据垃圾回收器的状态执行集合。  <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> 方法请求后台回收，但并不确定；根据环境，阻塞式回收仍可执行。  垃圾回收器尝试提供最佳性能。  如果后台回收正在进行，则此方法将立即返回。|  
  
## 请参阅  
 [Latency Modes](../../../docs/standard/garbage-collection/latency.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)