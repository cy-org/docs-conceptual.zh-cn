---
title: "&lt;authorizationPolicies&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 613a03d8-4384-4556-bce2-8c23286c0bb0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;authorizationPolicies&gt; 的 &lt;add&gt;
指定声明转换的授权策略。  
  
## 语法  
  
```  
  
<authorizationPolicies>  
   <add policyType="String" />  
</authorizationPolicies>  
```  
  
## 类型  
 `Type`  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`policyType`|必需的字符串属性。<br /><br /> [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 访问控制模型支持以类型的形式提供一组授权策略。  此属性指定一个授权策略，使得可以将一组输入声明转换为另一组声明。  可以根据该授权策略来授予或拒绝访问控制。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<authorizationPolicies\>](../../../../../docs/framework/configure-apps/file-schema/wcf/authorizationpolicies.md)|指定一个授权策略类型集合。|  
  
## 备注  
 每个授权类型都包含一个所需的 `policyType` 属性，此属性是一个字符串。  该属性指定一个授权策略，可以将一组输入声明转换为另一组声明。  可以根据该授权策略来授予或拒绝访问控制。  有关身份验证策略的工作方式的更多信息，请参见 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 和[授权策略](../../../../../docs/framework/wcf/samples/authorization-policy.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>   
 <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElement>   
 <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement.AuthorizationPolicies%2A>   
 <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElementCollection>   
 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>   
 [授予对服务操作的访问权限](../../../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)   
 [如何：为服务创建自定义授权管理器](../../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)   
 [\<add\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-authorizationpolicies.md)   
 [授权策略](../../../../../docs/framework/wcf/samples/authorization-policy.md)