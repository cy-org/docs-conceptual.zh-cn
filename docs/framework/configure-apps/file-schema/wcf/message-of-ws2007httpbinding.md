---
title: "&lt;ws2007HttpBinding&gt; 的 &lt;message&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9ffd8db6-84a8-4b38-a9fe-2cb1a87a1c97
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;ws2007HttpBinding&gt; 的 &lt;message&gt;
定义 [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) 元素的消息级安全性设置。  
  
## 语法  
  
```  
  
<ws2007HttpBinding>  
 <binding >  
  <security>  
   <message clientCredentialType =  
    "None/Windows/UserName/Certificate/IssuedToken"  
    establishSecurityContext="Boolean"  
    negotiateServiceCredential="Boolean"  
    algorithmSuite= Enumeration. See algorithmSuite Attribute below.  
    defaultProtectionLevel="None/Sign/EncryptionAndSign" />  
  </security>  
 </binding>  
</ws2007HttpBinding>  
```  
  
## 类型  
 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp>  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`algorithmSuite`|设置消息加密和密钥包装算法。  算法和密钥大小由 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 类确定。  这些算法映射到安全策略语言 \(WS\-SecurityPolicy\) 规范中指定的算法。<br /><br /> 默认值为 Basic256。|  
|`clientCredentialType`|可选。  指定在使用安全模式 `Message` 或 `TransportWithMessageCredentials` 执行客户端身份验证时要使用的凭据的类型。  请参见下表中的枚举值。  默认值为 Windows。<br /><br /> 此属性的类型为 <xref:System.ServiceModel.MessageCredentialType>。|  
|`establishSecurityContext`|一个确定安全通道是否建立安全会话的值。  安全会话将在交换应用程序消息之前建立安全上下文令牌 \(SCT\)。  建立 SCT 时，此安全通道将提供与上层通道之间的 <xref:System.ServiceModel.Channels.ISession> 接口。  有关使用安全会话的更多信息，请参见[如何：创建安全会话](../../../../../docs/framework/wcf/feature-details/how-to-create-a-secure-session.md)。<br /><br /> 默认值为 `true`。|  
|`negotiateServiceCredential`|可选。  一个值，指定是在带外客户端提供服务凭据，还是通过协商过程从服务向客户端获取服务凭据。  这种协商是正常消息交换的前提。<br /><br /> 如果 `clientCredentialType` 特性等于 None、Username 或 Certificate，那么将此特性设置为 `false` 意味着可以在带外客户端使用服务证书，并且客户端必须在 [\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)服务行为中指定服务证书（使用 [\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)）。  此模式可与实现 WS\-Trust 和 WS\-SecureConversation 的 SOAP 堆栈交互操作。<br /><br /> 如果 `ClientCredentialType` 属性设置为 `Windows`，则将此属性设置为 `false` 会指定基于 Kerberos 的身份验证。  这意味着客户端和服务必须是相同 Kerberos 域的一部分。  此模式可与实现 Kerberos 令牌配置文件（如 OASIS WSS TC 中所定义）以及 WS\-Trust 和 WS\-SecureConversation 的 SOAP 堆栈交互操作。<br /><br /> 当此属性为 `true` 时，将导致 .NET SOAP 协商，从而通过 SOAP 消息进行 <xref:System.ServiceModel.Security.Tokens.ServiceModelSecurityTokenTypes.Spnego%2A> 交换隧道处理。<br /><br /> 默认值为 `true`。|  
  
## algorithmSuite 属性  
  
|值|描述|  
|-------|--------|  
|Basic128|使用 Aes128 加密，对消息摘要使用 Sha1，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic192|使用 Aes192 加密，对消息摘要使用 Sha1，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic256|使用 Aes256 加密，对消息摘要使用 Sha1，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic256Rsa15|对消息加密使用 Aes256，对消息摘要使用 Sha1，对密钥包装使用 Rsa15。|  
|Basic192Rsa15|对消息加密使用 Aes192，对消息摘要使用 Sha1，对密钥包装使用 Rsa15。|  
|TripleDes|使用 TripleDes 加密，对消息摘要使用 Sha1，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic128Rsa15|对消息加密使用 Aes128，对消息摘要使用 Sha1，对密钥包装使用 Rsa15。|  
|TripleDesRsa15|使用 TripleDes 加密，对消息摘要使用 Sha1，对密钥包装使用 Rsa15。|  
|Basic128Sha256|对消息加密使用 Aes256，对消息摘要使用 Sha256，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic192Sha256|对消息加密使用 Aes192，对消息摘要使用 Sha256，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic256Sha256|对消息加密使用 Aes256，对消息摘要使用 Sha256，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|TripleDesSha256|对消息加密使用 TripleDes，对消息摘要使用 Sha256，对密钥包装使用 Rsa\-oaep\-mgf1p。|  
|Basic128Sha256Rsa15|对消息加密使用 Aes128，对消息摘要使用 Sha256，对密钥包装使用 Rsa15。|  
|Basic192Sha256Rsa15|对消息加密使用 Aes192，对消息摘要使用 Sha256，对密钥包装使用 Rsa15。|  
|Basic256Sha256Rsa15|对消息加密使用 Aes256，对消息摘要使用 Sha256，对密钥包装使用 Rsa15。|  
|TripleDesSha256Rsa15|对消息加密使用 TripleDes，对消息摘要使用 Sha256，对密钥包装使用 Rsa15。|  
  
## clientCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|`None`|允许服务与匿名客户端交互。  对于服务，这表示服务不需要任何客户端凭据。  对于客户端，这表示客户端不提供任何客户端凭据。|  
|`Certificate`|允许服务要求使用证书对客户端进行身份验证。  如果使用 `message` 安全模式并且将 `negotiateServiceCredential` 属性设置为 `false`，则必须向客户端提供服务证书。|  
|`IssuedToken`|指定自定义令牌，该令牌通常由安全令牌服务 \(STS\) 颁发。|  
|`UserName`|允许服务要求使用 `UserName` 凭据对客户端进行身份验证。  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 不支持发送密码摘要，也不支持使用密码派生密钥并使用这样的密钥来提供消息安全性。  因此，在使用 `UserName` 凭据时，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 将确保传输的安全性。  这种凭据模式将产生可互操作的交换或不可互操作的协商，具体取决于 `negotiateServiceCredential` 属性。|  
|`Windows`|允许 SOAP 交换在已通过身份验证的 `Windows` 凭据上下文中执行。  如果 `negotiateServiceCredential` 属性设置为 `true`，则将执行 SSPI 协商或 Kerberos（一种可互操作的标准）。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-ws2007httpbinding.md)|定义 [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)的安全设置。|  
  
## 请参阅  
 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Message%2A>   
 <xref:System.ServiceModel.WSHttpSecurity.Message%2A>   
 <xref:System.ServiceModel.Configuration.NonDualMessageSecurityOverHttpElement>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)