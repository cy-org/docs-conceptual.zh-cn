---
title: "单并发模式中的有序消息处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 单并发模式中的有序消息处理
WCF 不对处理消息的顺序进行任何保证，除非基础通道是会话通道。例如，使用 MsmqInputChannel（不是会话信道）的 WCF 服务将无法按顺序处理消息。有一些情况，开发人员可能会想要按顺序处理行为，但不想使用会话。本主题介绍在单个并发模式中运行服务时，如何配置这种行为。  
  
## 有序消息处理  
 名为 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> 的新特性已添加到 <xref:System.ServiceModel.ServiceBehaviorAttribute>。当 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A>设置为 true，并且<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 设置为 <xref:System.ServiceModel.ConcurrencyMode> 时，将按顺序处理发送到服务的消息。下面的代码段演示如何设置这些特性。  
  
```  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
  
```  
  
 如果 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 设置为任何其他值，则引发 <xref:System.InvalidOperationException>。  
  
## 请参阅  
 [会话、实例化和并发](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)   
 [并发](../../../../docs/framework/wcf/samples/concurrency.md)