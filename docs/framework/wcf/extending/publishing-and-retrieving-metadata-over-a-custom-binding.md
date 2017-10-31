---
title: "通过自定义绑定发布和检索元数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 904e11b4-d90e-45c6-9ee5-c3472c90008c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 通过自定义绑定发布和检索元数据
<xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 提供对向服务添加元数据终结点的支持。这些元数据终结点可对具有 `?wsdl` QueryString 的 URL 处的 HTTP GET 请求作出响应，并可对在 WS\-MetadataExchange \(MEX\) 规范中定义的 WS\-Transfer GET 请求作出响应。MEX 终结点可实现 <xref:System.ServiceModel.Description.IMetadataExchange?displayProperty=fullName> 协定。  
  
## 通过自定义绑定发布元数据  
 通过将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A?displayProperty=fullName> 属性设置为 `true`，可以启用 HTTP GET 元数据终结点和 HTTPS GET 元数据终结点。无法配置这些终结点的绑定。  
  
 不过，<xref:System.ServiceModel.Description.IMetadataExchange> 协定可与任何终结点（包括使用自定义绑定的终结点）一起使用，这是因为 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点与任何其他 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务终结点相同。如果您了解如何修改系统提供的绑定的配置，或者了解如何配置 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>，则可以将绑定配置为与 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点一起使用。  
  
## 通过自定义绑定检索元数据  
 可以从 HTTP Get 和 HTTPS Get 元数据终结点使用标准 HTTP 或 HTTPS GET 请求检索元数据。  
  
 若要从 MEX 元数据终结点检索元数据，您通常可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 所支持的标准 MEX 绑定之一。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=fullName>.<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 类型和 Svcutil.exe 工具将根据指定元数据终结点的地址自动选择这些标准 MEX 绑定之一。  
  
 如果 MEX 元数据终结点使用与标准 MEX 绑定之一不同的其他绑定，则您可以使用代码或通过提供 <xref:System.ServiceModel.Description.IMetadataExchange> 客户端终结点配置来配置由 <xref:System.ServiceModel.Description.MetadataExchangeClient> 所使用的绑定。Svcutil.exe 工具可自动从其配置文件中加载一个 <xref:System.ServiceModel.Description.IMetadataExchange> 客户端终结点配置，该配置具有与元数据终结点地址的 URI 方案相同的名称。  
  
## 安全  
 通过自定义绑定发布元数据时，请确保该绑定提供您的元数据所要求的安全支持。例如，若要防止信息泄漏，并确保客户端具有获取元数据的权限，您可以通过将 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点配置为要求身份验证和加密的方式使元数据和应用程序更加安全。示例[自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)演示了这种方案。  
  
## 请参阅  
 [保证服务的安全](../../../../docs/framework/wcf/securing-services.md)   
 [WS\-MetadataExchange 绑定](../../../../docs/framework/wcf/extending/ws-metadataexchange-bindings.md)   
 [如何：配置自定义 WS\-Metadata Exchange 绑定](../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)   
 [如何：通过非 MEX 绑定检索元数据](../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)