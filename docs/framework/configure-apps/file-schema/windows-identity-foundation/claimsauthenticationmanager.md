---
title: "&lt;claimsAuthenticationManager&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d30a450-6d13-4671-81a8-77e0204500c5
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;claimsAuthenticationManager&gt;
注册传入的声明的声明身份验证管理器。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthenticationManager type=xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthenticationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|类型|指定从 <xref:System.Security.Claims.ClaimsAuthenticationManager> 类派生的自定义类型。  有关如何指定 `type` 属性的更多信息，请 [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferencess)参见。|  
  
### 子元素  
 如果没有 `type` 属性，或者，如果 `type` 属性引用 <xref:System.Security.Claims.ClaimsAuthenticationManager> 类， `<claimsAuthenticationManager>` 元素不采用子元素;但是，从 <xref:System.Security.Claims.ClaimsAuthenticationManager> 派生的类可以定义子配置元素。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定服务级别的标识设置。|  
  
## 备注  
 通过 <xref:System.Security.Claims.ClaimsAuthenticationManager> 类提供的默认行为回显传入的声明。  如果 `type` 未指定属性，或者 `type` 属性指定 <xref:System.Security.Claims.ClaimsAuthenticationManager> 类， `<claimsAuthenticationManager>` 元素不采用子元素。  可以指定 `type` 特性添加到类型 <xref:System.Security.Claims.ClaimsAuthenticationManager> 从类派生来实现自定义行为的注册。  派生类可以通过 `<claimsAuthenticationManager>` 元素的子元素支持配置通过重写 <xref:System.Security.Claims.ClaimsAuthenticationManager.LoadCustomConfiguration%2A> 方法处理这些元素。  为子元素定义的模式由类的设计器。  
  
 `<claimsAuthenticationManager>` 元素将设置 <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthenticationManager%2A?displayProperty=fullName> 属性。  
  
## 示例  
  
```  
<system.identityModel>  
    <identityConfiguration name=”MyIdentity”>  
      <claimsAuthenticationManager type="MyNamespace.CustomClaimsAuthenticationManager, MyAssembly"/>          
    </identityConfiguration>  
</microsoft.identityModel>  
```