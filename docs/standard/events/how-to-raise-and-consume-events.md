---
title: "如何：引发和使用事件 | Microsoft Docs"
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
  - "事件 [.NET Framework], 引发"
  - "事件 [.NET Framework], 示例"
  - "引发事件"
ms.assetid: 42afade7-3a02-4f2e-868b-95845f302f8f
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：引发和使用事件
本主题中的示例演示了如何处理事件。  他们包含<xref:System.EventHandler>委托的例子，<xref:System.EventHandler%601>委托和一个特定委托用来说明包含和不包含数据的事件。  
  
 [事件](../../../docs/standard/events/index.md)文章中的示例使用了可以被理解的描述。  
  
## 示例  
 第一个示例演示如何引发和销毁一个没有数据的事件。  它包含一个名为`Counter`that has an event named`ThresholdReached`的类。  当计数器值等于或者超过阈值时，将引发此事件。  The <xref:System.EventHandler>委托和事件联系，因为没有事件的数据被提供。  
  
 [!code-csharp[EventsOverview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programnodata.cs#5)]
 [!code-vb[EventsOverview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1nodata.vb#5)]  
  
## 示例  
 下一个示例演示如何引发和销毁提供数据的事件。  <xref:System.EventHandler%601>委托和事件关联着，并提供一个特定的数据对象的实例。  
  
 [!code-cpp[EventsOverview#6](../../../samples/snippets/cpp/VS_Snippets_CLR/eventsoverview/cpp/programwithdata.cpp#6)]
 [!code-csharp[EventsOverview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdata.cs#6)]
 [!code-vb[EventsOverview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdata.vb#6)]  
  
## 示例  
 下一个示例演示如何声明事件的委托。  委托命名为`ThresholdReachedEventHandler` 这只是一个示例。  典型的，你不必为一个事件申明委托，因为你可以使用<xref:System.EventHandler>或者<xref:System.EventHandler%601>委托。  您极少情况下应声明一个委托，例如，让你的类用于遗留代码不能使用泛型  
  
 [!code-csharp[EventsOverview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdelegate.cs#7)]
 [!code-vb[EventsOverview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdelegate.vb#7)]  
  
## 请参阅  
 [事件](../../../docs/standard/events/index.md)