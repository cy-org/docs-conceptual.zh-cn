---
title: "传输安全概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00959326-aa9d-44d0-af61-54933d4adc7f
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# 传输安全概述
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的传输安全机制取决于使用的绑定和传输。 例如，当使用<xref:System.ServiceModel.WSHttpBinding>类中，传输为 HTTP，且用于保护传输安全的主要机制是通过 HTTP，通常称为 HTTPS 安全套接字层 (SSL)。 本主题讨论 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 系统提供的绑定中使用的主要传输安全机制。  
  
> [!NOTE]
>  将 SSL 安全与 .NET Framework 3.5 及更高版本一起使用时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端将同时使用其证书存储区中的中间证书和 SSL 协商期间收到的中间证书，对服务的证书执行证书链验证。 .NET Framework 3.0 仅使用本地证书存储区中安装的中间证书。  
  
> [!WARNING]
>  当使用传输安全时， <xref:System.Treading.Thread.CurrentPrincipal%2A>属性可能会被覆盖。 若要避免这种情况发生集<xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermission%2A>为无。 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>是可以在服务说明设置的服务行为。  
  
## <a name="basichttpbinding"></a>BasicHttpBinding  
 默认情况下， <xref:System.ServiceModel.BasicHttpBinding>类不提供安全性。 此绑定旨在提供与不实现安全机制的 Web 服务提供程序的互操作性。 但是，您可以切换对安全性通过设置<xref:System.ServiceModel.BasicHttpSecurity.Mode%2A>属性设置为之外的任何值<xref:System.ServiceModel.BasicHttpSecurityMode>。 若要启用传输安全，请将属性设置为<xref:System.ServiceModel.BasicHttpSecurityMode>。  
  
### <a name="interoperation-with-iis"></a>与 IIS 的互操作  
 <xref:System.ServiceModel.BasicHttpBinding>类主要用于与现有的 Web 服务进行互操作且的许多服务承载由 Internet 信息服务 (IIS)。 因此，此绑定的传输安全旨在实现与 IIS 站点的无缝互操作。 这通过将安全模式设置为<xref:System.ServiceModel.BasicHttpSecurityMode>，然后设置客户端凭据类型。 凭据类型值对应于 IIS 目录安全机制。 下面的代码演示如何设置模式以及如何将凭据类型设置为 Windows。 当客户端和服务器在同一个 Windows 域中时，您可以使用此配置。  
  
 [!code-csharp[c_ProgrammingSecurity#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#10)]
 <!-- TODO: review snippet reference [!code-vb[c_ProgrammingSecurity#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#10)]  -->  
  
 或在配置中：  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <binding name="SecurityByTransport">  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" />  
       </security>  
     </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 以下几节讨论其他客户端凭据类型。  
  
#### <a name="basic"></a>Basic  
 这对应于 IIS 中的基本身份验证方法。 使用此模式时，必须为 IIS 服务器配置 Windows 用户帐户和适当的 NTFS 文件系统权限。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)]请参阅[启用基本身份验证和配置领域名](http://go.microsoft.com/fwlink/?LinkId=88592)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)]请参阅[IIS 7.0 Beta︰ 配置基本身份验证](http://go.microsoft.com/fwlink/?LinkId=88593)。  
  
#### <a name="certificate"></a>证书  
 IIS 有一个要求客户端使用证书进行登录的选项。 此功能还可以使 IIS 将客户端证书映射到 Windows 帐户。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)]请参阅[在 IIS 6.0 中启用客户端证书](http://go.microsoft.com/fwlink/?LinkId=88594)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)]请参阅[IIS 7.0 Beta︰ 在 IIS 7.0 中配置服务器证书](http://go.microsoft.com/fwlink/?LinkId=88595)。  
  
#### <a name="digest"></a>摘要  
 摘要式身份验证类似于基本身份验证，但其具有以哈希形式而不是明文形式发送凭据的优点。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)]请参阅[在 IIS 6.0 中的摘要式身份验证](http://go.microsoft.com/fwlink/?LinkID=88443)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)]请参阅[IIS 7.0 Beta︰ 配置摘要式身份验证](http://go.microsoft.com/fwlink/?LinkId=88596)。  
  
#### <a name="windows"></a>Windows  
 这对应于 IIS 中的集成 Windows 身份验证。 设置为此值时，还需要服务器位于使用 Kerberos 协议作为其域控制器的 Windows 域中。 如果服务器不在支持 Kerberos 的域中，或者如果 Kerberos 系统失败，您可以使用下一节中说明的 NT LAN Manager (NTLM) 值。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)]请参阅[集成 Windows 身份验证在 IIS 6.0 中](http://go.microsoft.com/fwlink/?LinkId=88597)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)]请参阅[IIS 7.0 Beta︰ 在 IIS 7.0 中配置服务器证书](http://go.microsoft.com/fwlink/?LinkId=88595)。  
  
#### <a name="ntlm"></a>NTLM  
 这使服务器可以在 Kerberos 协议失败时使用 NTLM 进行身份验证。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]配置 IIS 中的[!INCLUDE[iis601](../../../../includes/iis601-md.md)]，请参阅[强制 NTLM 身份验证](http://go.microsoft.com/fwlink/?LinkId=88598)。 对于 [!INCLUDE[iisver](../../../../includes/iisver-md.md)]，Windows 身份验证包括 NTLM 身份验证。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS 7.0 Beta︰ 在 IIS 7.0 中配置服务器证书](http://go.microsoft.com/fwlink/?LinkID=88595)。  
  
## <a name="wshttpbinding"></a>WsHttpBinding  
 <xref:System.ServiceModel.WSHttpBinding>类专用于与实现 WS-服务进行互操作 * 规范。 此绑定的传输安全为 HTTP 上的安全套接字层 (SSL)，即 HTTPS。 若要创建使用 SSL 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序，请使用 IIS 承载该应用程序。 或者，如果您要创建自承载的应用程序，请使用 HttpCfg.exe 工具将 X.509 证书绑定到计算机上的特定端口。 端口号作为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的一部分以终结点地址的形式进行指定。 使用传输模式时，终结点地址必须包括 HTTPS 协议，否则运行时将引发异常。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][HTTP 传输安全](../../../../docs/framework/wcf/feature-details/http-transport-security.md)。  
  
 对于客户端身份验证设置<xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A>属性<xref:System.ServiceModel.HttpTransportSecurity>类传递给之一<xref:System.ServiceModel.HttpClientCredentialType>枚举值。 枚举值是相同的客户端凭据类型为<xref:System.ServiceModel.BasicHttpBinding> ，旨在与 IIS 服务承载。  
  
 下面的示例演示与 Windows 的客户端凭据类型一起使用的绑定。  
  
 [!code-csharp[c_ProgrammingSecurity#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#11)]
 [!code-vb[c_ProgrammingSecurity#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#11)]  
  
## <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 此绑定只提供消息级别的安全，不提供传输级别的安全。  
  
## <a name="nettcpbinding"></a>NetTcpBinding  
 <xref:System.ServiceModel.NetTcpBinding>类使用 TCP 进行消息传输。 通过实现 TCP 上的传输层安全性 (TLS) 为传输模式提供安全。 由操作系统提供 TLS 实现。  
  
 此外可以通过设置指定客户端的凭据类型<xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A>属性<xref:System.ServiceModel.TcpTransportSecurity>类传递给之一<xref:System.ServiceModel.TcpClientCredentialType>值，如下面的代码中所示。  
  
 [!code-csharp[c_ProgrammingSecurity#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#12)]
 [!code-vb[c_ProgrammingSecurity#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#12)]  
  
#### <a name="client"></a>客户端  
 在客户端，您必须指定证书使用<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>方法<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>类。  
  
> [!NOTE]
>  如果您要使用 Windows 安全性，则不需要证书。  
  
 下面的代码使用唯一标识证书的证书指纹。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]证书，请参见[使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。  
  
 [!code-csharp[c_ProgrammingSecurity#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#13)]
 [!code-vb[c_ProgrammingSecurity#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#13)]  
  
 或者，在客户端的配置中指定的证书使用[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)的 behaviors 节中的元素。  
  
```xml  
<behaviors>  
  <behavior>  
   <clientCredentials>  
     <clientCertificate findValue= "101010101010101010101010101010000000000"   
      storeLocation="LocalMachine" storeName="My"   
      X509FindType="FindByThumbPrint"/>  
     </clientCertificate>  
   </clientCredentials>  
 </behavior>  
</behaviors>    
```  
  
## <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 <xref:System.ServiceModel.NetNamedPipeBinding>类用于进行有效的计算机内通信; 也就是说，为进程在同一台计算机上运行，尽管命名管道通道您可以创建同一网络上的两台计算机之间。 此绑定只提供传输级别的安全。 在创建使用此绑定的应用程序时，终结点地址必须包括“net.pipe”作为终结点地址的协议。  
  
## <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 此绑定使用传输安全时，使用 SSL over HTTP，称为 HTTPS 与已颁发的令牌 (<xref:System.ServiceModel.WSFederationHttpSecurityMode>)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]联合应用程序，请参阅[联合令牌与颁发的令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。  
  
## <a name="netpeertcpbinding"></a>NetPeerTcpBinding  
 <xref:System.ServiceModel.NetPeerTcpBinding>类是旨在使用对等网络功能进行有效通信的安全传输。 TCP 是协议，这与类和绑定的名称相一致。 当安全模式设置为“传输”时，绑定将实现 TCP 上的 TLS。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]对等功能，请参阅[对等网络](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)。  
  
## <a name="msmqintegrationbinding-and-netmsmqbinding"></a>MsmqIntegrationBinding 和 NetMsmqBinding  
 有关传输的完整讨论安全与消息队列 （以前称为 MSMQ），请参阅[使用传输安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [WCF 安全编程](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)