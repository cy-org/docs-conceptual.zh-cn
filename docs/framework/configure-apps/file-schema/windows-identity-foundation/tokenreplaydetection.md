---
title: "&lt;tokenReplayDetection&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac3f588e-5f75-4275-b969-2d492ecc3b47
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;tokenReplayDetection&gt;
启用标记重播检测并指定标记的到期时间。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <tokenReplayDetection enabled=xs:boolean expirationPeriod=TimeSpan>  
    </tokenReplayDetection>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 类型  
 <xref:System.IdentityModel.Configuration.TokenReplayDetectionElement>  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|启用|指定的值标记重播检测是否启用;“true”启用标记重播检测。|  
|expirationPeriod|<xref:System.TimeSpan> 中的项之前指定最大时间被视为从缓存过期并将其移除。  有关如何指定 <xref:System.TimeSpan> 值的更多信息，请 [Timespan Values](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_TimespanValues)参见。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定服务级别的标识设置。|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|出于安全标记处理程序的集合提供配置。|  
  
## 备注  
 `<tokenReplayDetection>` 元素既可以在服务级别在 `<identityConfiguration>` 元素下或在 `<securityTokenHandlerConfiguration>` 元素下的安全标记处理程序集合级别。  在服务重写这些指定的标记处理程序集合的设置。  
  
 标记重播缓存的类型由元素中指定 [\<tokenReplayCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md) 。