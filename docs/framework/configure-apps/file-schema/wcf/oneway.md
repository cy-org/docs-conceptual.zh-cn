---
title: "&lt;oneWay&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00e67e0e-77c0-4695-9138-c0997b0e5f3c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;oneWay&gt;
对自定义绑定启用数据包路由并使用单向方法。  
  
## 语法  
  
```  
  
<oneWay packetRoutable="Boolean">  
        <channelPoolSettings  
           idleTimeout"TimeSpan"  
          leaseTimeout"TimeSpan"  
          maxOutboundConnectionsPerEndpopint=”Integer” />  
```  
  
```  
  
</oneWay>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`packetRoutable`|一个布尔值，指定是否启用数据包路由。  默认值为 `false`。|  
|`MaxAcceptedChannels`|一个整数，指定可接受的最大通道数。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<channelPoolSettings\>](../../../../../docs/framework/configure-apps/file-schema/wcf/channelpoolsettings.md)|一个 <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement> 对象，包含当前通道的通道池的属性。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<绑定\>](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## 备注  
 若要启用数据包路由，必须使用此元素提供的单向转换层。  用户可以创建一个自定义绑定，将此绑定置于具有会话功能或请求\/答复传输的上层，使之可进行数据包路由。  如果希望以更自然的方式公开单向方法，则此元素也十分有用。  在这一层上可应用更多的转换，如复合双工和可靠消息。  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.OneWayBindingElement>   
 <xref:System.ServiceModel.Configuration.OneWayElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)