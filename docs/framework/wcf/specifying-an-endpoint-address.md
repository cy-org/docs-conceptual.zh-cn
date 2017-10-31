---
title: "指定终结点地址 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "寻址的终结点 [WCF]"
ms.assetid: ac24f5ad-9558-4298-b168-c473c68e819b
caps.latest.revision: 41
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 41
---
# 指定终结点地址
与 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务的所有通信都是通过服务的终结点发生的。 每个<xref:System.ServiceModel.Description.ServiceEndpoint>包含<xref:System.ServiceModel.Description.ServiceEndpoint.Address%2A>、<xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A>，和一个<xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A>。 协定指定可用的操作。 绑定指定如何与服务进行通信，而地址指定查找服务的位置。 每个终结点都必须具有一个唯一的地址。 终结点地址都由<xref:System.ServiceModel.EndpointAddress>类，该类包含表示服务的地址统一资源标识符 (URI)，<xref:System.ServiceModel.EndpointAddress.Identity%2A>，这表示该服务的安全标识和可选的集合<xref:System.ServiceModel.EndpointAddress.Headers%2A>。 可选标头提供用于标识终结点或与终结点交互的更多详细寻址信息。 例如，标头可指示如何处理传入消息，终结点应发送答复消息的位置，或在多个实例可用时应使用哪个服务实例处理来自特定用户的传入消息。  
  
## <a name="definition-of-an-endpoint-address"></a>终结点地址的定义  
 在[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]、 <xref:System.ServiceModel.EndpointAddress>按照 Ws-addressing 标准中定义终结点引用 (EPR) 的模型。  
  
 大多数传输的地址 URI 包含四个部分。 例如，“http://www.fabrikam.com:322/mathservice.svc/secureEndpoint”这个 URI 具有以下四个部分：  
  
-   方案：http:  
  
-   计算机：www.fabrikam.com  
  
-   （可选）端口：322  
  
-   路径：/mathservice.svc/secureEndpoint  
  
 作为 EPR 模型的一部分，每个终结点引用都可以包含一些添加额外标识信息的引用参数。 在[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]，这些引用参数建模为实例︰ <xref:System.ServiceModel.Channels.AddressHeader>类。  
  
 可以通过使用代码以强制方式或通过配置以声明方式指定服务的终结点地址。 在代码中定义终结点通常是不可行的，因为已部署服务的绑定和地址通常与在部署服务时所用的绑定和地址不同。 一般而言，使用配置定义服务终结点比使用代码更为可行。 通过将绑定和寻址信息放置在代码之外，可以在更改这些信息之后不必重新编译和重新部署应用程序。 如果在代码或配置中未指定任何终结点，则运行时在该服务实现的每个协定的每个基地址上添加一个默认终结点。  
  
 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中，有两种指定服务终结点地址的方式。 您可以指定与服务关联的每个终结点的绝对地址，也可以提供一个基址<xref:System.ServiceModel.ServiceHost>的一项服务，然后指定与此相对于此基址定义的服务关联的每个终结点的地址。 可以在配置或代码中使用这两种过程来为服务指定终结点地址。 如果不指定相对地址，则服务会使用基址。 也可以为一个服务指定多个基址，但是对于每个传输协议，每个服务只允许有一个基址。 如果有多个终结点，则会使用不同的绑定来配置每个终结点，它们的地址必须是唯一的。 使用相同绑定但使用不同协定的终结点可以使用相同的地址。  
  
 使用 IIS 承载时，不管理<xref:System.ServiceModel.ServiceHost>实例自己。 在 IIS 中承载时，基址始终为在服务的 .svc 文件中指定的地址。 因此，必须对 IIS 承载的服务终结点使用相对终结点地址。 提供完全限定的终结点地址会在服务的部署过程中导致错误。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][部署 Internet 信息服务承载的 WCF 服务](../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)。  
  
## <a name="defining-endpoint-addresses-in-configuration"></a>在配置中定义终结点地址  
 若要在配置文件中定义终结点，请使用[ <> \> ](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017)元素。  
  
 <!-- TODO: review snippet reference [!code[S_UEHelloWorld#5](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp2.config#5)]  -->  
  
 当<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>方法被调用 （即，当宿主应用程序尝试启动服务） 时，系统将查找[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/service.md)元素其 name 属性，指定"UE。Samples.HelloService"。 如果[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/service.md)找到元素，则系统加载指定的类，并使用配置文件中提供的终结点定义创建终结点。 此机制允许你将绑定和寻址信息放置在代码之外，而用两行代码来加载和启动服务。 此方法的优点是在进行这些更改后不必重新编译或重新部署应用程序。  
  
 可选标头中声明[ <> \</> \> ](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)。 下面是用于在配置文件中指定服务终结点的元素的示例，该配置文件分为两个标头：来自 http://tempuri1.org/ 的“黄金”客户端和来自 http://tempuri2.org/ 的“标准”客户端。 调用此服务的客户端必须具有适当[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)其配置文件中。  
  
 <!-- TODO: review snippet reference [!code[S_UEHelloWorld#1](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp.config#1)]  -->  
  
 也可以为个别消息而不是终结点上的所有消息（如前面所示）设置标头。 这通过使用<xref:System.ServiceModel.OperationContextScope>若要在客户端应用程序以向传出消息添加自定义标头中创建新的上下文，如下面的示例中所示。  
  
 [!code-csharp[OperationContextScope#4](../../../samples/snippets/csharp/VS_Snippets_CFX/operationcontextscope/cs/client.cs#4)]
 [!code-vb[OperationContextScope#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationcontextscope/vb/client.vb#4)]  
  
## <a name="endpoint-address-in-metadata"></a>元数据中的终结点地址  
 终结点地址在 Web 服务描述语言 (WSDL) 中表示为对应终结点的 `EndpointReference` 元素内的 WS-Addressing `wsdl:port` (EPR) 元素。 EPR 包含终结点的地址以及所有的地址属性。 请注意，`wsdl:port` 内的 EPR 可替换 `soap:Address`，如下面的示例所示。  
  
  
  
## <a name="defining-endpoint-addresses-in-code"></a>在代码中定义终结点地址  
 可以在代码中使用创建的终结点地址<xref:System.ServiceModel.EndpointAddress>类。 为终结点地址指定的 URI 可以是完全限定的路径，也可以是相对于服务的基址的路径。 下面的代码演示如何创建的实例<xref:System.ServiceModel.EndpointAddress>类，并将其添加到<xref:System.ServiceModel.ServiceHost>承载服务的实例。  
  
 下面的示例演示如何在代码中指定完整的终结点地址。  
  
 [!code-csharp[S_UEHelloWorld#2](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#2)]  
  
 下面的示例演示将相对地址（“MyService”）添加到服务主机的基址中。  
  
 [!code-csharp[S_UEHelloWorld#3](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#3)]  
  
> [!NOTE]
>  属性的<xref:System.ServiceModel.Description.ServiceDescription>在服务应用程序不能修改之后<xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>方法<xref:System.ServiceModel.ServiceHostBase>。 一些成员，如<xref:System.ServiceModel.ServiceHostBase.Credentials%2A>属性和`AddServiceEndpoint`上的方法<xref:System.ServiceModel.ServiceHostBase>和<xref:System.ServiceModel.ServiceHost>，如果在该点之后修改引发异常。 允许修改其他成员，但结果不可确定。  
>   
>  同样，在客户端<xref:System.ServiceModel.Description.ServiceEndpoint>值不能修改调用的后面<xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>上<xref:System.ServiceModel.ChannelFactory>。 <xref:System.ServiceModel.ChannelFactory.Credentials%2A>属性将引发异常，如果在该点之后修改。 可以对其他客户端说明值进行修改而不会出现错误，但结果不可确定。  
>   
>  是否对于服务还是客户端，建议您修改在调用之前说明<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>。  
  
## <a name="using-default-endpoints"></a>使用默认终结点  
 如果在代码或配置中未指定任何终结点，则运行时通过在该服务实现的每个服务协定的每个基地址上添加一个默认终结点，来提供默认终结点。 在代码中或在配置中，可以指定的基址和时添加默认终结点<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>上调用<xref:System.ServiceModel.ServiceHost>。  
  
 如果显式提供终结点，在默认终结点，仍可以通过调用添加<xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints%2A>上<xref:System.ServiceModel.ServiceHost>之前调用<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]默认终结点、 绑定和行为，请参阅[简化配置](../../../docs/framework/wcf/simplified-configuration.md)和[WCF 服务的简化配置](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.EndpointAddress>   
 [服务标识和身份验证](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [终结点创建概述](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [承载](../../../docs/framework/wcf/feature-details/hosting.md)