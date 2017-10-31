---
title: "Deciding When to Implement the Event-based Asynchronous Pattern | Microsoft Docs"
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
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "AsyncOperation class"
  - "AsyncCompletedEventArgs class"
ms.assetid: a00046aa-785d-4f7f-a8e5-d06475ea50da
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Deciding When to Implement the Event-based Asynchronous Pattern
基于事件的异步模式提供了一种公开类的异步行为的模式。  引入此模式后，[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 定义了两种公开异步行为的模式：基于 <xref:System.IAsyncResult?displayProperty=fullName> 接口的异步模式和基于事件的模式。  本主题介绍何时适合实现上述两种模式。  
  
 有关使用 <xref:System.IAsyncResult> 接口进行异步编程的更多信息，请参见 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)。  
  
## 一般原则  
 一般而言，您应该在所有可能的情况下使用基于事件的异步模式公开异步功能。  但是，有些要求是基于事件的模式无法满足的。  在这些情况下，除实现基于事件的模式外，可能还需要实现 <xref:System.IAsyncResult> 模式。  
  
> [!NOTE]
>  不实现基于事件的模式而只实现 <xref:System.IAsyncResult> 模式的情况非常少见。  
  
## 准则  
 下面的列表介绍有关应在何时实现基于事件的异步模式的准则：  
  
-   将基于事件的模式用作默认 API 以公开类的异步行为。  
  
-   当类主要用在客户端应用程序（例如 Windows 窗体）中时，不要公开 <xref:System.IAsyncResult> 模式。  
  
-   仅在必须公开 <xref:System.IAsyncResult> 模式才能满足要求时公开该模式。  例如，需要与现有 API 兼容时可能需要公开 <xref:System.IAsyncResult> 模式。  
  
-   不要在不公开基于事件的模式时公开 <xref:System.IAsyncResult> 模式。  
  
-   如果必须公开 <xref:System.IAsyncResult> 模式，应将其作为高级选项公开。  例如，如果生成一个代理对象，则应默认生成基于事件的模式，其中具有一个生成 <xref:System.IAsyncResult> 模式的选项。  
  
-   在 <xref:System.IAsyncResult> 模式实现上生成基于事件的模式实现。  
  
-   避免在同一个类上同时公开基于事件的模式和 <xref:System.IAsyncResult> 模式。  在“较高级别”的类上公开基于事件的模式，在“较低级别”的类上公开 <xref:System.IAsyncResult> 模式。  例如，比较 <xref:System.Net.WebClient> 组件上的基于事件的模式与 <xref:System.Web.HttpRequest> 类上的 <xref:System.IAsyncResult> 模式。  
  
    -   当为了提供兼容性需要在同一个类上公开基于事件的模式和 <xref:System.IAsyncResult> 模式时，同时公开这两种模式。  例如，如果已经释放了一个使用 <xref:System.IAsyncResult> 模式的 API，则需要保留 <xref:System.IAsyncResult> 模式以提供向后兼容性。  
  
    -   如果得到的对象模型复杂性方面的优点大于分开实现的优点，则在同一个类上实现基于事件的模式和 <xref:System.IAsyncResult> 模式。  在一个类上同时公开两种模式比避免公开基于事件的模式效果更好。  
  
    -   如果必须在同一个类上同时公开基于事件的模式和 <xref:System.IAsyncResult> 模式，可使用设置为 <xref:System.ComponentModel.EditorBrowsableState> 的 <xref:System.ComponentModel.EditorBrowsableAttribute> 将 <xref:System.IAsyncResult> 模式实现标记为高级功能。  这指示设计环境（如 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] IntelliSense）不显示 <xref:System.IAsyncResult> 属性和方法。  这些属性和方法仍然是完全可用的，但使用 IntelliSense 的开发人员能够更清楚地查看 API。  
  
## 在公开基于事件的模式的同时公开 IAsyncResult 模式的条件  
 在前面介绍的许多情形中，基于事件的异步模式具有诸多优点，但是，如果性能是最重要的考虑因素，则需要了解这种模式同时也具有一些缺点。  
  
 基于事件的模式不如 <xref:System.IAsyncResult> 模式的情形有三种：  
  
-   被阻止，正在等待一个 <xref:System.IAsyncResult>  
  
-   被阻止，正在等待多个 <xref:System.IAsyncResult> 对象  
  
-   轮询 <xref:System.IAsyncResult> 上的完成情形  
  
 您可以将基于事件的模式用于这些情形，但这种方式比使用 <xref:System.IAsyncResult> 模式较为麻烦。  
  
 开发人员经常将 <xref:System.IAsyncResult> 模式用于通常具有很高的性能要求的服务。  例如，对完成情形的轮询就是一种高性能服务器技术。  
  
 此外，基于事件的模式不如 <xref:System.IAsyncResult> 模式有效，因为它创建更多的对象（尤其是 <xref:System.EventArgs>），而且它会在线程之间进行同步。  
  
 下表列出了决定使用 <xref:System.IAsyncResult> 模式时应遵循的一些建议：  
  
-   仅在明确要求支持 <xref:System.Threading.WaitHandle> 和 <xref:System.IAsyncResult> 对象时公开 <xref:System.IAsyncResult> 模式。  
  
-   仅当已经具有使用 <xref:System.IAsyncResult> 模式的现有 API 时公开 <xref:System.IAsyncResult> 模式。  
  
-   如果已经具有基于 <xref:System.IAsyncResult> 模式的现有 API，则应考虑在下一个版本中也公开基于事件的模式。  
  
-   仅当具有高性能要求，而且经过验证发现基于事件的模式无法满足此要求而 <xref:System.IAsyncResult> 模式能够满足时，才公开 <xref:System.IAsyncResult> 模式。  
  
## 请参阅  
 [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)   
 [实现基于事件的异步模式的最佳做法](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)