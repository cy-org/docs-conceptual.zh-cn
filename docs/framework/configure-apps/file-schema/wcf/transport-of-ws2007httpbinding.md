---
title: "&lt;ws2007HttpBinding&gt; 的 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 692befa3-8b0b-4ec5-b601-755874e98eb0
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;ws2007HttpBinding&gt; 的 &lt;transport&gt;
定义 HTTP 传输的身份验证设置。  
  
## 语法  
  
```  
  
transport clientCredentialType =   
       "Basic/Certificate/Digest/None/Ntlm/Windows"  
       proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
       realm="string"   
```  
  
## 类型  
 <xref:System.ServiceModel.HttpTransportSecurity>  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`clientCredentialType`|指定用于向服务证明客户端身份的凭据。  此属性的类型为 <xref:System.ServiceModel.HttpClientCredentialType>。|  
|`proxyCredentialType`|指定用于向域代理证明客户端身份的凭据。  此属性的类型为 <xref:System.ServiceModel.HttpProxyCredentialType>。|  
|`realm`|摘要式或基本身份验证的身份验证领域。  默认值为一个空字符串。<br /><br /> 身份验证领域至少指定执行身份验证的主机的名称。  它还可以指定具有访问权限的用户集合。  用户可以查询身份验证领域，以确定多个可能的用户名和密码中哪一个可以使用。|  
  
## clientCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|无|禁用安全性。|  
|Basic|使用基本身份验证。|  
|摘要|使用摘要式身份验证。|  
|Ntlm|对 Windows 域使用 NTLM 身份验证作为回退。|  
|Windows|使用集成 Windows 身份验证。|  
|证书|使用 X.509 证书对客户端进行身份验证。|  
  
## proxyCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|无|禁用安全性。|  
|Basic|使用基本身份验证。|  
|摘要|使用摘要式身份验证。|  
|Ntlm|对 Windows 域使用 NTLM 作为回退。|  
|Windows|使用集成 Windows 身份验证。|  
|证书|使用 X.509 证书对客户端进行身份验证。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-ws2007httpbinding.md)|表示 [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) 元素的安全功能。|  
  
## 请参阅  
 <xref:System.ServiceModel.HttpTransportSecurity>   
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpTransportSecurityElement>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)