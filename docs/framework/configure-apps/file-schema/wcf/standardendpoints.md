---
title: "&lt;standardEndpoints&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;standardEndpoints&gt;
此配置节用于定义一个标准终结点集合，这些终结点是预配置的可重用终结点。  标准终结点具有一个或多个设置为固定值的地址、绑定和协定特性。  例如，发现终结点具有固定的协定。  此外，还可以使用标准终结点用新属性扩展服务终结点，这与定义自定义绑定相似。  
  
 \<system.ServiceModel\>  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
  
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<announcementEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/announcementendpoint.md)|定义具有固定公告协定的标准终结点。  当分别打开或关闭服务时，服务可以选择通过发送一条联机和脱机公告消息来公告其可用性。  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务在 [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) 元素中指定公告终结点，并使用 AnnouncementClient 执行公告。  如果客户端希望侦听来自其他服务的公告，它实际充当的是 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务；因此，必须在 [\<服务\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md) 节中为该客户端配置公告终结点。|  
|[\<discoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/discoveryendpoint.md)|定义具有固定发现协定的标准终结点。  将此元素添加到服务配置后，该元素将指定侦听发现消息的位置。  将此元素添加到客户端配置后，该元素将指定发送发现查询的位置。|  
|[\<dynamicEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/dynamicendpoint.md)|此配置元素定义一个标准终结点，应用程序通过利用该终结点包含的信息，能够充当可在运行时动态查找终结点地址的客户端程序。|  
|[\<mexEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/mexendpoint.md)|定义具有固定 IMetadataExchange 协定的标准终结点。  由于所有元数据交换终结点都指定 IMetadataExchange 作为其协定，因此可以使用此标准终结点，而不必定义您自己的终结点。|  
|[\<udpAnnoucementEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpannoucementendpoint.md)|定义由服务用于通过 UDP 绑定发送公告消息的标准终结点。  它具有固定协定并支持两个发现版本。  此外，根据 WS\-Discovery 规范（WS\-Discovery 2005 年 4 月版或 WS\-Discovery 1.1 版）中的规定，它还具有固定 UDP 绑定和默认地址值。  您可以指定用于发送和接收公告消息的多播地址。|  
|[\<udpDiscoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpdiscoveryendpoint.md)|定义通过 UDP 多播绑定为发现操作预先配置的标准终结点。  此终结点具有固定协定并支持两个 WS\-Discovery 协议版本。  此外，根据 WS\-Discovery 规范（WS\-Discovery 2005 年 4 月版或 WS\-Discovery 1.1 版）中的规定，它还具有固定 UDP 绑定和默认地址。|  
|[\<webHttpEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpendpoint.md)|定义带有自动添加 [\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) 行为的固定 [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) 绑定的标准终结点。  在编写 REST 服务时，请使用此终结点。|  
|[\<webScriptEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webscriptendpoint.md)|定义带有自动添加 [\<enableWebScript\>](../../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) 行为的固定 [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) 绑定的标准终结点。  在编写从 ASP.NET AJAX 应用程序中调用的服务时，请使用此终结点。|  
|[\<workflowControlEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/workflowcontrolendpoint.md)|定义用于控制工作流实例的执行（创建、运行、挂起、终止等）的标准终结点。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|\<system.ServiceModel\>|所有 WCF 配置元素的根元素。|  
  
## 请参阅  
 [标准终结点](../../../../../docs/framework/wcf/feature-details/standard-endpoints.md)