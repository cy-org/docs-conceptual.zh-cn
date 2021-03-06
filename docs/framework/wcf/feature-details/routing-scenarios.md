---
title: "路由方案 | Microsoft Docs"
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
  - "路由 [WCF], 方案"
ms.assetid: ec22f308-665a-413e-9f94-7267cb665dab
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# 路由方案
尽管路由服务可高度自定义，但是，如果要从头开始创建新配置，设计高效的路由逻辑很富有挑战性。  然而，大多数路由服务配置都遵循一些常见方案。  虽然这些方案可能并不直接适用于特定配置，但是了解如何配置路由服务以处理这些方案有助于您了解路由服务。  
  
## 常见方案  
 路由服务最基本的用途是聚合多个目标终结点以减少公开给客户端应用程序的终结点数目，然后使用消息筛选器将各消息路由到正确的目标。  可以根据逻辑或物理处理要求（如必须由特定服务处理的消息类型）或任意业务需要（如对来自特定源的消息提供优先级处理）路由消息。  下表列出了一些常见方案及其使用时间：  
  
|方案|何时使用|  
|--------|----------|  
|服务版本控制|需要支持服务的多个版本，或者可能会在将来部署更新服务|  
|服务数据分区|必须跨多个主机对服务进行分区|  
|动态更新|必须在运行时动态重新配置路由逻辑以处理不断变化的服务部署|  
|多播|必须将一条消息发送到多个终结点|  
|协议桥接|通过一个传输协议接收消息，且目标终结点使用不同协议|  
|错误处理|需要为网络中断和通信故障提供弹性|  
  
> [!NOTE]
>  虽然提供的多种方案都特定于某些业务需求或处理要求，但计划支持动态更新和利用错误处理通常可认为是最佳做法，因为它们允许在运行时修改路由逻辑并从暂时的网络和通信故障恢复。  
  
### 服务版本控制  
 引入新的服务版本时，您通常需要维护以前的版本，直到所有客户端都已转换到新服务为止。  如果服务是需要数天、数周甚至数月才能完成的长时间运行的进程，这一点尤为重要。  通常，这要求为新服务实现一个新终结点地址，同时维护以前版本的原始终结点。  
  
 使用路由服务，您可以公开一个终结点以接收来自客户端应用程序的消息，然后基于消息内容将各消息路由到正确的服务版本。  最基本的实现涉及在消息中添加自定义标头，用于指示将对消息进行处理的服务版本。  路由服务可以使用 XPathMessageFilter 检查各消息中是否存在自定义标头，并将消息路由到适当的目标终结点。  
  
 有关创建服务版本控制配置所采用的步骤，请参见[如何：服务版本控制](../../../../docs/framework/wcf/feature-details/how-to-service-versioning.md)。  有关使用 XPathMessageFilter 根据自定义标头路由消息的示例，请参见[高级筛选器](../../../../docs/framework/wcf/samples/advanced-filters.md)示例。  
  
### 服务数据分区  
 设计分布式环境时，通常需要在多台计算机之间分布处理负载以提供高可用性，降低各计算机上的处理负载，或为特定消息子集提供专用资源。  虽然路由服务无法取代专用负载平衡解决方案，但是它具有执行基于内容的路由的功能，可以利用这一功能将其他类似的消息路由到特定目标。  例如，您可能需要单独处理从特定客户端接收的消息和从其他客户端接收的消息。  
  
 有关创建服务数据分区配置所采用的步骤，请参见[如何：划分服务数据](../../../../docs/framework/wcf/feature-details/how-to-service-data-partitioning.md)。  有关使用筛选器根据 URL 和自定义标头对数据进行分区的示例，请参见[高级筛选器](../../../../docs/framework/wcf/samples/advanced-filters.md)示例。  
  
### 动态路由  
 通常需要修改路由配置以满足不断变化的业务需求，例如，在服务的较新版本中添加一个路由，更改路由条件或更改筛选器将特定消息路由到的目标终结点。  路由服务允许您通过 <xref:System.ServiceModel.Routing.RoutingExtension>（用于在运行时提供新 RoutingConfiguration）实现此操作。  新配置将立即生效，但只影响路由服务处理的任何新会话。  
  
 有关实现动态路由所采用的步骤，请参见[如何：动态更新](../../../../docs/framework/wcf/feature-details/how-to-dynamic-update.md)。  有关使用动态路由的示例，请参见[动态重新配置](../../../../docs/framework/wcf/samples/dynamic-reconfiguration.md)示例。  
  
### 多播  
 路由消息时，您通常需要将各消息路由到一个特定的目标终结点。  但是，有时您可能需要将消息副本路由到多个目标终结点。  若要执行多播路由，必须满足以下条件：  
  
-   通道形状不能为请求\-答复（但可以为单向或双工），因为请求\-答复要求客户端应用程序在响应请求时只能接收一个答复。  
  
-   多个筛选器在计算消息时必须返回 **true**。  
  
 如果满足这些条件，则与返回 true 的筛选器关联的每个目标终结点都将收到消息的一个副本。  
  
### 协议桥接  
 在不同 SOAP 协议之间路由消息时，路由服务使用 WCF API 将消息从一个协议转换为另一个协议。  如果路由服务公开的服务终结点与消息路由到的客户端终结点使用不同的协议，则会自动执行上述转换。  如果使用的协议不是标准协议，则可以禁用此行为；但是您必须提供您自己的桥接代码。  
  
 .  有关使用路由服务在协议之间转换消息的示例，请参见[桥接和错误处理](../../../../docs/framework/wcf/samples/bridging-and-error-handling.md)示例。  
  
### 错误处理  
 在分布式环境中，通常会遇到暂时的网络或通信故障。  如果不采用中介服务（如路由服务），则处理此类故障的重担将落在客户端应用程序上。  如果客户端应用程序不包含发生网络或通信故障时进行重试的特定逻辑且不知道备用位置，用户可能会遇到这样的情况：必须多次提交某条消息才能使目标服务成功处理该消息。  客户可能会将该应用程序视为不可靠的应用程序，进而可能影响客户对该应用程序的满意度。  
  
 路由服务将为遇到网络或通信相关故障的消息提供可靠的错误处理功能，从而纠正此状况。  通过创建可能的目标终结点列表并将此列表与各消息筛选器相关联，可以避免由于只有一个可能的终结点而导致的单点故障。  出现故障时，路由服务会尝试将消息传递到列表中的下一个终结点，直到已传递此消息、出现非通信故障或所有终结点已耗尽。  
  
 有关配置错误处理所采用的步骤，请参见[如何：错误处理](../../../../docs/framework/wcf/feature-details/how-to-error-handling.md)。  有关实现错误处理的示例，请参见[桥接和错误处理](../../../../docs/framework/wcf/samples/bridging-and-error-handling.md)和[高级错误处理](../../../../docs/framework/wcf/samples/advanced-error-handling.md)示例。  
  
### 本节内容  
 [如何：服务版本控制](../../../../docs/framework/wcf/feature-details/how-to-service-versioning.md)  
  
 [如何：划分服务数据](../../../../docs/framework/wcf/feature-details/how-to-service-data-partitioning.md)  
  
 [如何：动态更新](../../../../docs/framework/wcf/feature-details/how-to-dynamic-update.md)  
  
 [如何：错误处理](../../../../docs/framework/wcf/feature-details/how-to-error-handling.md)  
  
## 请参阅  
 [路由简介](../../../../docs/framework/wcf/feature-details/routing-introduction.md)