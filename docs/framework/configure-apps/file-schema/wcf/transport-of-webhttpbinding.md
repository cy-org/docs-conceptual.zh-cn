---
title: "&lt;webHttpBinding&gt; 的 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f150fb19-7de1-44af-81f4-86cad881cd05
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;webHttpBinding&gt; 的 &lt;transport&gt;
定义配置为接收 HTTP 请求的服务终结点的传输级安全设置。  
  
## 语法  
  
```  
<webHttpBinding>  
    <binding>  
        <security  
        mode="None|Transport|Message|TransportWithMessageCredential|TransportCredentialOnly">  
            <transport clientCredentialType="None|Basic|Digest|Ntlm|Windows"  
             proxyCredentialType="None|Basic|Digest|Ntlm|Windows" realm="string" >  
                <extendedProtectionPolicy  
                     policyEnforcement="Never|WhenSupported|Always"  
                     protectionScenario="TransportSelected|TrustedProxy">  
                    <customServiceNames></customServiceNames>  
                        </extendedProtectionPolicy>  
            </transport>  
        </security>  
    </binding>  
</WebHttpBinding>  
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
|`realm`|一个字符串，指定摘要式或基本身份验证的身份验证领域。  默认值为一个空字符串。<br /><br /> 身份验证领域至少指定执行身份验证的主机的名称。  它还可以指定具有访问权限的用户的集合。  用户可以查询身份验证领域，以确定多个可能的用户名和密码中哪一个可以使用。|  
|`policyEnforcement`|此枚举指定应何时强制实施 <xref:System.Security.Authentication.ExtendedProtectionPolicy>。<br /><br /> 1.  Never – 绝不强制实施此策略（禁用扩展保护）。<br />2.  WhenSupported – 仅在客户端支持扩展保护时才强制实施此策略。<br />3.  Always – 总是强制实施此策略。  不支持扩展保护的客户端将无法进行身份验证。|  
  
## clientCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|`None`|禁用安全性。|  
|`Basic`|使用基本身份验证。|  
|`Certificate`|使用 X.509 证书对客户端进行身份验证。|  
|`Digest`|使用摘要式身份验证。|  
|`Ntlm`|对 Windows 域使用 NTLM 身份验证作为回退。|  
|`Windows`|使用集成 Windows 身份验证。|  
  
## proxyCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|`None`|禁用安全性。|  
|`Basic`|使用基本身份验证。|  
|`Digest`|使用摘要式身份验证。|  
|`Ntlm`|对 Windows 域使用 NTLM 作为回退。|  
|`Windows`|使用集成 Windows 身份验证。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-webhttpbinding.md)|表示 [\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 元素的安全功能。|  
  
## 请参阅  
 <xref:System.ServiceModel.HttpTransportSecurity>   
 <xref:System.ServiceModel.Configuration.WebHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.WebHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)   
 [WCF Web HTTP 编程模型](../../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)