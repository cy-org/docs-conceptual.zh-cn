---
title: "自定义消息格式化程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c07435f3-5214-4791-8961-2c2b61306d71
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 自定义消息格式化程序
消息内容通常为 XML 格式，该格式通常不便于在应用程序中使用。  应用程序操作对象，并且获取和设置其属性。  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用数据协定将 <xref:System.ServiceModel.Channels.Message> 对象转换为应用程序易于处理的对象。  我们将这些过程称为序列化和反序列化。  请注意，这些词同样用于描述传输层对消息连网格式所进行的序列化和反序列化，这是一个不相关的过程。  
  
 如果需要实现通过数据协定无法完成的消息和对象之间的专用转换，则可以使用自定义消息格式化程序。  方法是修改或扩展客户端或服务上的特定协定操作的执行行为。  
  
## 自定义客户端上的消息格式化程序  
 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 接口定义用于控制客户端应用程序的消息与对象之间的转换方法。  
  
 您必须实现此接口。  首先重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> 方法以反序列化消息。  在接收传入消息后，将消息调度到客户端操作之前调用此方法。  
  
 然后，重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> 方法以序列化对象。  在发送传出消息前调用此方法。  
  
 若要将自定义格式化程序插入服务应用程序，请使用操作行为将 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 对象分配给 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> 属性。  有关行为的信息，请参见[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 自定义服务上的消息格式化程序  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 接口定义将服务应用程序中的 <xref:System.ServiceModel.Channels.Message> 对象转换为操作参数并将参数转换为 <xref:System.ServiceModel.Channels.Message> 对象的方法。  
  
 您必须实现此接口。  首先重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> 方法以反序列化消息。  在接收传入消息后，将消息调度到客户端操作之前调用此方法。  
  
 然后，重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> 方法以序列化对象。  在发送传出消息前调用此方法。  
  
 若要将自定义格式化程序插入服务应用程序，请使用操作行为将 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 对象分配给 <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> 属性。  有关行为的信息，请参见[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>   
 [使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)