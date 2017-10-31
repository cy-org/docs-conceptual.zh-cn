---
title: "终结点地址 | Microsoft Docs"
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
  - "地址 [WCF]"
  - "WCF [WCF], 地址"
  - "Windows Communication Foundation [WCF], 地址"
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 终结点地址
每个终结点都具有与其关联的地址，该地址用于查找和标识终结点。此地址主要包括指定终结点位置的统一资源标识符 \(URI\)。终结点地址在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 编程模型中由 <xref:System.ServiceModel.EndpointAddress> 类表示，该类包含一个可选的 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 属性（允许由与一个终结点交换消息的其他终结点对该终结点进行身份验证）和一组可选的 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 属性（定义到达服务所需的任何其他 SOAP 头）。可选头提供其他的更详细寻址信息以标识服务终结点或与之交互。终结点的地址在网络上表示为 WS\-Addressing 终结点引用 \(EPR\)。  
  
## 地址的 URI 结构  
 大多数传输的地址 URI 包含四个部分。例如，下面详细列举了 URI http:\/\/www.fabrikam.com:322\/mathservice.svc\/secureEndpoint 的四个部分：  
  
-   方案：http:  
  
-   计算机：www.fabrikam.com  
  
-   （可选）端口：322  
  
-   路径：\/mathservice.svc\/secureEndpoint  
  
## 定义服务地址  
 您可以通过使用代码以强制方式或通过配置以声明方式指定服务的终结点地址。在代码中定义终结点通常不可行，因为已部署的服务的绑定和地址通常不同于开发服务时使用的绑定和地址。一般而言，使用配置定义服务终结点比使用代码更为可行。通过在代码之外保存绑定和寻址信息，无须重新编译或重新部署应用程序即可更改它们。  
  
### 在配置中定义地址  
 若要在配置文件中定义终结点，请使用 [\<endpoint（终结点）\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) 元素。有关详细信息和示例，请参见[指定终结点地址](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)。  
  
### 在代码中定义地址  
 在代码中可以使用 <xref:System.ServiceModel.EndpointAddress> 类创建终结点地址。有关详细信息和示例，请参见[指定终结点地址](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)。  
  
### WSDL 中的终结点  
 在 WSDL 中终结点地址也可以表示为对应终结点的 `wsdl:port` 元素内的 WS\-Addressing EPR 元素。EPR 包含终结点的地址以及所有的地址属性。有关详细信息和示例，请参见[指定终结点地址](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)。  
  
## .NET Framework 3.5 中的多个 IIS 绑定支持  
 Internet 服务提供商通常在同一服务器和站点上承载许多应用程序，以增加站点密度和降低总拥有成本。这些应用程序通常绑定到不同的基址。Internet 信息服务 \(IIS\) 网站可以包含多个应用程序。可以通过一个或多个 IIS 绑定访问站点中的应用程序。  
  
 IIS 绑定提供了两则信息：绑定协议和绑定信息。绑定协议定义发生通信所依据的方案，而绑定信息是用于访问站点的信息。  
  
 下面的示例演示可以存在于 IIS 绑定中的组件：  
  
-   绑定协议：HTTP  
  
-   绑定信息：IP 地址、端口、主机头  
  
 IIS 可以为每个站点指定多个绑定，这会导致每个方案有多个基址。在 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] 之前，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不支持一个方案有多个地址；如果指定了多个地址，则在激活期间引发 <xref:System.ArgumentException>。  
  
 通过 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]，Internet 服务提供商可以在同一站点上使用同一方案的不同基址承载多个应用程序。  
  
 例如，一个站点可能包含以下基址：  
  
-   http:\/\/payroll.myorg.com\/Service.svc  
  
-   http:\/\/shipping.myorg.com\/Service.svc  
  
 使用 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]，可以在配置文件中指定 AppDomain 级别的前缀筛选器。通过 [\<baseAddressPrefixFilters\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md) 元素（它包含前缀列表）可以执行此操作。基于可选前缀列表筛选由 IIS 提供的传入基址。默认情况下，如果未指定前缀，则使所有地址通过。指定前缀导致仅使该方案的匹配基址通过。  
  
 下面的配置代码示例使用前缀筛选器。  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 在前面的示例中，net.tcp:\/\/payroll.myorg.com:8000 和 http:\/\/shipping.myorg.com:8000 是其各自方案的唯一基址（已使它们通过）。  
  
 `baseAddressPrefixFilter` 不支持通配符。  
  
 IIS 提供的基址可能具有绑定到 `baseAddressPrefixFilters` 列表中不存在的其他方案的地址。未筛选出这些地址。  
  
## .NET Framework 4 及更高版本中的多个 IIS 绑定支持  
 从 .NET 4 开始，通过将 <xref:System.ServiceModel.ServiceHostingEnvironment> 的 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> 设置为 True，您无需选取单个基址便可实现对 IIS 中多个绑定的支持。此支持限于 HTTP 协议方案。  
  
 下面的配置代码示例在 [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) 上使用 multipleSiteBindingsEnabled。  
  
```  
  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled=”true” >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 对于 HTTP 和非 HTTP 协议，当使用此设置启用多个网站绑定时，忽略任何 baseAddressPrefixFilter 设置。  
  
 有关详细信息和示例，请参见[支持多个 IIS 站点绑定](../../../../docs/framework/wcf/feature-details/supporting-multiple-iis-site-bindings.md)和 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A>。  
  
## 在 WCF 服务中扩展寻址  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的默认寻址模型使用终结点地址 URI 以达到以下目的：  
  
-   指定服务侦听地址，即终结点侦听消息的位置，  
  
-   指定 SOAP 地址筛选器，即终结点期望作为 SOAP 头的地址。  
  
 可以单独指定用于其中每个目的的值，从而允许涉及有用方案的若干寻址扩展：  
  
-   SOAP 媒介：客户端发送的消息在到达其最终目的地之前遍历一个或多个处理消息的其他服务。SOAP 媒介可以执行各种任务，如对消息进行缓存、路由、负载平衡或架构验证。此方案是通过将消息发送到单独的物理地址（`via`，以媒介为目标），而不是仅发送到逻辑地址（`wsa:To`，以最终目的地为目标）完成的。  
  
-   终结点的侦听地址是专用 URI，它设置为与其 `listenURI` 属性不同的值。  
  
 `via` 指定的传输地址是将消息发往 `to` 参数指定的、服务所在的某个其他远程地址途中应该最初发送到的地址。在大多数 Internet 方案中，`via` URI 与服务的最终 `to` 地址的 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 属性相同。仅当必须执行手动路由时，才区分这两个地址。  
  
### 寻址头  
 除了其基本 URI 外，终结点可以按一个或多个 SOAP 头寻址。这一点在其中很有用的一组方案是一组 SOAP 媒介方案，其中终结点要求该终结点的客户端包括以媒介为目标的 SOAP 头。  
  
 可以通过两种方法定义自定义地址头 \- 使用代码或使用配置：  
  
-   在代码中，通过使用 <xref:System.ServiceModel.Channels.AddressHeader> 类创建自定义地址头，然后在构造 <xref:System.ServiceModel.EndpointAddress> 时使用它。  
  
-   在配置中，自定义 [\<页眉\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)[\<endpoint\> 被指定为](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017) 元素的子元素。  
  
 配置通常比代码更可取，因为它允许您在部署后更改头。  
  
### 自定义侦听地址  
 可以将侦听地址设置为与终结点的 URI 不同的值。在要公开的 SOAP 地址为公共 SOAP 媒介的地址，而终结点实际侦听的地址是专用网络地址的媒介方案中，这是很有用的。  
  
 可以通过使用代码或配置指定自定义侦听地址：  
  
-   在代码中，通过将 <xref:System.ServiceModel.Description.ClientViaBehavior> 类添加到终结点的行为集合指定自定义侦听地址。  
  
-   在配置中，通过服务 [\<endpoint\>](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017) 元素的 `ListenUri` 属性指定自定义侦听地址。  
  
### 自定义 SOAP 地址筛选器  
 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 与任何 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 属性联合使用，以定义终结点的 SOAP 地址筛选器 \(<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>\)。默认情况下，此筛选器验证传入消息是否具有与终结点的 URI 匹配的 `To` 消息头，以及所有必需的终结点头是否存在于消息中。  
  
 在某些方案中，终结点接收抵达基础传输的所有消息，而不仅仅是具有相应 `To` 头的消息。若要启用这一点，用户可以使用 <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> 类。  
  
## 请参阅  
 [指定终结点地址](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)   
 [服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)