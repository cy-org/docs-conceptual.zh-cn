---
title: "Weak References | Microsoft Docs"
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
  - "weak references, short"
  - "weak references, using"
  - "weak references, long"
  - "garbage collection, weak references"
ms.assetid: 6a600fe5-3af3-4c64-82da-10a0a8e2d79b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Weak References
如果应用程序的代码可以访问一个正由该程序使用的对象，垃圾回收器就不能收集该对象，  那么，就认为应用程序对该对象具有强引用。  
  
 弱引用允许应用程序访问对象，同时也允许垃圾回收器收集相应的对象。  如果不存在强引用，则弱引用的有限期只限于收集对象前的一个不确定的时间段。  使用弱引用时，应用程序仍可对该对象进行强引用，这样做可防止该对象被收集。  但始终存在这样的风险：垃圾回收器在重新建立强引用之前先处理该对象。  
  
 弱引用特别适合以下对象：占用大量内存，但通过垃圾回收功能回收以后很容易重新创建。  
  
 假设 Windows 窗体应用程序中的一个树视图向用户显示了复杂的选项层次结构。  如果基础数据量很大，则用户使用应用程序中的其他部分时，在内存中保留该树会导致效率低下。  
  
 当用户切换到应用程序的其他部分时，可使用 <xref:System.WeakReference> 类来创建对该树的弱引用，并销毁所有强引用。  当用户切换回该树时，应用程序会尝试获得对该树的强引用，如果得到，就不必重新构造该树。  
  
 要对某个对象建立弱引用，请使用要跟踪的对象的实例创建一个 <xref:System.WeakReference>。  然后为该对象设置该 <xref:System.WeakReference.Target%2A> 属性，将该对象原始的引用设置为 `null`。  有关代码示例，请参见类库中的 <xref:System.WeakReference>。  
  
## 短弱引用和长弱引用  
 可创建短弱引用或长弱引用：  
  
-   Short  
  
     垃圾回收功能回收对象后，短弱引用的目标会变为 `null`。  弱引用本身是托管对象，和任何其他托管对象一样需要经过垃圾回收。短弱引用是 <xref:System.WeakReference> 的默认构造函数。  
  
-   Long  
  
     调用对象的 <xref:System.Object.Finalize%2A> 方法后，会保留长弱引用。  这样，您就可以重新创建该对象，但该对象仍保持不可预知的状态。  要使用长引用，请在 <xref:System.WeakReference> 构造函数中指定 `true`。  
  
     如果对象的类型没有 <xref:System.Object.Finalize%2A> 方法，则会应用短弱引用功能，该弱引用只在目标被收集之前有效，运行终结器之后可以随时收集目标。  
  
 要建立强引用并重新使用该对象，请将 <xref:System.WeakReference> 的 <xref:System.WeakReference.Target%2A> 属性强制转换为该对象的类型。  如果 <xref:System.WeakReference.Target%2A> 属性返回 `null`，则表示对象已被收集；否则，您可继续使用该对象，因为应用程序已重新获得了对它的强引用。  
  
## 使用弱引用的准则  
 仅在必要时使用长弱引用，因为在终止后对象的状态是不可预知的。  
  
 避免对小对象使用弱引用，因为指针本身可能和对象一样大，或者比对象还大。  
  
 不应将弱引用作为内存管理问题的自动解决方案，  而应开发一个有效的缓存策略来处理应用程序的对象。  
  
## 请参阅  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)