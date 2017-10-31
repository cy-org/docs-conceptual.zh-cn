---
title: "&lt;securityTokenHandlerConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 28724cc6-020c-4a06-9a1f-d7594f315019
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;securityTokenHandlerConfiguration&gt;
提供了配置标记处理程序的集合。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration saveBootstrapContext=xs:boolean  
          maximumClockSkew=TimeSpan>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|saveBootstrapContext|指定是否应包含引导标记的会话令牌中。  该值还通过设置设置标记处理程序集合上`saveBootstrapContext`属性上[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素。  上的标记处理程序集合值将替代该服务上设置的值。|  
|maximumClockSkew|A <xref:System.TimeSpan> ，它指定允许的最大时钟不一致。  执行时间敏感型业务，如验证登录会话的到期时间时，可以控制允许的最大时钟不一致。  默认为 5 分钟，"00: 05: 00"。  有关如何指定<xref:System.TimeSpan>的值，请参阅[Timespan Values](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_TimespanValues)。  也可以在服务级别通过设置来设置最大时钟倾斜`maximumClockSkew`属性上[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素。  上的标记处理程序集合值将替代该服务上设置的值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<audienceUris\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/audienceuris.md)|指定的 Uri 的都是可接受的标识符，该依赖方的组。  可选。|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|注册用于会话令牌和令牌重做检测的缓存。  可指定服务级别或安全令牌的处理程序集。  可选。|  
|[\<certificateValidation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidation.md)|控制用于验证证书的标记处理程序的设置。  可指定服务级别或安全令牌的处理程序集。  如果特定处理程序配置为使用其自己的验证程序重写这些设置。  可选。|  
|[\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)|配置颁发者名称注册表所使用的标记处理程序集合中的处理程序。  可选。|  
|[\<issuerTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuertokenresolver.md)|注册颁发令牌解析所使用的标记处理程序集合中的处理程序。  颁发者令牌解析用于解析上传入令牌和邮件的签名标记。  可选。|  
|[\<serviceTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicetokenresolver.md)|注册服务令牌解析所使用的标记处理程序集合中的处理程序。  令牌解析服务用于解析传入令牌和邮件加密标记。  可选。|  
|[\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md)|启用标记重做检测并指定标记的过期时间。  可指定服务级别或安全令牌的处理程序集。  可选。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|指定的安全令牌的处理程序中注册该终结点的集合。|  
  
## 备注  
 本部分提供的属性值<xref:System.IdentityModel.Tokens.SecurityTokenHandlerConfiguration>对象。  本节中的设置重写该服务上配置的。  其中的某些设置，可以通过安全标记处理程序集合添加一个处理程序时指定的设置覆盖。  
  
## 示例  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>   
      <securityTokenHandlerConfiguration>  
  
        <audienceUris>  
          <clear/>  
          <add value="http://www.example.com/myapp/" />  
        </audienceUris>  
  
        <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel">  
          <trustedIssuers>  
            <add thumbprint="97249e1a … 4c9158de" name="contoso.com" />  
          </trustedIssuers>  
        </issuerNameRegistry>  
  
        <issuerTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
        <serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```