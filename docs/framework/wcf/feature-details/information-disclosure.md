---
title: "信息泄露 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4064c89f-afa6-444a-aa7e-807ef072131c
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 信息泄露
信息泄露会使攻击者获得有价值的系统相关信息。因此，应始终考虑到您正在泄露何种信息以及恶意用户是否可能使用这些信息。下面列出了可能的信息泄露攻击并针对每种攻击提供了缓解措施。  
  
## 消息安全性和 HTTP  
 如果正在 HTTP 传输层上使用消息级安全性，请注意消息级安全性不保护 HTTP 头。保护 HTTP 头的唯一方式是使用 HTTPS 传输协议而不是 HTTP 传输协议。HTTPS 传输协议会导致使用安全套接字层 \(SSL\) 协议对整个消息（包括 HTTP 头）进行加密。  
  
## 策略信息  
 保持策略安全是十分重要的，在联合方案中尤其如此 — 在这些方案中，会在策略中公开敏感的已颁发令牌要求或令牌颁发者信息。在这些情况下，建议保护联合服务的策略终结点，以防止攻击者获取服务的有关信息（如要放置在已颁发令牌中的声明的类型）或是将客户端重定向到恶意的令牌颁发者。例如，攻击者可能通过将联合信任链重新配置为终止于执行中间人攻击的颁发者处，来发现用户名\/密码对。此外，还建议通过策略检索来获取绑定的联合客户端验证是否应信任所获得的联合信任链中的颁发者。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]联合方案的更多信息，请参见[联合](../../../../docs/framework/wcf/feature-details/federation.md)。  
  
## 内存转储可能泄露声明信息  
 当应用程序失败时，日志文件（如由 Dr. Watson 生成的那些日志文件）可能包含声明信息。不应该将这些信息导出到其他实体，如支持团队；否则，包含私有数据的声明信息也会导出。通过避免将日志文件发送到未知实体，可以减轻这一问题带来的威胁。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Windows Server 2003](http://go.microsoft.com/fwlink/?LinkId=89160)。  
  
## 终结点地址  
 终结点地址包含与终结点通信所需的信息。SOAP 安全必须在安全协商消息中包含完整地址，这些消息会被交换以便在客户端与服务器之间协商一个对称密钥。因为安全协商是一个引导过程，所以在此过程中无法对地址头进行加密。因此，地址不应包含任何机密数据；否则，会导致信息泄露攻击。  
  
## 未加密传输的证书  
 在使用 X.509 证书对客户端进行身份验证时，该证书会以明文形式在 SOAP 标头内传输。请注意，这可能会泄露个人身份信息 \(PII\)。对于 `TransportWithMessageCredential` 模式而言，这不是问题，因为在该模式中使用传输级安全对整个消息进行加密。  
  
## 服务引用  
 服务引用是对另一个服务的引用。例如，服务可能会在操作过程中将服务引用传递给客户端。服务引用也用于“信任标识验证程序”，该验证程序是一个内部组件，用于在向目标泄露信息（如应用程序数据或凭据）之前确认目标主体的标识。如果远程信任标识无法验证或不正确，则发送方应确保没有泄露任何可能危及自身、应用程序或用户的数据。  
  
 缓解措施包括：  
  
-   假定服务引用是值得信任的。无论何时传输服务引用实例时都应小心处理，以确保它们没有被篡改。  
  
-   某些应用程序可以提供这样一种用户体验，即允许基于服务引用中的数据和经过远程主机证明的信任数据来交互地建立信任。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为这样一种功能提供了扩展点，但用户必须实现这些扩展点。  
  
## NTLM  
 默认情况下，在 Windows 域环境中，Windows 身份验证使用 Kerberos 协议对用户进行身份验证和授权。如果出于某种原因而无法使用 Kerberos 协议，则使用 NT LAN Manager \(NTLM\) 作为后备方式。通过将 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> 属性设置为 `false`，可以禁用此行为。在允许使用 NTLM 时应注意的问题包括：  
  
-   NTLM 会公开客户端用户名。如果用户名需要保密，请将绑定上的 `AllowNTLM` 属性设置为 `false`。  
  
-   NTLM 不提供服务器身份验证。因此，当您使用 NTLM 作为身份验证协议时，客户端无法确保其正在与正确的服务进行通信。  
  
### 指定客户端凭据或无效标识会强制使用 NTLM  
 在创建客户端时，如果指定不带域名的客户端凭据或指定无效的服务器标识，则会导致使用 NTLM 而不是 Kerberos 协议（如果 `AlllowNtlm` 属性设置为 `true`）。因为 NTLM 不进行服务器身份验证，所以信息可能会泄露。  
  
 例如，可能指定不带域名的 Windows 客户端凭据，如下面的 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 代码中所示。  
  
```  
MyChannelFactory.Credentials.Windows.ClientCredential = new System.Net.NetworkCredential("username", "password");  
```  
  
 这段代码未指定域名，因而将使用 NTLM。  
  
 如果指定了域，但使用终结点标识功能指定了无效的服务主体名称，则会使用 NTLM。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何指定终结点标识的更多信息，请参见[服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)。  
  
## 请参阅  
 [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [特权提升](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [拒绝服务](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [篡改](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [不支持的方案](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)   
 [重播攻击](../../../../docs/framework/wcf/feature-details/replay-attacks.md)