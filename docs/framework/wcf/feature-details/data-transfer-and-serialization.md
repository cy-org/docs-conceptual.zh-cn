---
title: "数据传输和序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据序列化 [WCF]"
  - "数据传输 [WCF]"
ms.assetid: 0f03c635-f3e7-4c5c-9463-3cb0135e221e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 数据传输和序列化
在已连接的系统中，服务和客户端依赖于数据交换来完成任何任务。作为服务或客户端的开发人员，您还必须了解 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 如何处理数据和数据序列化以便创建可轻松维护的高效应用程序。  
  
## 本节内容  
 [在服务协定中指定数据传输](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)  
 描述服务中数据传输的基本概念。  
  
 [使用数据协定](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
 描述什么是数据协定以及如何创建和使用它们。  
  
 [数据协定序列化程序](../../../../docs/framework/wcf/feature-details/data-contract-serializer.md)  
 描述如何通过 <xref:System.Runtime.Serialization.DataContractSerializer> 类或 <xref:System.Runtime.Serialization.XmlObjectSerializer> 类的任何扩展完成数据序列化。  
  
 [使用 XmlSerializer 类](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)  
 描述如何使用以及为什么使用 <xref:System.Xml.Serialization.XmlSerializer> 类（<xref:System.Runtime.Serialization.DataContractSerializer> 类的替代类）。  
  
 [使用消息约定](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)  
 描述消息协定如何允许很好的控制 SOAP 消息。  
  
 [使用 Message 类](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)  
 描述如何使用消息类功能。  
  
 [筛选](../../../../docs/framework/wcf/feature-details/filtering.md)  
 描述基于各种条件启用消息预处理的筛选。  
  
 [大型数据和流](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)  
 描述如何发送大数据块，如二进制文件。  
  
 [数据的安全考虑事项](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)  
 描述在对数据传输和序列化进行编程时要注意的项。  
  
 [数据传输体系结构概述](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)  
 描述 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中数据传输的总体设计视图。  
  
## 参考  
 <xref:System.ServiceModel>  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>  
  
 <xref:System.Xml.Serialization.XmlSerializer>  
  
 <xref:System.Runtime.Serialization>  
  
 <xref:System.Xml.Serialization>  
  
## 相关章节  
 [扩展编码器和序列化程序](../../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md)  
  
## 请参阅  
 [最佳做法：数据协定版本管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)   
 [服务版本管理](../../../../docs/framework/wcf/service-versioning.md)