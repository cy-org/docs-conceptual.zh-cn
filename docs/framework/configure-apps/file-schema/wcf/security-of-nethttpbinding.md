---
title: "&lt;netHttpBinding 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc41f6f7-cabc-4a64-9fa0-ceabf861b348
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;netHttpBinding 的 &lt;security&gt;
定义 [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)的安全功能。  
  
## 语法  
  
```  
  
<security mode="Message/None/Transport/TransportWithCredential">  
   <transport  
      clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
      proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
      realm="string" />  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />  
</security>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|可选。  指定所使用的安全类型。  默认值为 `None`。  此属性的类型为 <xref:System.ServiceModel.NetHttpSecurityMode>。|  
  
## mode 属性  
  
|值|描述|  
|-------|--------|  
|无|-   在传输过程中不能保证消息的安全。|  
|传输|使用 HTTPS 传输提供安全性。  用 HTTPS 保证 SOAP 消息的安全。  使用服务的 X.509 证书向客户端对服务进行身份验证。  使用所提供的 ClientCredentialType 对客户端进行身份验证。|  
|消息|使用 SOAP 消息安全提供安全性。  默认情况下，将对正文进行加密和签名。  对于此绑定，系统要求向带外客户端提供服务器证书。  此绑定仅有的有效 `ClientCredentialType` 为 `Certificate`。|  
|TransportWithMessageCredential|完整性、保密性和服务器身份验证由传输安全来提供。  客户端身份验证采用 SOAP 消息安全方式提供。  如果要使用用户名\/密码对用户进行身份验证，并且存在用于保护消息传输的现有 HTTP 部署，则适用此模式。|  
|TransportCredentialOnly|此模式并不提供消息的完整性和保密性，  而是提供基于 http 的客户端身份验证。  使用此模式时应当小心。  在通过其他方式（如 IPSec）提供传输安全并且 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 基础结构只提供客户端身份验证的环境中，应该使用此模式。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nethttpbinding.md)|定义基本 HTTP 服务的传输安全设置。  此元素与 <xref:System.ServiceModel.HttpTransportSecurity> 相对应。|  
|[\<消息\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-nethttpbinding.md)|定义基本 HTTP 服务的消息安全设置。  此元素与 <xref:System.ServiceModel.NetHttpMessageSecurity> 相对应。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|绑定|[\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)的绑定元素。|  
  
## 备注  
 默认情况下，不会对 SOAP 消息进行保护，也不会对客户端进行身份验证。  使用此元素，您可以配置 `netHttpBinding` 元素的其他安全设置。  
  
## 请参阅  
 <xref:System.ServiceModel.NetHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetHttpSecurityElement>   
 <xref:System.ServiceModel.NetHttpSecurity>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [选择凭据类型](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)