---
title: "&lt;webHttpBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 727cf3d2-6f56-48ad-a59f-ba423edb9c83
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# &lt;webHttpBinding&gt; 的 &lt;security&gt;
指定对用 [\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)配置的终结点的安全要求。  
  
## 语法  
  
```  
  
<system.ServiceModel>  
    <bindings>  
        <webHttpBinding>  
            <binding name = "string">  
              <security mode="None/Transport/TransportCredentialOnly">  
                                    <transport clientCredentialType =   
                                     "Basic/Certificate/Digest/None/Ntlm/Windows"  
                                     proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
                                     realm="string" />  
              </security>  
        </webHttpBinding>  
    </bindings>  
</system.ServiceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|指定终结点是使用传输级安全模式还是不使用安全模式。  默认值为 `None`。  此属性的类型为 <xref:System.ServiceModel.WebHttpSecurityMode>。|  
  
## Mode 属性  
  
|值|描述|  
|-------|--------|  
|无|禁用安全性。|  
|传输|使用 HTTPS 提供安全性。  此服务需要使用 SSL 证书进行配置。  消息使用 HTTPS 获得全面保护，而且客户端使用服务的 SSL 证书对服务进行身份验证。  客户端身份验证是通过 [\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-webhttpbinding.md) 的 `ClientCredentialType` 属性控制的。|  
|TransportCredentialOnly|此模式并不提供消息的完整性和保密性，  而是提供基于 HTTP 的客户端身份验证。  使用此模式时应当小心。  在通过其他方式（如 IPSec）提供传输安全并且 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 基础结构只提供客户端身份验证的环境中，应该使用此模式。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-webhttpbinding.md)|定义传输安全设置。  此元素与 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> 类型相对应。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md)|一个绑定元素，可用于为响应 HTTP 请求（而不是 SOAP 消息）的 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] Web 服务配置终结点。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.WebHttpBindingElement>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>   
 <xref:System.ServiceModel.WebHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WebHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.WebHttpSecurity>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [选择凭据类型](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)   
 [WCF Web HTTP 编程模型](../../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)