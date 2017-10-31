---
title: "&lt;netMsmqBinding&gt; 的 &lt;message&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ebf0240-d7be-4493-b0fe-f00fd5989d77
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;netMsmqBinding&gt; 的 &lt;message&gt;
在此 `netMsmqBinding` 绑定上定义 SOAP 消息安全设置。  
  
## 语法  
  
```  
  
<netMsmqBinding>  
    <binding>  
      <security>  
         <message   
                      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            clientCredentialType="None/Windows/UserName/Certificate/CardSpace" />  
    </security>  
</netMsmqBinding>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|algorithmSuite|设置消息加密和密钥包装算法，这些算法用于针对通过 MSMQ 传输发送的消息实现基于消息的安全性。<br /><br /> 默认值为 `Aes256`。  此属性的类型为 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>。|  
|clientCredentialType|指定针对通过 MSMQ 传输发送的消息执行客户端身份验证时要使用的凭据类型。  包括以下有效值：<br /><br /> -   None：允许服务与匿名客户端交互。  服务和客户端都不需要凭据。<br />-   Windows：使 SOAP 交换可以在已通过身份验证的 Windows 凭据上下文中进行。  此设置总是执行基于 Kerberos 的身份验证。<br />-   UserName：使服务可以要求使用 UserName 凭据对客户端进行身份验证。  在此情况下，需要使用 `clientCredentials` 行为来指定凭据。 **Caution:**  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 不支持发送密码摘要，也不支持使用密码派生密钥并使用这样的密钥来提供消息安全性。  因此，在使用 UserName 凭据时，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 将确保交换的安全性。  此模式要求使用 `clientCredential` 行为和 `serviceCertificate` 在客户端指定服务证书。 <br /><br /> -   Certificate：使服务可以要求使用证书对客户端进行身份验证。  在此情况下，需要使用 `clientCredentials` 行为指定客户端凭据。  在此情况下，需要使用 `clientCredentials` 行为，通过指定 `serviceCertificate` 来指定服务凭据。<br />-   CardSpace：允许服务要求使用 CardSpace 对客户端进行身份验证。  必须在 `clientCredential` 行为中设置 `serviceCertiifcate`。<br /><br /> 默认值为 `Windows`。  此属性的类型为 <xref:System.ServiceModel.MessageCredentialType>。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netmsmqbinding.md)|定义绑定的安全设置。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.MessageSecurityOverMsmqElement>   
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Message%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity.Message%2A>   
 <xref:System.ServiceModel.MessageSecurityOverMsmq>   
 [WCF 中的队列](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)