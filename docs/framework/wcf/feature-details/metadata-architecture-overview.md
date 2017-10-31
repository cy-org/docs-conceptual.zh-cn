---
title: "元数据体系结构概述 | Microsoft Docs"
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
  - "元数据 [WCF], 概述"
ms.assetid: 1d37645e-086d-4d68-a358-f3c5b6e8205e
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# 元数据体系结构概述
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 为导出、发布、检索和导入元数据服务提供丰富的基础设施。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用元数据来描述如何与服务终结点进行交互，以便工具例如，Svcutil.exe，可以自动生成用于访问服务的客户端代码。  
  
 构成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 元数据基础结构的大多数类型驻留在 <xref:System.ServiceModel.Description> 命名空间中。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 <xref:System.ServiceModel.Description.ServiceEndpoint> 类描述服务中的终结点。可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为服务终结点生成元数据或者导入服务元数据以生成 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将服务的元数据表示为 <xref:System.ServiceModel.Description.MetadataSet> 类型的实例，其结构被强附加到在 WS\-MetadataExchange 中定义的元数据序列化格式。<xref:System.ServiceModel.Description.MetadataSet> 类型将实际的服务元数据（如 Web 服务描述语言 \(WSDL\) 文档、XML 架构文档或 WS\-Policy 表达式）作为 <xref:System.ServiceModel.Description.MetadataSection> 实例的集合绑定。每个 <xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName> 实例都包含特定的元数据方言和标识符。<xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName> 在其 <xref:System.ServiceModel.Description.MetadataSection.Metadata%2A?displayProperty=fullName> 属性中可能包含以下项：  
  
-   原始元数据。  
  
-   一个 <xref:System.ServiceModel.Description.MetadataReference> 实例。  
  
-   一个 <xref:System.ServiceModel.Description.MetadataLocation> 实例。  
  
 <xref:System.ServiceModel.Description.MetadataReference?displayProperty=fullName> 实例指向另一个元数据交换 \(MEX\) 终结点和 <xref:System.ServiceModel.Description.MetadataLocation?displayProperty=fullName> 实例指向使用 HTTPURL 的元数据文档。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持使用 WSDL 文件来描述服务终结点、服务合同、绑定、消息交换模式、消息和实施的一项服务的故障消息。服务使用的数据类型在 WSDL 文档中使用 XML 架构进行描述。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][架构导入和导出](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md).可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 导出和导入服务行为的 WSDL 扩展、协定行为和扩展服务功能的绑定元素。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][导出 WCF 扩展的自定义元数据](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md).  
  
## 导出服务元数据  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，“元数据导出”是描述服务终结点并将它们投影到客户端可以用来了解如何使用服务的并行标准化表示的过程。若要从 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例导出元数据，请使用 <xref:System.ServiceModel.Description.MetadataExporter> 抽象类的实现。<xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 实现生成包装在 <xref:System.ServiceModel.Description.MetadataSet> 实例中的元数据。  
  
 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 类提供了一个框架，用于生成描述终结点绑定的功能和要求及其关联操作、消息和错误的策略表达式。在 <xref:System.ServiceModel.Description.PolicyConversionContext> 实例中可捕获这些策略表达式。然后 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 实现可以将这些策略表达式附加到它生成的元数据。  
  
 当生成供 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 实现使用的 <xref:System.ServiceModel.Description.PolicyConversionContext> 对象时，<xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 调入在 <xref:System.ServiceModel.Description.ServiceEndpoint> 的绑定中实现 <xref:System.ServiceModel.Description.IPolicyExportExtension> 接口的每个 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName>。通过在 <xref:System.ServiceModel.Channels.BindingElement> 类型的自定义实现上实现 <xref:System.ServiceModel.Description.IPolicyExportExtension> 接口，可以导出新策略断言。  
  
 <xref:System.ServiceModel.Description.WsdlExporter> 类型是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 所包含的 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 抽象类的实现。<xref:System.ServiceModel.Description.WsdlExporter> 类型使用附加的策略表达式生成 WSDL 元数据。  
  
 若要导出自定义 WSDL 元数据或终结点行为的 WSDL 扩展、协定行为或服务终结点中的绑定元素，可以实现 <xref:System.ServiceModel.Description.IWsdlExportExtension> 接口。在生成 WSDL 文档时，<xref:System.ServiceModel.Description.WsdlExporter> 为实现 <xref:System.ServiceModel.Description.IWsdlExportExtension> 接口的绑定元素、操作行为、协定行为和终结点行为查看 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例。  
  
## 发布服务元数据  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务通过公开一个或多个元数据终结点来发布元数据。使用标准协议（如 MEX 和 HTTP\/GET 请求）发布服务元数据可使服务元数据变得可用。元数据终结点与其他服务终结点类似，都具有地址、绑定和协定。可以在配置中或在代码中将元数据终结点添加到服务主机。  
  
 若要发布 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的元数据终结点，必须首先将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 服务行为的实例添加到服务。将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 实例添加到服务，使服务增添了通过公开一个或多个元数据终结点发布元数据的功能。添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 服务行为后，可以公开支持 MEX 协议的元数据终结点或响应 HTTP\/GET 请求的元数据终结点。  
  
 若要添加使用 MEX 协议的元数据终结点，请将服务终结点添加到使用名为 IMetadataExchange 的服务协定的服务主机。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 定义具有此服务协定名称的 <xref:System.ServiceModel.Description.IMetadataExchange> 接口。WS\-MetadataExchange 终结点或 MEX 终结点可以使用由 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类上静态工厂方法公开的四个默认绑定之一，以匹配 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工具（如 Svcutil.exe）使用的默认绑定。也可以使用自定义绑定配置 MEX 元数据终结点。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 使用  <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=fullName> 导出元数据服务中的所有服务终结点。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 导出元数据从一种服务，请参阅 [导出和导入元数据](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)。  
  
 通过将 <xref:System.ServiceModel.Description.ServiceMetadataExtension> 实例作为服务主机的扩展添加，<xref:System.ServiceModel.Description.ServiceMetadataBehavior> 增强了服务主机。<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> 提供了元数据发布协议的实现。还可以使用 <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> 通过访问 <xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A> 属性来在运行时获取服务的元数据。  
  
> [!CAUTION]
>  如果在应用程序配置文件中添加 MEX 终结点，然后尝试在代码中向服务主机添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>，则会得到以下异常：  
>   
>  System.InvalidOperationException: 在服务 Service1 实现的协定列表中找不到协定名称“ImetadataExchange”。将 ServiceMetadataBehavior 添加到配置文件或直接添加到 ServiceHost，以启用对该协定的支持。  
>   
>  通过在配置文件中 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 或在代码中同时添加终结点和 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>，可以解决此问题。  
>   
>  有关在应用程序配置文件中添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 的示例，请参见[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。有关在代码中添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 的示例，请参见[自承载](../../../../docs/framework/wcf/samples/self-host.md)示例。  
  
> [!CAUTION]
>  当发布公开两个不同服务协定（两个服务协定包含具有相同名称的操作）的服务的元数据时，会引发异常。例如，如果有一个服务公开了一个名为 ICarService 的服务协定，该服务协定具有一个 Get\(Car c\) 操作，且同一服务还公开了一个名为 IBookService 的服务协定，该服务协定具有一个 Get\(Book b\) 操作，则当生成该服务的元数据时，会引发异常或显示错误消息。若要解决此问题，请执行下列操作之一：  
>   
>  -   重命名其中的一项操作。  
> -   将 <xref:System.ServiceModel.OperationContractAttribute.Name%2A> 设置为其他名称。  
> -   使用 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 属性将其中一项操作的命名空间设置为其他命名空间。  
  
## 检索服务元数据  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以使用标准化协议（如 WS\-MetadataExchange 和 HTTP）检索服务元数据。这两种协议均受 <xref:System.ServiceModel.Description.MetadataExchangeClient> 类型支持。通过提供地址和可选绑定，使用 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 类型检索服务元数据。由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例使用的绑定可以是 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 静态类中的默认绑定之一、用户提供的绑定或从 `IMetadataExchange` 协定的终结点配置加载的绑定。<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 也可以使用 <xref:System.Net.HttpWebRequest> 类型来解析 HTTP URL 对元数据的引用。  
  
 默认情况下，<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例与单个 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 实例关联。通过重写 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 虚拟方法，您可以更改或替换由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 使用的 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 实例。同样，通过重写 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=fullName> 虚拟方法，可以更改或替换由 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 使用的 <xref:System.Net.HttpWebRequest?displayProperty=fullName> 实例以发出 HTTP\/GET 请求。  
  
 通过使用 Svcutil.exe 工具并传递 **\/target:metadata** 开关和地址，您可以使用 WS\-MetadataExchange 或 HTTP\/GET 请求来检索服务的元数据。Svcutil.exe 下载指定位置的元数据并将文件保存到磁盘。Svcutil.exe 在内部使用 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 实例，并加载其名称与传递到 Svcutil.exe 的地址的方案（如果存在）匹配的 MEX 终结点配置（从应用程序配置文件）。否则，Svcutil.exe 默认使用由 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 静态工厂类型定义的绑定之一。  
  
## 导入服务元数据  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，元数据导入是从服务的元数据生成服务或其组成部分的抽象表示的过程。例如，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以从服务的 WSDL 文档导入 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例、<xref:System.ServiceModel.Channels.Binding> 实例或 <xref:System.ServiceModel.Description.ContractDescription> 实例。若要在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中导入服务元数据，请使用 <xref:System.ServiceModel.Description.MetadataImporter> 抽象类的实现。派生自 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 类的类型实现对导入元数据格式的支持，这些元数据格式利用了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 WS\-Policy 导入逻辑。  
  
 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 实现收集附加到 <xref:System.ServiceModel.Description.PolicyConversionContext> 对象中服务元数据的策略表达式。然后，通过在 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> 属性中调用 <xref:System.ServiceModel.Description.IPolicyImportExtension> 接口的实现 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 在导入元数据的过程中处理策略。  
  
 通过将自己的 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 接口实现添加到 <xref:System.ServiceModel.Description.IPolicyImportExtension> 实例上的 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> 集合，可以添加对将新策略断言导入到 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 的支持。或者，可以在客户端应用程序配置文件中注册策略导入扩展。  
  
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 类型是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 所包含的 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 抽象类的实现。<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 类型可以导入含有附加策略（这些策略捆绑在 <xref:System.ServiceModel.Description.MetadataSet> 对象中）的 WSDL 元数据。  
  
 通过实现 <xref:System.ServiceModel.Description.IWsdlImportExtension> 接口，然后将实现添加到 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 实例上的 <xref:System.ServiceModel.Description.WsdlImporter.WsdlImportExtensions%2A> 属性，可以添加对导入 WSDL 扩展的支持。<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 还可以加载在客户端应用程序配置文件中注册的 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName> 接口的实现。  
  
## 动态绑定  
 如果终结点的绑定更改，或者希望为使用相同协定但具有不同绑定的终结点创建一个通道，则可以动态更新用来为服务终结点创建通道的绑定。可以使用 <xref:System.ServiceModel.Description.MetadataResolver> 静态类在运行时为实现特定协定的服务终结点检索和导入元数据。然后可以使用导入的 <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=fullName> 对象为所需终结点创建客户端或通道工厂。  
  
## 请参阅  
 <xref:System.ServiceModel.Description>   
 [元数据格式](../../../../docs/framework/wcf/feature-details/metadata-formats.md)   
 [导出和导入元数据](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)   
 [发布元数据](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)   
 [检索元数据](../../../../docs/framework/wcf/feature-details/retrieving-metadata.md)   
 [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [元数据的安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)   
 [扩展元数据系统](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)