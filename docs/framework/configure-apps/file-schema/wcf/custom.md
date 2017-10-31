---
title: "&lt;自定义&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6f65a00-bd1a-4d4a-955a-fe009ec02ab8
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;自定义&gt;
指定自定义对等解析程序服务的设置。  
  
## 语法  
  
```  
  
<custom address="Uri"  
   resolverType="String">  
      <headers/>  
   <identity/>  
</peerResolver>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`address`|一个 URI，指定承载自定义对等解析程序服务的对等节点的终结点地址。|  
|`resolverType`|一个字符串值，指定自定义对等解析程序服务的类型。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<标识\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|指定配置了此元素的自定义对等解析程序的标识。  此元素的类型为 <xref:System.ServiceModel.Configuration.IdentityElement>。|  
|[\<页眉\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|一个地址标头集合，可用于由自定义对等解析程序处理的 SOAP 消息。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<resolver\>](../../../../../docs/framework/configure-apps/file-schema/wcf/resolver.md)|一个对等解析程序，可用于将对等网格 ID 解析为一组对等节点地址，这些地址表示参与网格的若干节点。|  
  
## 备注  
 此元素可定义自定义对等解析程序服务的基本设置，其中包括执行服务的对等解析程序的终结点地址和所有特定绑定设置。  有关创建自定义解析程序的更多信息，请参见[Adding a Custom Resolver to a PeerChannel Application](http://msdn.microsoft.com/zh-cn/12aa3787-2962-439c-ad27-46523c8b0419)。  
  
## 请参阅  
 <xref:System.Servicemodel.PeerResolvers.CustomPeerResolverService>   
 <xref:System.ServiceModel.PeerResolvers.PeerCustomResolverSettings>   
 <xref:System.ServiceModel.Configuration.PeerResolverElement.Custom%2A>   
 <xref:System.ServiceModel.Configuration.PeerCustomResolverElement>   
 [对等解析程序](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md)   
 [Adding a Custom Resolver to a PeerChannel Application](http://msdn.microsoft.com/zh-cn/12aa3787-2962-439c-ad27-46523c8b0419)