---
title: "如何：配置 WCF 服务以便与 WSE 3.0 客户端进行互操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f38c4a0-49a6-437c-bdde-ad1d138d3c4a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：配置 WCF 服务以便与 WSE 3.0 客户端进行互操作
在将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务配置为使用 WS\-Addressing 规范的 2004 年 8 月版时，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务与 Web Services Enhancements 3.0 for Microsoft .NET 客户端具有网络级别兼容性。  
  
### 使 WCF 服务与 WSE 3.0 客户端进行互操作  
  
1.  定义 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的自定义绑定。  
  
     若要指定将 WS\-Addressing 规范的 2004 年 8 月版用于消息编码，必须创建自定义绑定。  
  
    1.  将子级 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)添加到服务的配置文件的 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)。  
  
    2.  通过将 [\<绑定\>](../../../../docs/framework/misc/binding.md)添加到 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)中并设置 `name` 属性，为绑定指定一个名称。  
  
    3.  通过将子级 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)添加到 [\<绑定\>](../../../../docs/framework/misc/binding.md)中，指定身份验证模式和用于保护消息安全的 WS\-Security 规范的版本，该版本与 WSE 3.0 兼容。  
  
         若要设置身份验证模式，请设置 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)的 `authenicationMode` 属性。身份验证模式大致等效于 WSE 3.0 中的关守安全断言。下表将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的身份验证模式映射为 WSE 3.0 中的关守安全断言。  
  
        |WCF 身份验证模式|WSE 3.0 关守安全断言|  
        |----------------|--------------------|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`anonymousForCertificateSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`kerberosSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`mutualCertificate10Security`\*|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`mutualCertificate11Security`\*|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`usernameOverTransportSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`usernameForCertificateSecurity`|  
  
         \*`mutualCertificate10Security` 和 `mutualCertificate11Security` 关守安全断言之间的主要区别在于，WSE 用于保护 SOAP 消息的 WS\-Security 规范的版本不同。`mutualCertificate10Security` 使用 WS\-Security 1.0，而 WS\-Security 1.1 用于 `mutualCertificate11Security`。对于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，WS\-Security 规范的版本在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)的 `messageSecurityVersion` 属性中指定。  
  
         若要设置用于保证 SOAP 消息安全的 WS\-Security 规范的版本，请设置 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)的 `messageSecurityVersion` 属性。若要与 WSE 3.0 进行互操作，请将 `messageSecurityVersion` 属性的值设置为 <xref:System.ServiceModel.MessageSecurityVersion.WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10%2A>。  
  
    4.  通过添加 [\<textMessageEncoding\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md)并将 `messageVersion` 设置为它的 <xref:System.ServiceModel.Channels.MessageVersion.Soap11WSAddressingAugust2004%2A> 的值，指定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-Addressing 规范的 2004 年 8 月版本。  
  
        > [!NOTE]
        >  在使用 SOAP 1.2 时，请将 `messageVersion` 属性设置为 <xref:System.ServiceModel.Channels.MessageVersion.Soap12WSAddressingAugust2004%2A>。  
  
2.  指定该服务使用自定义绑定。  
  
    1.  将[\<endpoint（终结点）\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)元素的 `binding` 属性设置为 `customBinding`。  
  
    2.  将[\<endpoint（终结点）\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)元素的 `bindingConfiguration` 属性设置为在 [\<绑定\>](../../../../docs/framework/misc/binding.md)的 `name` 属性中为自定义绑定指定的值。  
  
## 示例  
 下面的代码示例指定 `Service.HelloWorldService` 使用自定义绑定与 WSE 3.0 客户端进行互操作。自定义绑定指定使用 WS\-Addressing 的 2004 年 8 月版本和 WS\-Security 1.1 规范集对所交换的消息进行编码。使用 <xref:System.ServiceModel.Configuration.AuthenticationMode> 身份验证模式保证消息的安全。  
  
```  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
        behaviorConfiguration="ServiceBehavior"   
        name="Service.HelloWorldService">  
        <endpoint binding="customBinding" address=""  
          bindingConfiguration="ServiceBinding"  
          contract="Service.IHelloWorld"></endpoint>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="ServiceBinding">  
          <security authenticationMode="AnonymousForCertificate"  
                  messageProtectionOrder="SignBeforeEncrypt"  
                  messageSecurityVersion="WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10"  
                  requireDerivedKeys="false">  
          </security>  
          <textMessageEncoding messageVersion ="Soap11WSAddressingAugust2004"></textMessageEncoding>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    <behaviors>  
      <behavior name="ServiceBehavior" returnUnknownExceptionsAsFaults="true">  
        <serviceCredentials>  
          <serviceCertificate findValue="CN=WCFQuickstartServer" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName"/>  
        </serviceCredentials>  
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## 请参阅  
 [如何：自定义系统提供的绑定](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)