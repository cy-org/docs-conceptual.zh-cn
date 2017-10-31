---
title: "如何：创建双工联合绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4331d2bc-5455-492a-9189-634a82597726
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：创建双工联合绑定
<xref:System.ServiceModel.WSFederationHttpBinding> 仅支持数据报和请求\/答复消息交换协定。若要使用双工消息交换协定，必须创建自定义绑定。下面的过程演示如何使用 HTTP 和 TCP 传输协议的消息模式安全设置，以及使用 TCP 传输协议的混合模式安全设置，在配置中执行此操作。本主题的结尾是演示所有 3 个绑定的示例代码。  
  
 还可以在代码中创建绑定。有关要创建的绑定元素堆栈的说明，请参见[如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)。  
  
### 使用 HTTP 创建双工联合自定义绑定  
  
1.  在配置文件的 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)[\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) 元素。  
  
2.  在 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) 元素内，创建一个其 `name` 属性设置为 `FederationDuplexHttpMessageSecurityBinding` 的 [\<绑定\>](../../../../docs/framework/misc/binding.md) 元素。  
  
3.  在 [\<绑定\>](../../../../docs/framework/misc/binding.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `SecureConversation` 的 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素。  
  
4.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `IssuedTokenForCertificate` 或 `IssuedTokenForSslNegotiated` 的 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 元素。  
  
5.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<compositeDuplex\>](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md) 元素。  
  
6.  在 [\<compositeDuplex\>](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素。  
  
7.  在 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md) 元素。  
  
### 使用 TCP 消息安全模式创建双工联合自定义绑定  
  
1.  在配置文件的 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素。  
  
2.  在 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素内，创建一个其 `name` 属性设置为 `FederationDuplexTcpMessageSecurityBinding` 的 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素。  
  
3.  在 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `SecureConversation` 的 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素。  
  
4.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `IssuedTokenForCertificate` 或 `IssuedTokenForSslNegotiated` 的 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 元素。  
  
5.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<tcpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 元素。  
  
### 使用 TCP 混合安全模式创建双工联合自定义绑定  
  
1.  在配置文件的 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素。  
  
2.  在 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素内，创建一个其 `name` 属性设置为 `FederationDuplexTcpTransportSecurityWithMessageCredentialBinding` 的 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素。  
  
3.  在 [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `SecureConversation` 的 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素。  
  
4.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 元素内，创建一个其 `authenticationMode` 属性设置为 `IssuedTokenForCertificate` 或 `IssuedTokenForSslNegotiated` 的 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 元素。  
  
5.  在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<sslStreamSecurity\>](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) 元素。  
  
6.  在 [\<sslStreamSecurity\>](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)[\<tcpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 元素。  
  
## 代码示例  
  
#### 包含 3 个绑定的示例  
  
1.  将以下代码插入到配置文件中。  
  
## 示例  
  
```  
  
<bindings>  
   <customBinding>  
      <binding name="FederationDuplexHttpMessageSecurityBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />  
          </security>  
          <compositeDuplex />  
          <oneWay />  
          <httpTransport />  
       </binding>  
<!-- duplex over https is not supported -->  
       <binding name="FederationDuplexTcpMessageSecurityBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />  
          </security>  
          <tcpTransport />  
       </binding>              
       <binding name="FederationDuplexTcpTransportSecurityWithMessageCredentialsBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenOverTransport" />  
          </security>  
<!-- requireClientCertificate = true or <windowsStreamSecurity /> can be used, but does not make sense for most scenarios -->  
          <sslStreamSecurity />  
          <tcpTransport />  
       </binding>              
    </customBinding>  
</bindings>  
  
```