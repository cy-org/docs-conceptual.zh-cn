---
title: "如何：使用 MetadataExchangeClient 检索元数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0754e9dc-13c5-45c2-81b5-f3da466e5a87
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 如何：使用 MetadataExchangeClient 检索元数据
使用 <xref:System.ServiceModel.Description.MetadataExchangeClient> 类可以下载使用 WS\-MetadataExchange \(MEX\) 协议的元数据。检索到的元数据文件作为 <xref:System.ServiceModel.Description.MetadataSet> 对象返回。返回的 <xref:System.ServiceModel.Description.MetadataSet> 对象包含 <xref:System.ServiceModel.Description.MetadataSection> 对象的集合，其中每个对象包含一个特定的元数据方言和一个标识符。您可以将返回的元数据写入文件；或者，如果返回的元数据包含 Web 服务描述语言 \(WSDL\) 文档，则可以使用 <xref:System.ServiceModel.Description.WsdlImporter> 导入元数据。  
  
 接受地址的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 构造函数可对符合该地址的统一资源标识符 \(URI\) 方案的 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 静态类使用绑定。您也可以使用 <xref:System.ServiceModel.Description.MetadataExchangeClient> 构造函数显式指定要使用的绑定。指定的绑定用于解析所有元数据引用。  
  
 与任何其他 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端一样，<xref:System.ServiceModel.Description.MetadataExchangeClient> 类型提供一个用于使用终结点配置名称加载客户端终结点配置的构造函数。指定的终结点配置必须指定 <xref:System.ServiceModel.Description.IMetadataExchange> 约定。不会加载终结点配置中的地址，因此必须使用接受地址的 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 重载之一。当使用 <xref:System.ServiceModel.EndpointAddress> 实例指定元数据地址时，<xref:System.ServiceModel.Description.MetadataExchangeClient> 假设该地址指向 MEX 终结点。如果将元数据地址指定为 URL，则您还需要指定要使用的 <xref:System.ServiceModel.Description.MetadataExchangeClientMode>（MEX 或 HTTP GET）。  
  
> [!IMPORTANT]
>  默认情况下，<xref:System.ServiceModel.Description.MetadataExchangeClient> 为您解析所有引用，包括 WSDL 和 XML 架构导入和包括的内容。通过将 <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 属性设置为 `false`，可以禁用此功能。使用 <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> 属性可以控制要解析的最大引用数。可以与 `MaxReceivedMessageSize` 属性一起对绑定使用此属性，以控制所检索的元数据的量。  
  
### 使用 MetadataExchangeClient 获取元数据  
  
1.  通过显式指定一个绑定、一个终结点配置名称或元数据的地址，创建一个新的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 对象。  
  
2.  配置 <xref:System.ServiceModel.Description.MetadataExchangeClient> 以适合您的需要。例如，您可以指定请求元数据时要使用的凭据、控制元数据引用的解析方式和设置 <xref:System.ServiceModel.Description.MetadataExchangeClient.OperationTimeout%2A> 属性以控制元数据请求超时之前必须在多长时间内返回。  
  
3.  通过调用 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 方法之一获取包含检索的元数据的 <xref:System.ServiceModel.Description.MetadataSet> 对象。请注意，如果您在构造 <xref:System.ServiceModel.Description.MetadataExchangeClient> 时显式指定了地址，则只能使用不带参数的 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 重载。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.ServiceModel.Description.MetadataExchangeClient> 下载和枚举元数据文件。  
  
 [!code-csharp[MetadataResolver#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/metadataresolver/cs/client.cs#3)]  
  
## 编译代码  
 若要编译此代码示例，必须引用 System.ServiceModel.dll 程序集并导入 <xref:System.ServiceModel.Description> 命名空间。  
  
## 请参阅  
 <xref:System.ServiceModel.Description.MetadataResolver>   
 <xref:System.ServiceModel.Description.MetadataExchangeClient>   
 <xref:System.ServiceModel.Description.WsdlImporter>