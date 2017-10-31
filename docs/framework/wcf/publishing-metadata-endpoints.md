---
title: "发布元数据终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29cd8a60-dfb7-460c-bf5a-c2b31b782671
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 发布元数据终结点
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务通过发布一个或多个元数据终结点来发布元数据。发布服务元数据之后，可以通过标准协议（如 WS\-MetadataExchange \(MEX\) 和 HTTP\/GET 请求）来使用该元数据。元数据终结点类似于其他服务终结点：它们都有一个地址、一个绑定和一个协定，并且它们都可通过配置或使用代码添加到服务主机。若要启用发布元数据终结点，必须将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 服务行为添加到该服务。  
  
## 本节内容  
 [如何：使用配置文件发布服务的元数据](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 演示如何配置 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务来发布元数据，以使客户端可使用 WS\-MetadataExchange 或包含 `?wsdl` 查询字符串的 HTTP\/GET 请求来检索元数据。  
  
 [如何：使用代码发布服务的元数据](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 演示如何在代码中为 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务启用元数据发布，以使客户端可使用 WS\-MetadataExchange 或包含 `?wsdl` 查询字符串的 HTTP\/GET 请求来检索元数据。  
  
## 请参阅  
 [发布元数据](../../../docs/framework/wcf/feature-details/publishing-metadata.md)