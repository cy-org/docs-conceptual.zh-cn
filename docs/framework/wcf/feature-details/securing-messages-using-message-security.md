---
title: "使用消息安全保护消息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a17ebe67-836b-4c52-9a81-2c3d58e225ee
caps.latest.revision: 16
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 16
---
# 使用消息安全保护消息
本主题讨论在使用 <xref:System.ServiceModel.NetMsmqBinding> 时的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息安全。  
  
> [!NOTE]
>  通读本主题之前，建议您先阅读[安全性概念](../../../../docs/framework/wcf/feature-details/security-concepts.md)。  
  
 以下插图提供了使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的排队通信的概念模型。此图及术语用于说明  
  
 传输安全概念。  
  
 ![排队应用程序关系图](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Distributed\-Queue\-Figure")  
  
 使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发送排队消息时，将以消息队列 \(MSMQ\) 消息正文的形式附加 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息。传输安全保护整个 MSMQ 消息，而消息（或 SOAP）安全仅保护 MSMQ 消息正文。  
  
 传输安全用于在客户端保护目标队列的消息，与此不同，消息安全的关键概念在于客户端保护接收应用程序（服务）的消息。这样，在使用消息安全保护 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 时，MSMQ 不起任何作用。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息安全向与现有安全基础结构（如证书或 Kerberos 协议）集成在一起的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息中添加安全标头。  
  
## 消息凭据类型  
 使用消息安全，服务和客户端可以提供相互进行身份验证的凭据。可以通过将 <xref:System.ServiceModel.NetMsmqBinding.Security%2A> 模式设置为 `Message` 或 `Both`（即既使用传输安全又使用消息安全）来选择消息安全。  
  
 该服务可以使用 <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> 属性检查用于对客户端进行身份验证的凭据。这也可用于该服务选择实现的进一步的授权检查。  
  
 本节说明不同的凭据类型以及如何将其用于队列。  
  
### 证书  
 证书凭据类型使用 X.509 证书来标识服务和客户端。  
  
 在典型方案中，由受信任的证书颁发机构向客户端和服务颁发有效证书。然后将建立连接，客户端使用服务的证书对服务有效性进行身份验证，以决定是否可以信任该服务。同样，服务使用客户端的证书来验证客户端是否可信。  
  
 鉴于队列有断开连接的特性，客户端和服务可能不会同时联机。这样，客户端和服务必须在带外交换证书。尤其是，由于客户端在其受信任存储中存有服务的证书（可以将该证书链接到证书颁发机构），因此必须信任将与正确的服务进行通信。至于对客户端进行身份验证，服务使用附有消息的 X.509 证书将该客户端与其存储中的证书进行匹配来验证客户端的真实性。该证书必须再次链接到证书颁发机构。  
  
 在运行 Windows 的计算机上，证书存放在多类存储中。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]不同的存储的更多信息，请参见 [Certificate stores](http://go.microsoft.com/fwlink/?LinkId=87787)（证书存储）。  
  
### Windows  
 Windows 消息凭据类型使用 Kerberos 协议。  
  
 Kerberos 协议是一种安全机制，可用于对域中的用户进行身份验证，并允许通过身份验证的用户与域中的其他实体建立安全上下文。  
  
 将 Kerberos 协议用于排队通信的问题在于包含密钥分发中心 \(KDC\) 所分发客户端标识的票证的生存期相对较短。生存期与指示票证有效性的 Kerberos 票证相关联。这样，鉴于滞后时间较长，您将无法确定令牌对于对客户端进行身份验证的服务仍有效。  
  
 请注意，在使用此凭据类型时，服务必须在 SERVICE 帐户下运行。  
  
 默认情况下，在选择消息凭据时使用 Kerberos 协议。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Exploring Kerberos, the Protocol for Distributed Security in Windows 2000](http://go.microsoft.com/fwlink/?LinkId=87790)（浏览 Windows 2000 中的分布式安全性协议 Kerberos）。  
  
### 用户名密码  
 使用此属性，可以使用消息安全标头中的用户名密码将客户端向服务器进行身份验证。  
  
### IssuedToken  
 客户端可以使用安全令牌服务发出随后可以附加到消息中的令牌，以供服务对客户端进行身份验证。  
  
## 使用传输安全和消息安全  
 在既使用传输安全又使用消息安全时，用于在传输级别和 SOAP 消息级别保护消息的证书必须相同。  
  
## 请参阅  
 [使用传输安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)   
 [基于消息队列的消息安全性](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)   
 [安全性概念](../../../../docs/framework/wcf/feature-details/security-concepts.md)   
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)