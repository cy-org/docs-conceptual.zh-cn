---
title: "Windows Communication Foundation 终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "终结点 [WCF]"
ms.assetid: bd0c310f-dd9f-4081-9be2-3db5909850b6
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Windows Communication Foundation 终结点
与 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务的所有通信是通过该服务的终结点进行的。  利用终结点，客户端可访问 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务提供的功能。  
  
 有关如何创建终结点的概述，请参见[终结点创建概述](../../../docs/framework/wcf/endpoint-creation-overview.md)。  每个终结点包含：  
  
-   一个指示要查找终结点位置的地址。  
  
-   一个指定客户端如何与终结点进行通信的绑定。  
  
-   一个标识可用方法的协定。  
  
 有关如何指定终结点的上述各个部分的说明，请参见：  
  
-   [指定终结点地址](../../../docs/framework/wcf/specifying-an-endpoint-address.md)  
  
-   [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)  
  
-   [设计和实现服务](../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
## 本节内容  
 [终结点创建概述](../../../docs/framework/wcf/endpoint-creation-overview.md)  
 描述终结点的结构，并概述如何在配置和代码中定义终结点，以及如何使用运行时提供的默认终结点、绑定和行为。  
  
 [指定终结点地址](../../../docs/framework/wcf/specifying-an-endpoint-address.md)  
 描述如何通过终结点与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务进行通信。  
  
 [如何：在配置中创建服务终结点](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)  
 演示如何在配置中创建服务终结点。  
  
 [如何：在代码中创建服务终结点](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)  
 演示如何在代码中创建服务终结点。  
  
 [发布元数据终结点](../../../docs/framework/wcf/publishing-metadata-endpoints.md)  
 演示如何通过在配置和代码中发布元数据终结点来发布元数据。  
  
## 参考  
 <xref:System.ServiceModel.EndpointAddress>  
  
## 相关章节  
 [基本编程生命周期](../../../docs/framework/wcf/basic-programming-lifecycle.md)