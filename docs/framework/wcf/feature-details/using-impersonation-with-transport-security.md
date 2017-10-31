---
title: "将模拟用于传输安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 426df8cb-6337-4262-b2c0-b96c2edf21a9
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# 将模拟用于传输安全
模拟是服务器应用程序呈现客户端标识的能力。服务在验证对资源的访问时常常使用模拟。服务器应用程序使用服务帐户运行，但当服务器接受客户端连接时，它模拟客户端，以便使用客户端凭据执行访问检查。传输安全是一种传递凭据和使用这些凭据确保通信安全的机制。本主题介绍如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中将模拟功能用于传输安全。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]用于消息安全的模拟的更多信息，请参见[委托和模拟](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)。  
  
## 五个模拟级别  
 传输安全使用五级模拟，如下表所述。  
  
|模拟级别|说明|  
|----------|--------|  
|无|服务器应用程序不尝试模拟客户端。|  
|Anonymous|服务器应用程序可以对照客户端凭据执行访问检查，但不接收有关客户端标识的任何信息。此模拟级别仅对计算机上的通信（例如命名管道）有意义。将 `Anonymous` 用于远程连接会将模拟级别提高到 Identify。|  
|Identify|服务器应用程序知道客户端的标识，并且可以对照客户端凭据执行访问验证，但不能模拟客户端。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，Identify 是用于 SSPI 凭据的默认模拟级别，除非令牌提供程序提供其他模拟级别。|  
|Impersonate|服务器应用程序除了执行访问检查以外，还可以像客户端一样访问服务器计算机上的资源。服务器应用程序不能使用客户端标识访问远程计算机上的资源，这是因为模拟的令牌没有网络凭据|  
|Delegate|Delegate 模拟级别具有 `Impersonate` 的功能，此外，服务器应用程序通过该模拟级别，还可以使用客户端标识访问远程计算机上的资源，并可将标识传递给其他应用程序。<br /><br /> **重要事项** 服务器域帐户必须标记为受信任，域控制器上的委托才能使用这些附加功能。模拟级别不能用于标记为敏感的客户端域帐户。|  
  
 最常用于传输安全的级别是 `Identify` 和 `Impersonate`。在典型用法中，不建议使用 `None` 和 `Anonymous` 级别，许多传输协议不支持在身份验证中使用这些级别。`Delegate` 级别功能强大，应谨慎使用。只应向受信任的服务器应用程序授予委托凭据的权限。  
  
 若要使用 `Impersonate` 或 `Delegate` 级别的模拟，服务器应用程序需要具有 `SeImpersonatePrivilege` 权限。如果在 Administrators 组中的帐户下运行，或在具有服务 SID（网络服务、本地服务或本地系统）的帐户下运行，则默认情况下，应用程序具有此权限。模拟不要求客户端和服务器相互进行身份验证。某些支持模拟的身份验证方案（例如 NTLM）不能用于相互身份验证。  
  
## 特定于传输协议的模拟问题  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中选择的传输协议会影响可选的模拟。本节介绍在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中影响标准 HTTP 和命名管道传输协议的一些问题。自定义传输协议在对模拟的支持上有自己的限制。  
  
### 命名管道传输协议  
 使用命名管道传输协议时，请注意以下事项：  
  
-   命名管道传输协议应仅用在本地计算机上。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的命名管道传输协议显式禁止跨计算机连接。  
  
-   命名管道不能用在 `Impersonate` 或 `Delegate` 模拟级别上。命名管道不能在这些模拟级别实施计算机上的保证。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]命名管道的更多信息，请参见[选择传输方式](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)。  
  
### HTTP 传输协议  
 使用 HTTP 传输协议（<xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.BasicHttpBinding>）的绑定支持多种身份验证方案，如[了解 HTTP 身份验证](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)中所述。支持的模拟级别取决于身份验证方案。使用 HTTP 传输协议时，请注意以下事项：  
  
-   `Anonymous` 身份验证方案忽略模拟。  
  
-   `Basic` 身份验证方案仅支持 `Delegate` 级别。所有低于此级别的模拟级别都会升级。  
  
-   `Digest` 身份验证方案仅支持 `Impersonate` 和 `Delegate` 级别。  
  
-   `NTLM` 身份验证方案（可直接选择或通过协商选择）仅在本地计算机上支持 `Delegate` 级别。  
  
-   Kerberos 身份验证方案（只能通过协商选择）可用于任何受支持的模拟级别。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] HTTP 传输协议的更多消息，请参见[选择传输方式](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)。  
  
## 请参阅  
 [委托和模拟](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)   
 [授权](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [如何：在服务上模拟客户端](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)   
 [了解 HTTP 身份验证](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)