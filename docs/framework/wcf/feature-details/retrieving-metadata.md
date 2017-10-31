---
title: "检索元数据 | Microsoft Docs"
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
  - "元数据 [WCF], 检索"
ms.assetid: 18d8ba4c-af0f-4827-a50b-4202d767bacc
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 检索元数据
元数据检索是从元数据终结点（如 WS\-MetadataExchange \(MEX\) 元数据终结点或 HTTP\/GET 元数据终结点）请求和检索元数据的过程。  
  
## 从命令行使用 Svcutil.exe 检索元数据  
 通过使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具并传递 `/target:metadata` 开关和地址，您可以使用 WS\-MetadataExchange 或 HTTP\/GET 请求来检索服务的元数据。Svcutil.exe 在指定地址下载元数据并将文件保存到磁盘上。Svcutil.exe 在内部使用一个 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例，并从配置中加载名称与作为输入传递给 Svcutil.exe 的地址方案相匹配的 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点配置。  
  
## 使用 MetadataExchangeClient 以编程方式检索元数据  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 可以使用标准化协议（如 WS\-MetadataExchange 和 HTTP\/GET 请求）检索元数据。这两种协议均受 <xref:System.ServiceModel.Description.MetadataExchangeClient> 类型支持。您可以通过提供元数据终结点的地址和一个可选绑定，使用 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 类型来检索服务元数据。由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例使用的绑定可以是 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 静态类中的默认绑定之一、用户提供的绑定或从 `IMetadataExchange` 协定的终结点配置加载的绑定。<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 也可以使用 <xref:System.Net.HttpWebRequest> 类型来解析 HTTP URL 对元数据的引用。  
  
 默认情况下，<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例与单个 <xref:System.ServiceModel.ChannelFactory> 实例关联。通过重写 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 虚拟方法，您可以更改或替换由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 使用的 <xref:System.ServiceModel.ChannelFactory?displayProperty=fullName> 实例。同样，通过重写 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=fullName> 虚拟方法，可以更改或替换由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 使用的 <xref:System.Net.HttpWebRequest> 实例以发出 HTTP\/GET 请求。  
  
## 本节内容  
 [如何：使用 Svcutil.exe 下载元数据文档](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)  
 演示如何使用 Svcutil.exe to 下载元数据文档。  
  
 [如何：使用 MetadataResolver 动态获取绑定元数据](../../../../docs/framework/wcf/feature-details/how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)  
 演示如何使用 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName> 在运行时动态获取绑定元数据。  
  
 [如何：使用 MetadataExchangeClient 检索元数据](../../../../docs/framework/wcf/feature-details/how-to-use-metadataexchangeclient-to-retrieve-metadata.md)  
 演示如何使用 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 类将元数据文件下载到包含要写入到文件或用于其他用途的 <xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName> 对象的 <xref:System.ServiceModel.Description.MetadataSet?displayProperty=fullName> 对象。  
  
## 请参阅  
 <xref:System.ServiceModel.Description.MetadataExchangeClient>