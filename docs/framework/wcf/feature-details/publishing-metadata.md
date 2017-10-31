---
title: "发布元数据 | Microsoft Docs"
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
  - "元数据 [WCF], 发布"
ms.assetid: 3a56831a-cabc-45c0-bd02-12e2e9bd7313
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 发布元数据
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务通过发布一个或多个元数据终结点来发布元数据。发布服务元数据之后，可以通过标准协议（如 WS\-MetadataExchange \(MEX\) 和 HTTP\/GET 请求）来使用该元数据。元数据终结点类似于其他服务终结点，因为它们都有一个地址、一个绑定和一个协定，并且它们都可通过配置或命令代码添加到服务主机。  
  
## 发布元数据终结点  
 若要发布 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的终结点，首先必须将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 服务行为添加到该服务。添加一个 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 实例将允许服务公开元数据终结点。添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 服务行为之后，就可以公开支持 MEX 协议或响应 HTTP\/GET 请求的元数据终结点。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 使用 <xref:System.ServiceModel.Description.WsdlExporter> 导出元数据服务中的所有服务终结点。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 导出元数据从一种服务，请参阅 [导出和导入元数据](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 添加一个 <xref:System.ServiceModel.Description.ServiceMetadataExtension> 实例作为服务主机的扩展。<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> 提供了元数据发布协议的实现。还可以使用 <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> 通过访问 <xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A?displayProperty=fullName> 属性来在运行时获取服务的元数据。  
  
### MEX 元数据终结点  
 要添加元数据终结点使用的墨西哥协议，将服务终结点添加到您使用的服务主机 `IMetadataExchange` 服务合同。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 包括 <xref:System.ServiceModel.Description.IMetadataExchange> 接口使用此服务合同名称，您可以使用的一部分 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的编程模型。WS\-MetadataExchange 终结点，即 MEX 终结点，可以使用静态工厂方法在 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类中公开的四种默认绑定之一来匹配 Svcutil.exe 之类的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工具所使用的默认绑定。还可以使用自己的自定义绑定来配置 MEX 元数据终结点。  
  
### HTTP GET 元数据终结点  
 若要将元数据终结点添加到响应 HTTP\/GET 请求的服务，请将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 属性设置为 `true`。将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 属性设置为 `true` 还可以配置使用 HTTPS 的元数据终结点。  
  
## 本节内容  
 [如何：使用配置文件发布服务的元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 演示如何配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务来发布元数据，以使客户端可使用 WS\-MetadataExchange 或包含 `?wsdl` 查询字符串的 HTTP\/GET 请求来检索元数据。  
  
 [如何：使用代码发布服务的元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 演示如何在代码中为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务启用元数据发布，以使客户端可使用 WS\-MetadataExchange 或包含 `?wsdl` 查询字符串的 HTTP\/GET 请求来检索元数据。  
  
## 参考  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>  
  
 <xref:System.ServiceModel.Description.IMetadataExchange>  
  
 <xref:System.ServiceModel.Description.ServiceMetadataExtension>  
  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings>  
  
## 请参阅  
 [导出和导入元数据](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)