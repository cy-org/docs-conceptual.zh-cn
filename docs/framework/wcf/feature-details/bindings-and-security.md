---
title: "绑定与安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "绑定 [WCF]"
  - "绑定 [WCF], 安全"
  - "WCF 安全"
  - "Windows Communication Foundation, 安全"
ms.assetid: 4de03dd3-968a-4e65-af43-516e903d7f95
caps.latest.revision: 42
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 42
---
# 绑定与安全
包含在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的系统提供的绑定提供了一种编写 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的快捷方法。但有一个例外，就是所有绑定都启用了默认的安全方案。本主题将帮助您根据安全需要来选择正确的绑定。  
  
 有关 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全性的概述，请参见[安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用绑定进行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 编程的更多信息，请参见 [WCF 安全编程](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)。  
  
 如果已经选择了绑定，有关安全性的关联运行时行为的更多信息，请参见 [安全行为](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)。  
  
 部分安全性功能无法用系统提供的绑定进行编程。有关如何更为灵活地使用自定义绑定的信息，请参见[使用自定义绑定的安全功能](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)。  
  
## 绑定的安全功能  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 包含许多由系统提供的绑定，这些绑定可以满足大多数需求。如果某个特定绑定不能满足要求，您还可以创建自定义绑定。有关系统提供的绑定的列表，请参见[系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]自定义绑定的更多信息，请参见[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的每个绑定都具有两种形式：一种是 API，一种是在配置文件中使用的 XML 元素。例如，`WSHttpBinding` \(API\) 在 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 中具有对应项。  
  
 下一节列出了每个绑定的两种形式，并概括了安全功能。  
  
### BasicHttp  
 在代码中，请使用 <xref:System.ServiceModel.BasicHttpBinding> 类；在配置中，请使用 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)。  
  
 此绑定的目的是与如下一系列现有技术一起使用：  
  
-   ASP.NET Web 服务 \(ASMX\) 版本 1。  
  
-   Web Service Enhancements \(WSE\) 应用程序。  
  
-   Web 服务互操作性 \(WS\-I\) 规范中定义的基本配置文件（[http:\/\/go.microsoft.com\/fwlink\/?LinkId\=38955](http://go.microsoft.com/fwlink/?LinkId=38955)（可能为英文网页））。  
  
-   WS\-I 中定义的基本安全配置文件。  
  
 默认情况下，此绑定是不安全的。它的目的是与 ASMX 服务进行互操作。启用安全性后，此绑定可以与 Internet 信息服务 \(IIS\) 安全机制（例如基本身份验证、摘要和 Windows 集成安全性）进行无缝的互操作。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][传输安全概述](../../../../docs/framework/wcf/feature-details/transport-security-overview.md).此绑定支持以下功能：  
  
-   HTTPS 传输安全。  
  
-   HTTP 基本身份验证。  
  
-   WS\-Security。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.BasicHttpSecurity>、<xref:System.ServiceModel.BasicHttpMessageSecurity>、<xref:System.ServiceModel.BasicHttpMessageCredentialType> 和 <xref:System.ServiceModel.BasicHttpSecurityMode>。  
  
### WSHttpBinding  
 在代码中，请使用 <xref:System.ServiceModel.WSHttpBinding> 类；在配置中，请使用 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)。  
  
 默认情况下，此绑定实现 WS\-Security 规范，并提供与实现 WS\-\* 规范的服务的互操作性。它支持以下功能：  
  
-   HTTPS 传输安全。  
  
-   WS\-Security。  
  
-   使用 SOAP 消息凭据安全对调用方进行身份验证的 HTTPS 传输保护。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSHttpSecurity>、<xref:System.ServiceModel.MessageSecurityOverHttp>、<xref:System.ServiceModel.MessageCredentialType>、<xref:System.ServiceModel.SecurityMode>、<xref:System.ServiceModel.HttpTransportSecurity>、<xref:System.ServiceModel.HttpClientCredentialType> 和 <xref:System.ServiceModel.HttpProxyCredentialType>。  
  
### WSDualHttpBinding  
 在代码中，请使用 <xref:System.ServiceModel.WSDualHttpBinding> 类；在配置中，请使用 [\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)。  
  
 此绑定的目的是启用双工服务应用程序。此绑定实现了 WS\-Security 规范，以便获得基于消息的传送安全。传输安全不可用。默认情况下，它提供下列功能：  
  
-   实现 WS\-Reliable Messaging 以保证可靠性。  
  
-   实现 WS\-Security 以保证传送安全和身份验证。  
  
-   使用 HTTP 进行消息传递。  
  
-   使用文本\/XML 消息编码。  
  
 使用 WS\-Security（消息层安全性），可通过此绑定配置下列参数：  
  
-   用来确定加密算法的安全算法组。  
  
-   下列功能的绑定选项：  
  
    -   提供可在客户端带外使用的服务凭据。  
  
    -   提供从服务协商的服务凭据作为通道设置的一部分。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSDualHttpSecurity> 和 <xref:System.ServiceModel.WSDualHttpSecurityMode>。  
  
### NetTcpBinding  
 在代码中，请使用 <xref:System.ServiceModel.NetTcpBinding> 类；在配置中，请使用 [\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)。  
  
 此绑定针对计算机之间的通信进行了优化。默认情况下，它具有以下特征：  
  
-   实现传输层安全性。  
  
-   利用 Windows 安全性来实现传送安全性和身份验证。  
  
-   使用 TCP 进行传输。  
  
-   实现二进制消息编码。  
  
-   实现 WS\-Reliable Messaging。  
  
 此绑定具有下列选项：  
  
-   消息层安全性（使用 WS\-Security）。  
  
-   使用消息凭据实现传输安全性：保密性和完整性由 Transport Layer Security \(TLS\) over TCP 提供，授权凭据由 WS\-Security 提供。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetTcpSecurity>、<xref:System.ServiceModel.TcpTransportSecurity>、<xref:System.ServiceModel.TcpClientCredentialType>、<xref:System.ServiceModel.MessageSecurityOverTcp> 和 <xref:System.ServiceModel.MessageCredentialType>。  
  
### NetNamedPipeBinding  
 在代码中，请使用 <xref:System.ServiceModel.NetNamedPipeBinding> 类；在配置中，请使用 [\<netNamedPipeBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md)。  
  
 此绑定针对进程之间的通信（通常在同一台计算机上）进行了优化。默认情况下，此绑定具有以下特征：  
  
-   使用传输安全性来实现消息传输和身份验证。  
  
-   使用命名管道进行消息传递。  
  
-   实现二进制消息编码。  
  
-   加密和消息签名。  
  
 此绑定具有下列选项：  
  
-   使用 Windows 安全性进行身份验证。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetNamedPipeSecurity>、<xref:System.ServiceModel.NetNamedPipeSecurityMode> 和 <xref:System.ServiceModel.NamedPipeTransportSecurity>。  
  
### MsmqIntegrationBinding  
 在代码中，请使用 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 类；在配置中，请使用 [\<msmqIntegrationBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)。  
  
 此绑定最适合于创建与非 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Microsoft 消息队列 \(MSMQ\) 终结点进行互操作的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和服务。  
  
 默认情况下，此绑定使用传输安全性并提供下列安全特征：  
  
-   可以禁用安全性 \(None\)。  
  
-   MSMQ 传输安全性 \(Transport\)。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetMsmqSecurity> 和 <xref:System.ServiceModel.NetMsmqSecurityMode>。  
  
### NetMsmqBinding  
 在代码中，请使用 <xref:System.ServiceModel.NetMsmqBinding> 类；在配置中，请使用 [\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)。  
  
 此绑定适合在创建需要 MSMQ 排队消息支持的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务时使用。  
  
 默认情况下，此绑定使用传输安全性并提供下列安全特征：  
  
-   可以禁用安全性 \(None\)。  
  
-   MSMQ 传输安全性 \(Transport\)。  
  
-   基于 SOAP 的消息安全性 \(Message\)。  
  
-   同时启用传输安全性和消息安全性 \(Both\)。  
  
-   支持的客户端凭据类型：None、Windows、UserName、Certificate、IssuedToken。  
  
 仅当安全模式设置为 <xref:System.ServiceModel.NetMsmqSecurityMode> 或 <xref:System.ServiceModel.NetMsmqSecurityMode> 时，才支持 <xref:System.ServiceModel.MessageCredentialType> 凭据。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.MessageSecurityOverMsmq> 和 <xref:System.ServiceModel.MsmqTransportSecurity>。  
  
### WSFederationHttpBinding  
 在代码中，请使用 <xref:System.ServiceModel.WSFederationHttpBinding> 类；在配置中，请使用 [\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)。  
  
 默认情况下，此绑定使用 WS\-Security（消息层安全性）。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [联合](../../../../docs/framework/wcf/feature-details/federation.md)、<xref:System.ServiceModel.WSFederationHttpSecurity> 和 <xref:System.ServiceModel.WSFederationHttpSecurityMode>。  
  
## 自定义绑定  
 如果系统提供的绑定都不能满足您的要求，则可以使用自定义安全绑定元素来创建自定义绑定。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][使用自定义绑定的安全功能](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md).  
  
## 绑定选择  
 下表概括了安全模式设置中提供的功能，也就是说，它列出了当安全模式设置为 `Transport`、`Message` 或 `TransportWithMessageCredential` 时可以使用的功能。使用此表可帮助您找到应用程序所需的安全功能。  
  
|设置|功能|  
|--------|--------|  
|Transport|服务器身份验证<br /><br /> 客户端身份验证<br /><br /> 点对点安全性<br /><br /> 互操作性<br /><br /> 硬件加速<br /><br /> 高吞吐量<br /><br /> 安全防火墙<br /><br /> 高延迟应用程序<br /><br /> 跨越多个跃点重新加密|  
|Message|服务器身份验证<br /><br /> 客户端身份验证<br /><br /> 端对端安全性<br /><br /> 互操作性<br /><br /> 丰富的声明<br /><br /> 联合<br /><br /> 多因素身份验证<br /><br /> 自定义令牌<br /><br /> 公证人\/时间戳服务<br /><br /> 高延迟应用程序<br /><br /> 消息签名的持久性|  
|TransportWithMessageCredential|服务器身份验证<br /><br /> 客户端身份验证<br /><br /> 点对点安全性<br /><br /> 互操作性<br /><br /> 硬件加速<br /><br /> 高吞吐量<br /><br /> 丰富的客户端声明<br /><br /> 联合<br /><br /> 多因素身份验证<br /><br /> 自定义令牌<br /><br /> 安全防火墙<br /><br /> 高延迟应用程序<br /><br /> 跨越多个跃点重新加密|  
  
 下表列出了支持各种模式设置的绑定。请从该表中选择用来创建服务终结点的绑定。  
  
|绑定|是否支持 Transport 模式|是否支持 Message 模式|是否支持 TransportWithMessageCredential|  
|--------|-----------------------|---------------------|-----------------------------------------|  
|`BasicHttpBinding`|是|是|是|  
|`WSHttpBinding`|是|是|是|  
|`WSDualHttpBinding`|否|是|否|  
|`NetTcpBinding`|是|是|是|  
|`NetNamedPipeBinding`|是|否|否|  
|`NetMsmqBinding`|是|是|否|  
|`MsmqIntegrationBinding`|是|否|否|  
|`wsFederationHttpBinding`|否|是|是|  
  
## 绑定中的传输凭据  
 下表列出了在传输安全模式下使用 `BasicHttpBinding` 或 `WSHttpBinding` 时可用的客户端凭据类型。  
  
|类型|说明|  
|--------|--------|  
|None|指定客户端不需要提供任何凭据。这相当于匿名客户端。|  
|Basic|基本身份验证[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]位于 [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=84023](http://go.microsoft.com/fwlink/?LinkId=84023)（可能为英文网页）的“RFC 2617 – HTTP Authentication: Basic and Digest Authentication”（RFC 2617 – HTTP 身份验证：基本和摘要式身份验证）。|  
|Digest|摘要式身份验证。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]位于 [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=84023](http://go.microsoft.com/fwlink/?LinkId=84023)（可能为英文网页）的“RFC 2617 – HTTP Authentication: Basic and Digest Authentication”（RFC 2617 – HTTP 身份验证：基本和摘要式身份验证）。|  
|NTLM|NT LAN Manager \(NTLM\) 身份验证。|  
|Windows|Windows 身份验证。|  
|Certificate|使用证书执行的身份验证。|  
|IssuedToken|允许服务要求使用由安全令牌服务或 [!INCLUDE[infocard](../../../../includes/infocard-md.md)] 颁发的令牌对客户端进行身份验证。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][联合令牌与颁发的令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).|  
  
### 绑定中的消息客户端凭据  
 下表列出在 Message 安全模式下使用绑定时可用的客户端凭据类型。  
  
|类型|说明|  
|--------|--------|  
|None|允许服务与匿名客户端交互。|  
|Windows|允许在 Windows 凭据的已通过身份验证的上下文中执行 SOAP 消息交换。|  
|用户名|允许服务要求使用用户名凭据对客户端进行身份验证。请注意，当安全模式设置为 `TransportWithMessageCredential` 时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不支持发送密码摘要，也不支持使用密码派生密钥并将这样的密钥用于 Message 模式安全。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 强制要求在使用用户名凭据时确保传输的安全性。|  
|证书|允许服务要求使用证书对客户端进行身份验证。|  
|IssuedToken|允许服务使用安全令牌服务来提供自定义令牌。|  
  
## 请参阅  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [选择凭据类型](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [使用自定义绑定的安全功能](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)   
 [安全行为](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Windows Server App Fabric 的安全模型](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x804)