---
title: "将 WSE 3.0 Web 服务迁移到 WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7bc5fff7-a2b2-4dbc-86cc-ecf73653dcdc
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 将 WSE 3.0 Web 服务迁移到 WCF
将 WSE 3.0 Web 服务迁移到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的好处包括：提高性能，支持其他传输协议、其他安全方案和 WS-* 规范。 在从 WSE 3.0 迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 之后，Web 服务的性能最多可以提高 200% 到 400%。 有关支持的传输[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅[选择传输方式](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)。 有关支持的方案的列表[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅[常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)。 有关支持的规范的列表[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅[Web 服务协议互操作性指南](../../../../docs/framework/wcf/feature-details/web-services-protocols-interoperability-guide.md)。  
  
 以下几节提供了有关如何将 WSE 3.0 Web 服务的特定功能迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的指导。  
  
## <a name="general"></a>常规  
 WSE 3.0 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序领域包括网络级互操作和一组常用术语。 WSE 3.0 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以基于二者均支持的 WS-* 规范集进行网络级互操作。 在开发 WSE 3.0 或 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序时，需要使用一组常用的术语，例如，WSE 中的关守安全断言的名称以及身份验证模式的名称。  
  
 尽管 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 ASP.NET 或 WSE 3.0 编程模型之间存在许多相似方面，但它们仍然是不同的。 有关详细信息[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]编程模型，请参见[基本编程生命周期](../../../../docs/framework/wcf/basic-programming-lifecycle.md)。  
  
> [!NOTE]
>  将 WSE Web 服务迁移到 WCF [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)工具可以用于生成客户端。 另一方面，该客户端还包含可以用作 WCF 服务起点的接口和类。 所生成的接口具有<xref:System.ServiceModel.OperationContractAttribute>应用到的协定的成员属性<xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A>属性设置为`*`。 当 WSE 客户端调用 Web 服务时使用此设置时，将引发以下异常︰ **Web.Services3.ResponseProcessingException: WSE910︰ 响应消息，在处理过程中发生错误，您可以在内部异常中查找错误**。 若要缓解此问题，将设置<xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A>属性<xref:System.ServiceModel.OperationContractAttribute>属性设为非`null`值，例如`http://Microsoft.WCF.Documentation/ResponseToOCAMethod`。  
  
## <a name="security"></a>安全性  
  
### <a name="wse-30-web-services-that-are-secured-using-a-policy-file"></a>使用策略文件保护其安全的 WSE 3.0 Web 服务  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以使用配置文件来保护服务的安全，该机制与 WSE 3.0 策略文件相似。 在 WSE 3.0 中，当使用策略文件来保护 Web 服务的安全时，可以使用关守安全断言或自定义策略断言。 关守安全断言严格映射到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全绑定元素的身份验证模式。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 身份验证模式和 WSE 3.0 关守安全断言不仅名称相同或相似，而且还使用相同的凭据类型来保护消息的安全。 例如，WSE 3.0 中的 `usernameForCertificate` 关守安全断言映射到 `UsernameForCertificate` 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 身份验证模式。 下面的代码示例演示一个使用 WSE 3.0 中的 `usernameForCertificate` 关守安全断言的最小策略如何映射到自定义绑定中使用的 `UsernameForCertificate` 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 身份验证模式。  
  
 **WSE 3.0**  
  
```  
<policies>  
  <policy name="MyPolicy">  
    <usernameForCertificate messageProtectionOrder="SignBeforeEncrypt"  
                            requireDeriveKeys="true"/>  
  </policy>  
</policies>  
```  
  
 **WCF**  
  
```  
<customBinding>  
  <binding name="MyBinding">  
    <security authenticationMode="UserNameForCertificate"   
              messageProtectionOrder="SignBeforeEncrypt"  
              requireDerivedKeys="true"/>  
  </binding>  
</customBinding>  
```  
  
 若要将策略文件中指定的 WSE 3.0 Web 服务的安全设置迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，必须在配置文件中创建一个自定义绑定，并且必须将关守安全断言设置为它的等效身份验证模式。 此外，当 WSE 3.0 客户端与服务进行通信时，必须将自定义绑定配置为使用 2004 年 8 月版 WS-Addressing 规范。 当所迁移的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务不需要与 WSE 3.0 客户端进行通信并且必须保持同等安全性时，请考虑使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的具有适当安全设置的系统定义绑定，而不是创建自定义绑定。  
  
 下表列出了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 WSE 3.0 策略文件和等效自定义绑定之间的映射。  
  
|WSE 3.0 关守安全断言|WCF 自定义绑定配置|  
|----------------------------------------|--------------------------------------|  
|<usernameOverTransportSecurity></usernameOverTransportSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UserNameOverTransport" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<mutualCertificate10Security></mutualCertificate10Security>\>|`<customBinding>   <binding name="MyBinding">     <security messageSecurityVersion="WSSecurity10WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10" authenticationMode="MutualCertificate" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<usernameForCertificateSecurity></usernameForCertificateSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UsernameForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<anonymousForCertificateSecurity></anonymousForCertificateSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="AnonymousForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<kerberosSecurity></kerberosSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="Kerberos"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<mutualCertificate11Security></mutualCertificate11Security>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="MutualCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
  
 有关在 WCF 中创建自定义绑定的详细信息，请参阅[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
### <a name="wse-30-web-services-that-are-secured-using-application-code"></a>使用应用程序代码保护其安全的 WSE 3.0 Web 服务  
 无论是使用 WSE 3.0 还是使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，都可以在应用程序代码而不是配置中指定安全要求。 在 WSE 3.0 中，可以通过以下方法完成此工作：创建一个派生自 `Policy` 类的类，然后通过调用 `Add` 方法添加相应的要求。 在代码中指定的安全要求的详细信息，请参阅[如何︰ 安全 Web 服务而无需使用策略文件](http://go.microsoft.com/fwlink/?LinkId=73747)。 在[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，若要在代码中指定安全要求，创建的实例<xref:System.ServiceModel.Channels.BindingElementCollection>类，并将实例添加<xref:System.ServiceModel.Channels.SecurityBindingElement>到<xref:System.ServiceModel.Channels.BindingElementCollection>。 可使用的静态身份验证模式帮助器方法设置安全断言要求<xref:System.ServiceModel.Channels.SecurityBindingElement>类。 有关在代码中使用指定的安全要求更多细节[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅[如何︰ 自定义绑定使用 SecurityBindingElement 创建](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)和[如何︰ 为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)。  
  
### <a name="wse-30-custom-policy-assertion"></a>WSE 3.0 自定义策略断言  
 在 WSE 3.0 中，有两种类型的自定义策略断言：保护 SOAP 消息安全的策略断言和不保护 SOAP 消息安全的策略断言。 保护 SOAP 消息安全的策略断言派生自 WSE 3.0`SecurityPolicyAssertion`类，并在概念上的等效[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]是<xref:System.ServiceModel.Channels.SecurityBindingElement>类。  
  
 需要特别注意的一点是，WSE 3.0 关守安全断言是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 身份验证模式的子集。 如果已经在 WSE 3.0 中创建了一个自定义策略断言，则可能存在一个等效的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 身份验证模式。 例如，WSE 3.0 没有提供与 `UsernameOverTransport` 关守安全断言等效的 CertificateOverTransport 安全断言，但使用 X.509 证书进行客户端身份验证。 如果您已经为此方案定义自己的自定义策略断言，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会使迁移工作变得非常简单。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]定义此方案中，身份验证模式，因此您可以利用静态身份验证模式帮助器方法来配置[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
 当不存在[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]身份验证模式，它等效于保护 SOAP 消息安全的自定义策略断言派生一个类从<xref:System.ServiceModel.Channels.TransportSecurityBindingElement>， <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>或<xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]类并指定等效的绑定元素。 有关详细信息，请参阅[如何︰ 自定义绑定使用 SecurityBindingElement 创建](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)。  
  
 若要将转换不保护 SOAP 消息的自定义策略断言，请参阅[筛选](../../../../docs/framework/wcf/feature-details/filtering.md)示例和示例[自定义消息拦截器](../../../../docs/framework/wcf/samples/custom-message-interceptor.md)。  
  
### <a name="wse-30-custom-security-token"></a>WSE 3.0 自定义安全令牌  
 用于创建自定义令牌的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 编程模型与 WSE 3.0 不同。 有关在 WSE 中创建自定义令牌的详细信息，请参阅[创建自定义安全令牌](http://go.microsoft.com/fwlink/?LinkID=73750)。 有关创建自定义令牌中的详细信息[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅[如何︰ 创建自定义令牌](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)。  
  
### <a name="wse-30-custom-token-manager"></a>WSE 3.0 自定义令牌管理器  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中用于创建自定义令牌管理器的编程模型与 WSE 3.0 不同。 有关如何创建自定义令牌管理器和其他组件所需的自定义安全令牌的详细信息，请参阅[如何︰ 创建自定义令牌](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)。  
  
> [!NOTE]
>  如果已经创建了一个自定义 `UsernameToken` 安全令牌管理器，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会提供一个比创建自定义安全令牌管理器更容易的机制来指定身份验证逻辑。 有关详细信息，请参阅[如何︰ 使用自定义用户名和密码验证程序](../../../../docs/framework/wcf/feature-details/how-to-use-a-custom-user-name-and-password-validator.md)。  
  
### <a name="wse-30-web-services-that-use-mtom-encoded-soap-messages"></a>使用 MTOM 编码 SOAP 消息的 WSE 3.0 Web 服务  
 像 WSE 3 应用程序一样，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以在配置中指定 MTOM 消息编码。 若要迁移此设置，请添加[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/mtommessageencoding.md)为该服务的绑定。 下面的代码示例演示如何在 WSE 3.0 中为在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中等效的服务指定 MTOM 编码。  
  
 **WSE 3.0**  
  
```  
<messaging>  
    <mtom clientMode="On"/>  
</messaging>  
```  
  
 **WCF**  
  
```  
<customBinding>  
  <binding name="MyBinding">  
    <mtomMessageEncoding/>  
  </binding>  
</customBinding>  
```  
  
## <a name="messaging"></a>消息  
  
### <a name="wse-30-applications-that-use-the-wse-messaging-api"></a>使用 WSE 消息 API 的 WSE 3.0 应用程序  
 当使用 WSE 消息 API 来获取对在客户端和服务之间交换的 XML 的直接访问时，可以将应用程序转换为使用“Plain Old XML”(POX)。 有关 POX 的更多详细信息，请参阅[与 POX 应用程序的互操作性](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md)。 有关 WSE 消息 API 的更多详细信息，请参阅[发送和接收 SOAP 消息使用 WSE 消息 API](http://go.microsoft.com/fwlink/?LinkID=73755)。  
  
## <a name="transports"></a>传输  
  
### <a name="tcp"></a>TCP  
 默认情况下，使用 TCP 传输协议发送 SOAP 消息的 WSE 3.0 客户端和 Web 服务不能与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和 Web 服务进行交互操作。 这一不兼容性是由于 TCP 协议中使用的组帧存在差异以及性能方面的原因。 但是，有一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例详细解释了如何实现能够与 WSE 3.0 进行交互操作的自定义 TCP 会话。 有关此示例的详细信息，请参阅[传输︰ WSE 3.0 TCP 互操作性](../../../../docs/framework/wcf/samples/transport-wse-3-0-tcp-interoperability.md)。  
  
 若要指定[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]应用程序使用 TCP 传输，请使用[ <> \</> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)。  
  
### <a name="custom-transport"></a>自定义传输协议  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，与 WSE 3.0 自定义传输协议等效的机制是通道扩展。 有关创建通道扩展的详细信息，请参阅[扩展通道层](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md)。  
  
## <a name="see-also"></a>另请参阅  
 [基本编程生命周期](../../../../docs/framework/wcf/basic-programming-lifecycle.md)   
 [自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [如何︰ 创建自定义绑定使用 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [如何︰ 为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)