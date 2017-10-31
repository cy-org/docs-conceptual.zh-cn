---
title: "分布式应用程序安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "分布式应用程序安全 [WCF]"
  - "安全 [WCF], 传输"
ms.assetid: 53928a10-e474-46d0-ab90-5f98f8d7b668
caps.latest.revision: 32
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 32
---
# 分布式应用程序安全
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 安全分为三个主要功能区域：传输安全、访问控制和审核。传输安全提供完整性、保密性和身份验证。传输安全由传送安全、消息安全或 `TransportWithMessageCredential` 实现。  
  
 有关 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息安全的概述，请参见[安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]其他两种 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全的更多信息，请参见[授权](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)和[审核](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)。  
  
## 传输安全方案  
 使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 传输安全的常见方案包括：  
  
-   使用 Windows 确保传输安全。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和服务部署在 Windows 域（或 Windows 目录林）中。消息包含个人数据，因此要求客户端和服务相互进行身份验证，要求实现消息完整性和消息保密性。此外，还需要有已发生特定事务的证明，例如，消息的接收方应记录签名信息。  
  
-   使用 `UserName` 和 HTTPS 确保传输安全。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和服务需要一些开发工作，以便通过 Internet 工作。客户端凭据根据数据库（其中的内容为用户名\/密码对）进行身份验证。服务是用受信任的安全套接字层 \(SSL\) 证书部署在一个 HTTPS 地址的。由于消息是通过 Internet 传输的，因此，客户端和服务需要相互进行身份验证，并且必须在传输过程中保持消息的保密性和完整性。  
  
-   使用证书确保传输安全。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和服务需要一些开发工作，以便通过公共 Internet 工作。客户端和服务都具有可用于确保消息安全的证书。客户端和服务通过 Internet 进行相互通信，执行要求消息完整性、保密性和相互身份验证的重要事务。  
  
## 完整性、保密性和身份验证  
 三项功能 — 完整性、保密性和身份验证 — 合称为传输安全。传输安全提供的这些功能，有助于减轻对分布式应用程序的威胁。下表简要介绍构成传输安全的三项功能。  
  
|功能|说明|  
|--------|--------|  
|完整性|完整性可以确保数据是完整、准确的，在数据从一点移动到另一点，并可能由多个操作者读取的情况下，尤其如此。完整性必须得到维护，以免数据被篡改，这通常是由消息的数字签名实现的。|  
|保密性|保密性可以确保消息不被目标读取者以外的任何人读取。例如，信用卡号在通过 Internet 发送时必须保密。保密性通常是用公钥\/私钥方案进行数据加密实现的。|  
|身份验证|身份验证是对已声明标识进行的验证。例如，当使用银行帐户时，必须只允许帐户的实际所有者取款。有多种方式可以实现身份验证。一个常用方法是使用用户\/密码系统。第二个方法是使用第三方提供的 X.509 证书。|  
  
## 安全模式  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 有多种传输安全模式，如下表所述。  
  
|模式|说明|  
|--------|--------|  
|None|传输层和消息层都不提供安全措施。默认情况下，预定义绑定都不使用此模式，只有 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) 元素（使用代码时，则为 <xref:System.ServiceModel.BasicHttpBinding> 类）例外。|  
|Transport|使用安全传送（如 HTTPS）实现完整性、保密性和相互身份验证。|  
|Message|使用 SOAP 消息安全实现完整性、保密性和相互身份验证。SOAP 消息是按照 WS\-Security 标准获得保护的。|  
|混合模式|使用传送安全实现完整性、保密性和服务器身份验证。使用消息安全（WS\-Security 和其他标准）实现客户端身份验证。<br /><br /> （此模式的枚举值是 `TransportWithMessageCredential`。）|  
|消息和传送|在传送级别和消息级别都执行保护和身份验证。此模式仅在 [\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md) 元素中可用。|  
  
## 凭据和传输安全  
 凭据是一些数据，用于证实已声明标识或功能。提交凭据涉及提交的数据和数据的所有权证明。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持多种凭据类型的传输和消息安全性级别。您可以为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定指定凭据类型。  
  
 在许多国家和地区，驾驶执照就是凭据的一个示例。该执照中包含表示个人身份和能力的数据。它以持有人照片的形式包含所有权证明。该执照由受信任的颁发机构颁发，通常是获得许可的政府部门。该执照采用密封形式且包含一张全息图，表明它未经改动或伪造。  
  
 例如，考虑 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中支持的两种凭据类型：用户名和 \(X.509\) 证书凭据。  
  
 对于用户名凭据，用户名表示已声明标识，密码表示所有权证明。这种情况下，受信任的颁发机构则是验证用户名和密码的系统。  
  
 在证书凭据中，主题名称、主题备用名称或证书中的特定字段可用于表示已声明标识和\/或功能。凭据中的数据所有权证明的建立，是用关联私钥生成签名实现的。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]传输安全编程和指定凭据的更多信息，请参见[绑定与安全](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)和 [安全行为](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)。  
  
### 传送客户端凭据类型  
 下表列出了在创建使用传输安全的应用程序时可能使用的值。在代码或绑定设置中，可以使用这些值。  
  
|设置|说明|  
|--------|--------|  
|None|指定客户端不需要提供任何凭据。这相当于匿名客户端。|  
|Basic|指定基本身份验证。有关其他信息，请参见 RFC2617“[HTTP 身份验证：基本和摘要式身份验证](http://go.microsoft.com/fwlink/?LinkId=88313)（可能为英文网页）。”|  
|Digest|指定摘要式身份验证。有关其他信息，请参见 RFC2617“[HTTP 身份验证：基本和摘要式身份验证](http://go.microsoft.com/fwlink/?LinkId=88313)（可能为英文网页）。”|  
|Ntlm|指定在 Windows 域中使用 SSPI 协商进行 Windows 身份验证。<br /><br /> 要使用 SSPI 协商，就需要使用 Kerberos 协议或 NT LanMan \(NTLM\)。|  
|Windows|指定在 Windows 域中使用 SSPI 进行 Windows 身份验证。SSPI 选择 Kerberos 协议或 NTLM 作为身份验证服务。<br /><br /> SSPI 首先尝试 Kerberos 协议；如果失败，则使用 NTLM。|  
|Certificate|使用证书（通常是 X.509）执行客户端身份验证。|  
  
### 消息客户端凭据类型  
 下表列出了在创建使用消息安全的应用程序时可能使用的值。在代码或绑定设置中，可以使用这些值。  
  
|设置|说明|  
|--------|--------|  
|None|允许服务与匿名客户端交互。|  
|Windows|允许在 Windows 凭据的已通过身份验证的上下文中执行 SOAP 消息交换。使用 SSPI 协商机制选择 Kerberos 协议或 NTLM 作为身份验证服务。|  
|Username|允许服务可以要求使用用户名凭据对客户端进行身份验证。请注意，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不允许对用户名进行任何加密操作，例如生成签名或加密数据。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 强制要求在使用用户名凭据时确保传输的安全性。|  
|证书|允许服务要求使用证书对客户端进行身份验证。|  
|[!INCLUDE[infocard](../../../../includes/infocard-md.md)]|允许服务要求使用 [!INCLUDE[infocard](../../../../includes/infocard-md.md)] 对客户端进行身份验证。|  
  
### 凭据编程  
 对于每个客户端凭据类型，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 编程模型都允许通过服务行为和通道行为来指定凭据值和凭据验证程序。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全有两种凭据类型：服务凭据行为和通道凭据行为。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的凭据行为指定实际数据，即用于满足安全要求（通过绑定表示）的凭据。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，客户端类是运行时组件，它在操作调用和消息之间进行转换。所有客户端都是从 <xref:System.ServiceModel.ClientBase%601> 类继承的。通过基类的 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 属性，可以指定不同的客户端凭据值。  
  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，服务行为是一些属性，它们在实现服务协定（接口）的类中应用，以编程方式对服务进行控制。使用 <xref:System.ServiceModel.Description.ServiceCredentials> 类，可以为服务凭据指定证书，也可以为不同的客户端凭据类型指定客户端验证设置。  
  
### 消息安全的协商模型  
 在消息安全模式中，通过执行传输安全，可以在客户端带外配置服务凭据。例如，如果使用的是存储在 Windows 证书存储区中的证书，则必须使用一个工具，如 Microsoft 管理控制台 \(MMC\) 单元。  
  
 在消息安全模式中，通过执行传输安全，还可以与客户端交换服务凭据，作为初始协商的一部分。若要启用协商，请将 <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> 属性设置为 `true`。  
  
## 请参阅  
 [终结点创建概述](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Windows Server App Fabric 的安全模型](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x804)