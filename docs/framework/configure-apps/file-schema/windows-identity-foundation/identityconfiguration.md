---
title: "&lt;identityConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1db76253-07da-447b-9e7a-3705c7228cf4
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# &lt;identityConfiguration&gt;
指定的服务级别标识设置。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration  
      name=xs:string  
      saveBootstrapContext=xs:boolean>  
      maximumClockSkew=TimeSpan >  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|name|标识配置节的名称。  您可以使用此名称来引用特定的配置节。  如果不是`name`指定属性，部分所定义的默认配置。  被动联合身份验证的情况下，总是使用默认配置。  有关更多信息，请参见 [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 元素。|  
|saveBootstrapContext|指定是否应包含引导标记的会话令牌中。  该值还通过设置设置标记处理程序集合上`saveBootstrapContext`属性上[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)元素。  上的标记处理程序集合值将替代该服务上设置的值。|  
|maximumClockSkew|A <xref:System.TimeSpan> ，它指定允许的最大时钟不一致。  执行时间敏感型业务，如验证登录会话的到期时间时，可以控制允许的最大时钟不一致。  默认为 5 分钟，"00: 05: 00"。  有关如何指定<xref:System.TimeSpan>的值，请参阅[Timespan Values](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_TimespanValues)。  也可以在标记处理程序集合上通过设置设置的最大时钟偏差`maximumClockSkew`属性上[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)元素。  上的标记处理程序集合值将替代该服务上设置的值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|注册用于会话令牌和令牌重做检测的缓存。  可指定服务级别或安全令牌的处理程序集。  可选。|  
|[\<certificateValidation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidation.md)|控制用于验证证书的标记处理程序的设置。  可指定服务级别或安全令牌的处理程序集。  可选。|  
|[\<claimsAuthenticationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthenticationmanager.md)|为传入的声明的声明身份验证管理器中注册。  可选。|  
|[\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md)|为传入的声明的声明授权管理器中注册。  可选。|  
|[\<claimTypeRequired\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimtyperequired.md)|指定所需的传入安全令牌的报销申请的一组。  可选。|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|指定安全标记处理程序的集合。  可指定零个或更多的安全令牌的处理程序的集合。  可选。|  
|[\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md)|启用标记重做检测并指定标记的过期时间。  可指定服务级别或安全令牌的处理程序集。  可选。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<system.identityModel\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md)|提供有关启用 Windows 标识基础 \(WIF\) 选项，在应用程序中的配置。|  
  
## 备注  
 多个标识可能定义的配置，每个都有一个唯一的名称。  行为如下所示：  
  
1.  如果不是`<identityConfiguration>`元素被指定。  标识的默认配置是在运行时创建并使用默认值填充。  
  
2.  如果一个`<identityConfiguration>`元素被指定。  它是默认标识配置。  这种是否被命名或未命名的。  
  
3.  如果多个`<identityConfiguration>`指定的元素。  未命名的元素指定的默认标识配置。  当指定多个推荐的`<identityConfiguration>`元素，其中之一应是未命名。  
  
> [!WARNING]
>  如果您指定多个`<identityConfiguration>`元素，其中之一应是未命名。  未命名的元素将默认标识配置。  
  
 某些设置中指定`<identityConfiguration>`元素可以被重写安全标记处理程序集合上的设置或者设置单独的安全令牌的处理程序。  
  
> [!IMPORTANT]
>  使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类来提供基于声明的访问控制，在代码中，所引用的标识配置`<federationConfiguration>`元素配置的索赔授权管理器和策略，用于做出授权决定。  是这样，即使在不是被动的 Web 方案，例如 Windows 资格） 应用程序或不是基于 Web 的应用程序的方案中。  如果应用程序不是被动的 Web 应用程序中， [\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md)元素 （和它的子策略元素，如果有的话） 的引用的标识配置将应用的唯一设置。  所有其他设置都被忽略。  有关更多信息，请参见 [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 元素。  
  
 `<identityConfiguration>`元素都由<xref:System.IdentityModel.Configuration.IdentityConfigurationElement>类。  标识配置节由<xref:System.IdentityModel.Configuration.IdentityConfiguration>类。  
  
> [!IMPORTANT]
>  指定下列元素的子元素作为`<identityConfiguration>`元素已被否决，虽然仍支持向后兼容性的行为。  这些元素，而下指定[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)元素。  
>   
>  -   [\<audienceUris\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/audienceuris.md)  
> -   [\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)  
> -   [\<issuerTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuertokenresolver.md)  
> -   [\<serviceTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicetokenresolver.md)  
  
## 示例  
 下面的示例创建一个名为"alternateConfiguration"的标识配置。  标识配置指定的默认设置。  
  
```  
<system.identityModel>  
    <identityConfiguration name="alternateConfiguration"/>  
</system.identityModel>  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Configuration.IdentityConfiguration>   
 <xref:System.IdentityModel.Configuration.IdentityConfigurationElement>