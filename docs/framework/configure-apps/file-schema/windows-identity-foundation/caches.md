---
title: "&lt;caches&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4651091b-3a20-40d8-b293-4408c0710143
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;caches&gt;
注册用于会话令牌和令牌重做检测的缓存。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<sessionSecurityTokenCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md)|注册为会话令牌缓存服务或安全令牌的处理程序集合。|  
|[\<tokenReplayCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md)|注册标记重播缓存服务或安全令牌的处理程序集合。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定的服务级别标识设置。|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌的处理程序。|  
  
## 备注  
 A `<caches>`元素都可以在服务级别下指定`<identityConfiguration>`元素或在安全标记处理程序集级别上`<securityTokenHandlerConfiguration>`元素。  标记处理程序集合上的设置会覆盖那些指定的服务。  
  
 `<caches>`元素都由<xref:System.IdentityModel.Configuration.IdentityModelCachesElement>类。  配置的缓存由<xref:System.IdentityModel.Configuration.IdentityModelCaches>类。  
  
## 示例  
 下面的 XML 显示用于保存安全令牌的会话的自定义缓存的配置 \(<xref:System.IdentityModel.Tokens.SessionSecurityToken>\)。  配置取自`ClaimsAwareWebFarm`的示例。  
  
```  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```