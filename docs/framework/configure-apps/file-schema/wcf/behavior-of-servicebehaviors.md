---
title: "&lt;serviceBehaviors&gt; 的 &lt;behavior&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 78fc0a08-55de-416a-ac12-a5e6ffc9a987
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;serviceBehaviors&gt; 的 &lt;behavior&gt;
`behavior` 元素包含服务行为的设置集合。  每个行为都按其 `name` 进行索引。  服务可使用 [\<endpoint（终结点）\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) 元素的 `behaviorConfiguration` 特性通过此名称链接到每个行为。  这样，终结点可以共享公共行为配置而不用重新定义设置。  从 [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] 开始，不要求绑定和行为具有名称。  有关默认配置以及无名称绑定和行为的更多信息，请参见[简化配置](../../../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
> [!NOTE]
>  特定于 Windows 工作流活动的行为元素（如 [\<sendMessageChannelCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sendmessagechannelcache.md) 元素）记录在 [\<serviceBehaviors\> 的 \<behavior\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md) 页中。  
  
## 语法  
  
```  
  
<system.ServiceModel>  
  <behaviors>  
    <serviceBehaviors>  
       <behavior name="String" />  
    </serviceBehaviors>  
  </behaviors>  
</system.ServiceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|name|一个包含行为的配置名称的唯一字符串。  此值是用户定义的一个字符串，该字符串必须是唯一的，因为它将充当元素的标识字符串。  从 [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] 开始，不要求绑定和行为具有名称。  有关默认配置以及无名称绑定和行为的更多信息，请参见[简化配置](../../../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)|包含 DataContractSerializer 的配置数据。|  
|[\<persistenceProvider\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistenceprovider.md)|指定要使用的持久性提供程序实现的类型以及用于持久性操作的超时值。|  
|[\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md)|提供对路由服务的运行时访问以允许对路由配置进行动态修改。|  
|[\<serviceAuthenticationManager\>](../../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthenticationmanager.md)|提供一个工作流配置元素，该元素在服务级别建立传输、消息或发起方的有效性。|  
|[\<serviceAuthorization\>](../../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)|指定用于授予服务操作访问权限的设置。|  
|[\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|指定要用于对服务进行身份验证的凭据以及与客户端凭据验证相关的设置。|  
|[\<serviceDebug\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md)|指定 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务的调试和帮助信息功能。|  
|[\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md)|指定服务终结点的可发现性。|  
|[\<serviceMetadata\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md)|指定服务元数据的发布和相关信息。|  
|[\<serviceSecurityAudit\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md)|指定用于在服务操作过程中启用安全事件审核的设置。|  
|[\<serviceThrottling\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicethrottling.md)|指定 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的限制机制。|  
|[\<serviceTimeouts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicetimeouts.md)|指定服务的超时。|  
|[\<workflowRuntime\>](../../../../../docs/framework/configure-apps/file-schema/wcf/workflowruntime.md)|指定用于承载基于工作流的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的 WorkflowRuntime 实例的设置。|  
|[\<useRequestHeadersForMetadataAddress\>](../../../../../docs/framework/configure-apps/file-schema/wcf/userequestheadersformetadataaddress.md)|允许从请求消息头中检索元数据地址信息。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)|服务行为元素的集合。|