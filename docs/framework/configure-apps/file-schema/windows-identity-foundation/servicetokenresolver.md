---
title: "&lt;serviceTokenResolver&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;serviceTokenResolver&gt;
注册服务令牌解析所使用的标记处理程序集合中的处理程序。  令牌解析服务用于解析传入令牌和邮件加密标记。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
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
|type|指定服务的令牌解析的类型。  任何一个<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类型或类型派生自的<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类。  有关如何指定`type`属性，请参阅[Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences)。  必选。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌的处理程序。|  
  
## 备注  
 令牌解析服务可用于解决上传入令牌和邮件加密标记。  它用于检索此密钥用于解密传入令牌。  您必须指定`type`属性。  指定的类型可以是<xref:System.IdentityModel.Selectors.SecurityTokenResolver>或自定义类型派生自的<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类。  
  
 某些标记处理程序允许您在配置中指定服务的令牌解析程序设置。  在单个标记处理程序的设置会覆盖指定的安全令牌的处理程序集合。  
  
> [!NOTE]
>  指定`<serviceTokenResolver>`元素的子元素作为[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被否决，但仍然支持向后兼容性。  在设置`<securityTokenHandlerConfiguration>`元素会覆盖那些在`<identityConfiguration>`元素。  
  
## 示例  
  
```  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```