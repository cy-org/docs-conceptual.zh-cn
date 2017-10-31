---
title: "SecurityBindingElement 身份验证模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 12300bf4-c730-4405-9f65-d286f68b5a43
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# SecurityBindingElement 身份验证模式
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供了几种供客户端和服务互相进行身份验证的模式。您可以通过使用 <xref:System.ServiceModel.Channels.SecurityBindingElement> 类上的静态方法或通过配置为这些身份验证模式创建安全绑定元素。本主题简要说明 18 种身份验证模式。  
  
 有关对一种身份验证模式使用该元素的示例，请参见[如何：为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)。  
  
## 基本配置编程  
 下面的过程说明如何在配置文件中设置身份验证模式。  
  
#### 在配置中设置身份验证模式  
  
1.  向 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素中添加一个 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
2.  将一个 [\<绑定\>](../../../../docs/framework/misc/binding.md) 元素作为子元素添加到 `<customBinding>` 元素中。  
  
3.  向 `<binding>` 元素中添加一个 `<security>` 元素。  
  
4.  将 `authenticationMode` 属性设置为下述值之一。例如，下面的代码将模式设置为 `AnonymousForCertificate`。  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="SecureCustomBinding">  
         <security authenticationMode ="AnonymousForCertificate" />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
#### 以编程方式设置模式  
  
1.  确定返回类型，可以是以下类型之一：<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>、<xref:System.ServiceModel.Channels.TransportSecurityBindingElement>、<xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 或 <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
2.  调用 <xref:System.ServiceModel.Channels.SecurityBindingElement> 类的适当静态方法。例如，下面的代码调用 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateAnonymousForCertificateBindingElement%2A> 方法。  
  
     [!code-csharp[c_CustomBindingsAuthMode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombindingsauthmode/cs/source.cs#3)]
     [!code-vb[c_CustomBindingsAuthMode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombindingsauthmode/vb/source.vb#3)]  
  
3.  使用绑定元素创建自定义绑定。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## 模式说明  
  
### AnonymousForCertificate  
 在此身份验证模式中，客户端是匿名的，因此使用 X.509 证书对服务进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateAnonymousForCertificateBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。或者，将 \<`security`\> 元素的 `authenticationMode` 属性设置为 `AnonymousForCertificate`。  
  
### AnonymousForSslNegotiated  
 在此身份验证模式中，客户端是匿名的，因此使用在运行时进行协商的 X.509 证书对服务进行身份验证。安全绑定元素是在为第一个参数传递 `false` 值时由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSslNegotiationBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。或者，将 `authenticationMode` 属性设置为 `AnonymousForSslNegotiated`。  
  
### CertificateOverTransport  
 在此身份验证模式中，客户端使用 X.509 证书进行身份验证，此证书作为认可的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。在传输层，服务是用 X.509 证书进行身份验证的。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateCertificateOverTransportBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>。或者，将 `authenticationMode` 属性设置为 `CertificateOverTransport`。  
  
### IssuedToken  
 在此身份验证模式中，客户端不向服务进行身份验证，而是向安全令牌服务进行身份验证并接收一个 SAML 令牌，然后将其提供给服务器，以证明它知道共享密钥。服务也不向客户端进行身份验证，但安全令牌服务会将共享密钥作为已颁发令牌的一部分进行加密，因此只有服务才能解密该密钥。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。或者，将 `authenticationMode` 属性设置为 `IssuedToken`。  
  
### IssuedTokenForCertificate  
 在此身份验证模式中，客户端不向服务进行身份验证，而是向安全令牌服务进行身份验证并接收一个 SAML 令牌，然后将其提供给服务器，以证明它知道共享密钥。颁发的令牌作为认可的支持令牌或持有者令牌（即签署消息签名的令牌）显示在 SOAP 层上。服务使用 X.509 证书对客户端进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。或者，将 `authenticationMode` 属性设置为 `IssuedTokenForCertificate`。  
  
### IssuedTokenForSslNegotiated  
 在此身份验证模式中，客户端不向服务进行身份验证，而是向安全令牌服务进行身份验证并接收一个 SAML 令牌，然后将其提供给服务器，以证明它知道共享密钥。颁发的令牌作为认可的支持令牌或持有者令牌（即签署消息签名的令牌）显示在 SOAP 层上。使用 X.509 证书对服务进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A> 方法返回的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。或者，将 `authenticationMode` 属性设置为 `IssuedTokenForSslnegotiated`。  
  
### IssuedTokenOverTransport  
 在此身份验证模式中，客户端不向服务进行身份验证，而是向安全令牌服务进行身份验证并接收一个 SAML 令牌，然后将其提供给服务器，以证明它知道共享密钥。颁发的令牌作为认可的支持令牌或持有者令牌（即签署消息签名的令牌）显示在 SOAP 层上。在传输层，服务是用 X.509 证书进行身份验证的。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A> 方法返回的 `TransportSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `IssuedTokenOverTransport`。  
  
### Kerberos  
 在此身份验证模式下，客户端使用 Kerberos 票证向服务进行身份验证。该票证还提供服务器身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `Kerberos`。  
  
> [!NOTE]
>  若要使用此身份验证模式，服务帐户必须与服务主体名称 \(SPN\) 关联。为此，请在 NETWORK SERVICE 帐户或 LOCAL SYSTEM 帐户下运行服务。也可以使用 SetSpn.exe 工具为服务帐户创建一个 SPN。不论何种情况，客户端都必须使用 [\<servicePrincipalName\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) 元素中的正确 SPN，或者通过使用 <xref:System.ServiceModel.EndpointAddress> 构造函数来应用正确的 SPN。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
> [!NOTE]
>  当使用 `Kerberos` 身份验证模式时，不支持 <xref:System.Security.Principal.TokenImpersonationLevel> 和 <xref:System.Security.Principal.TokenImpersonationLevel> 模拟级别。  
  
### KerberosOverTransport  
 在此身份验证模式下，客户端使用 Kerberos 票证向服务进行身份验证。Kerberos 令牌作为认可的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。在传输层，服务是用 X.509 证书进行身份验证的。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosOverTransportBindingElement%2A> 方法返回的 `TransportSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `KerberosOverTransport`。  
  
> [!NOTE]
>  若要使用此身份验证模式，服务帐户必须与 SPN 关联。为此，请在 NETWORK SERVICE 帐户或 LOCAL SYSTEM 帐户下运行服务。也可以使用 SetSpn.exe 工具为服务帐户创建一个 SPN。不论何种情况，客户端都必须使用 [\<servicePrincipalName\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) 元素中的正确 SPN，或者通过使用 <xref:System.ServiceModel.EndpointAddress> 构造函数来应用正确的 SPN。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
### MutualCertificate  
 在此身份验证模式中，客户端使用 X.509 证书进行身份验证，此证书作为认可的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。同样使用 X.509 证书对服务进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `MutualCertificate`。  
  
### MutualCertificateDuplex  
 在此身份验证模式中，客户端使用 X.509 证书进行身份验证，此证书作为认可的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。同样使用 X.509 证书对服务进行身份验证。此绑定是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateDuplexBindingElement%2A> 方法返回的 `AsymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `MutualCertificateDuplex`。  
  
### MutalSslNegotiation  
 在此身份验证模式中，客户端和服务都使用 X.509 证书进行身份验证。安全绑定元素是在为第一个参数传递 `true` 值时由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSslNegotiationBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `MutualSslNegotiated`。  
  
### SecureConversation  
 安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。此方法将 <xref:System.ServiceModel.Channels.SecurityBindingElement> 作为一个参数，在初始化过程中使用该参数建立安全会话。或者，将 `authenticationMode` 属性设置为 `SecureConversation`。  
  
 如果未指定启动绑定，则会对启动使用 `SspiNegotiated` 身份验证模式。  
  
### SspiNegotiation  
 在此身份验证模式中，使用协商协议来执行客户端和服务器身份验证。可能时使用 Kerberos；否则使用 NT LanMan \(NTLM\)。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `SspiNegotiated`。  
  
### SspiNegotiatedOverTransport  
 在此身份验证模式中，使用协商协议来执行客户端和服务器身份验证。可能时使用 Kerberos 协议；否则使用 NTLM。生成的令牌作为认可的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。在传输层，服务还是由 X.509 证书另外进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationOverTransportBindingElement%2A> 方法返回的 `TransportSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `SspiNegotiatedOverTransport`。  
  
### UserNameForCertificate  
 在此身份验证模式中，客户端使用用户名令牌向服务进行身份验证，此证书作为经过签名的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。服务使用 X.509 证书对客户端进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForCertificateBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `UserNameForCertificate`。  
  
 对于 `UserNameForCertificate` 身份验证模式，客户端和服务都必须使用 WS\-Security 1.1。  
  
### UserNameForSslNegotiated  
 在此身份验证模式中，客户端使用用户名令牌进行身份验证，此证书作为经过签名的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。使用 X.509 证书对服务进行身份验证。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForSslBindingElement%2A> 方法返回的 `SymmetricSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `UserNameForSslNegotiated`。  
  
### UserNameOverTransport  
 在此身份验证模式中，客户端使用用户名令牌进行身份验证，此证书作为经过签名的支持令牌（即签署消息签名的令牌）显示在 SOAP 层上。在传输层，服务是用 X.509 证书进行身份验证的。安全绑定元素是由 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameOverTransportBindingElement%2A> 方法返回的 `TransportSecurityBindingElement`。或者，将 `authenticationMode` 属性设置为 `UserNameOverTransport`。  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>   
 [如何：为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)