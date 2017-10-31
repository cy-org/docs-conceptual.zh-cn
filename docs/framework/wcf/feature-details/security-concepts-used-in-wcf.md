---
title: "WCF 中使用的安全概念 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b9dfcf5-4bf1-4f35-9070-723171c823a1
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# WCF 中使用的安全概念
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 安全性建立在已在各种安全基础架构中使用并部署的概念之上。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持这些基础结构的其中一些，如 HTTP 上的安全套接字层 \(SSL\) \(HTTPS\)。但是，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现了针对 SOAP 编码消息的更新的可互操作安全标准（如 WS\-Security），因此已不再仅仅是支持现有安全基础结构。无论是使用现有机制还是新的可互操作标准，其背后的安全概念都是相同的。理解现有基础结构以及较新的标准背后的概念对于为应用程序实现最佳安全模型至关重要。  
  
## WCF Web 服务安全简介  
 Microsoft 模式和实践组编写了一本可通过以下链接下载的有关 WCF 安全指南的详细白皮书：[WCF 安全指南](http://go.microsoft.com/fwlink/?LinkId=210210)。该白皮书介绍了与 Web 服务有关的基本安全概念、关键 WCF 安全概念、Intranet 应用程序方案和 Internet 应用程序方案。  
  
## 业界级安全规范  
  
### 公钥基础结构  
 公钥基础结构 \(PKI\) 是一种由数字证书、证书颁发机构以及其他注册机构所组成的系统，它通过使用公钥加密对电子事务中所涉及的各方进行检验和身份验证。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Windows Server 2008 R2 证书服务](http://go.microsoft.com/fwlink/?LinkId=210211).  
  
### Kerberos 协议  
 *Kerberos 协议*是一种规范，用于创建对 Windows 域中的用户进行身份验证的安全机制。它允许用户建立针对域中的其他实体的安全上下文。Windows 2000 及版本更高的平台默认情况下使用 Kerberos 协议。在创建将与 intranet 客户端进行交互的服务时，理解系统的机制非常有用。此外，由于 *Web Services Security Kerberos Binding* 的广泛发布，可以使用 Kerberos 协议与 Internet 客户端通信（即 Kerberos 协议是可互操作的）。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 如何实施 Kerberos协议在 Windows 中，请参阅 [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkId=210212)。  
  
### X.509 证书  
 X.509 证书是安全应用程序中使用的主要凭据形式。有关 X.509 证书的更多信息，请参见 [X.509 公钥证书](http://go.microsoft.com/fwlink/?LinkId=210213)。X.509 证书存储在证书存储区中。运行 Windows 的计算机有多种证书存储区，每一个都针对不同的用途。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 不同存储区的更多信息，请参见 [证书存储区](http://go.microsoft.com/fwlink/?LinkID=87787)。  
  
## Web 服务安全规范  
 系统定义的绑定支持许多常用 Web 服务安全规范。有关系统提供的绑定及其支持的 Web 服务规范的完整列表，请参见：[系统提供的互操作性绑定支持的 Web 服务协议](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)  
  
## 访问控制机制  
 WCF 提供了多种服务或操作的访问控制方式。其中包括：  
  
1.  <xref:System.Security.Permissions.PrinciplePermissionAttribute>  
  
2.  ASP.NET 成员身份提供程序  
  
3.  ASP.NET 角色提供程序  
  
4.  授权管理器  
  
5.  标识模型  
  
 有关这些主题的更多信息，请参见[访问控制机制](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md)。  
  
## 请参阅  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Windows Server App Fabric 的安全模型](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x804)