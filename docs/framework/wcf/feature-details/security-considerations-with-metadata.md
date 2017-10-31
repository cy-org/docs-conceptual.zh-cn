---
title: "元数据的安全注意事项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e78ef8ab-4f63-4656-ab93-b1deab2666d5
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# 元数据的安全注意事项
使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的元数据功能时，应该考虑发布、检索和使用服务元数据时所带来的安全隐患。  
  
## 何时发布元数据  
 默认情况下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务不会发布元数据。  若要发布 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的元数据，您必须通过向您的服务中添加元数据终结点来显式启用元数据发布（请参见[发布元数据](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)）。  禁用元数据发布可以缩小服务的攻击面，同时降低意外泄漏信息的风险。  并非所有服务都必须发布元数据。  如果不必发布元数据，请考虑使其处于关闭状态。  请注意，您仍可以使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 从服务程序集直接生成元数据和客户端代码。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用 Svcutil.exe 导出元数据的更多信息，请参见[如何：使用 Svcutil.exe 将元数据从已编译的服务代码中导出](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)。  
  
## 使用安全绑定发布元数据  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的默认元数据绑定不是安全的，它们允许对元数据进行匿名访问。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务发布的服务元数据包含关于服务的详细说明，可能有意或无意地包含敏感信息。  例如，服务元数据可能包含有关不希望对外公布的基础结构操作信息。  要防止对服务元数据进行未经授权的访问，您可以对元数据终结点使用安全绑定。  元数据终结点响应可以使用安全套接字层 \(SSL\) 保护元数据的 HTTP\/GET 请求。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [如何：保护元数据终结点](../../../../docs/framework/wcf/feature-details/how-to-secure-metadata-endpoints.md).  
  
 保护元数据终结点还为请求者提供一种安全检索服务元数据的方法，避免篡改或伪造的风险。  
  
## 仅使用受信任的元数据  
 您可以使用服务元数据自动构造调用服务所需的运行时组件。  还可以在设计时使用元数据来开发客户端应用程序，或在运行时使用元数据动态更新客户端调用服务所使用的绑定。  
  
 当以不安全方式检索服务元数据时，元数据可能会被篡改或伪造。  被篡改的元数据可能会使您的客户端重定向到恶意服务，包含有害的安全设置或包含恶意 XML 结构。  元数据文档可能很大，并且会频繁地保存到文件系统中。  若要防止篡改或伪造，请使用安全绑定来请求服务元数据（如果有安全绑定）。  
  
## 使用安全技术处理元数据  
 使用标准化协议（如 WS\-MetadataExchange \(MEX\)）通过网络从服务频繁检索服务元数据。  许多元数据格式包含引用机制，用以指向其他元数据。  <xref:System.ServiceModel.Description.MetadataExchangeClient> 类型会为您自动处理 Web 服务描述语言 \(WSDL\) 文档、XML 架构和 MEX 文档中的引用。  通过检索到的元数据创建的 <xref:System.ServiceModel.Description.MetadataSet> 对象的大小与使用的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 实例的 <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> 值以及该 <xref:System.ServiceModel.Description.MetadataExchangeClient> 实例正在使用的绑定的 `MaxReceivedMessageSize` 值成正比。  将这些配额设置为您的方案所指示的相应值。  
  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，服务元数据将被处理为 XML。  当处理 XML 文档时，应用程序应保护自己免受恶意 XML 结构的破坏。  处理 XML 时请使用具有适当配额的 `XmlDictionaryReader`，还要为您的 <xref:System.Xml.XmlReader> 实例将 <xref:System.Xml.XmlReaderSettings> 对象的 <xref:System.XML.XmlReaderSettings.ProhibitDtd%2A> 属性设置为 `true`。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的元数据系统是可扩展的，元数据扩展可以在应用程序配置文件中注册（请参见[扩展元数据系统](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)）。  元数据扩展可以运行任意代码，因此，您应利用适合的访问控制列表 \(ACL\) 来保护应用程序配置文件，并仅注册受信任的元数据扩展实现。  
  
## 验证生成的客户端  
 通过从不受信任的源中检索到的元数据生成客户端代码时，请验证生成的客户端代码，以确保生成的客户端符合您的客户端应用程序安全策略。  您可以使用验证行为来检查客户端绑定上的设置，也可以采用可视化方式来检查工具生成的代码。  有关如何实现用于验证行为的客户端的示例，请参见[客户端验证](../../../../docs/framework/wcf/samples/client-validation.md)。  
  
## 保护应用程序配置文件  
 服务的应用程序配置文件可以控制是否发布元数据以及如何发布元数据。  最好利用适当的访问控制列表 \(ACL\) 来保护应用程序配置文件，以确保攻击者无法修改此类设置。  
  
## 请参阅  
 [如何：保护元数据终结点](../../../../docs/framework/wcf/feature-details/how-to-secure-metadata-endpoints.md)   
 [安全性](../../../../docs/framework/wcf/feature-details/security.md)