---
title: "&lt;serviceBehavior&gt; 的 &lt;routing&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d8f9c844-4629-4a45-9599-856dc8f01794
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;serviceBehavior&gt; 的 &lt;routing&gt;
提供对路由服务的运行时访问以允许对路由配置进行动态修改。  
  
## 语法  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <routing filterTable=”String”  
         routeOnHeadersOnly="Boolean"  
         SoapProcessingEnabled=”Boolean” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|filterTable|一个字符串，指定路由服务要计算的筛选器所在的路由表的名称。  此值必须与 [\<filterTables\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertables.md) 节中的 [\<filterTable\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertable.md) 元素的 `name` 特性匹配。|  
|routeOnHeaderOnly|一个布尔值，指定筛选器将同时检查消息正文和标头，还是仅检查标头。  默认值为 `true`。|  
|soapProcessingEnabled|一个布尔值，指定是否应进行 SOAP 处理。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行为元素。|  
  
## 备注  
 将此配置元素添加到服务的行为配置中后，此配置元素将对该服务启用路由。  您可以在此元素中指定服务要使用的实际路由表。  
  
 通过使用此配置节，您可以在部署模式发生更改时动态更改路由设置。  在运行时，您可以使用新的路由设置注册自己的路由扩展，路由服务将开始对新消息和会话使用更新后的配置信息，而使正在实施的消息\/会话使用启动时的任何现有规则。这样，您就可以在运行时对路由服务进行会话安全的无回收重新配置。  
  
## 请参阅  
 <xref:System.ServiceModel.Routing.RoutingExtenstion>   
 <xref:System.ServiceModel.Routing.Configuration.RoutingExtenstionElement>