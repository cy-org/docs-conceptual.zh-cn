---
title: "基于声明的标识模型"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4a96a9af-d980-43be-bf91-341a23401431
caps.latest.revision: 7
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7219e982f755542a35a33dddf74ee24f4b67e8e6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="claims-based-identity-model"></a>基于声明的标识模型
在生成声明感知应用程序时，用户标识在应用程序中表示为一组声明。 其中一个声明可能是用户名，另一个声明可能是电子邮件地址。 其理念是，配置外部标识系统以便为您的应用程序提供所需的一切，是其了解用户及用户发出的每个请求和加密，从而确保您收到的标识数据来自受信任的源。  
  
 在此模型下，可以更轻松地实现单一登录，并且应用程序不再负责执行以下操作：  
  
-   对用户进行身份验证。  
  
-   存储用户帐户和密码。  
  
-   调用企业目录以查找用户标识详细信息。  
  
-   与来自其他平台或公司的标识系统集成。  
  
 在此模型下，应用程序可以基于由已对用户进行身份验证的系统提供的声明做出与标识相关的决定。 这可以是来自简单应用程序个性化的任何内容（带用户的名字），以便为用户授予访问应用程序中更有用的功能和资源的权限。  
  
 本主题提供以下信息：  
  
-   [基于声明的标识简介](../../../docs/framework/security/claims-based-identity-model.md#BKMK_1)  
  
-   [基于声明的标识模型的基本方案](../../../docs/framework/security/claims-based-identity-model.md#BKMK_2)  
  
<a name="BKMK_1"></a>   
## <a name="introduction-to-claims-based-identity"></a>基于声明的标识简介  
 下列术语和概念可帮助您了解标识的此新体系结构。  
  
### <a name="identity"></a>标识  
 为描述 Windows Identity Foundation (WIF) 中的编程模型，将使用术语“标识”来表示一组特性，这些特性描述了系统中要保护的用户或其他实体。  
  
### <a name="claim"></a>声明  
 将声明视为一条标识信息，如“销售”角色中的姓名、电子邮件地址、年龄和成员资格。 应用程序收到的声明越多，您对用户的了解就越深。 可能会想为何将它们称为“声明”，而不是像描述企业目一样称之为“特性”。 原因与传递方法相关。 在此模型中，应用程序不会查找目录中的用户特性。 相反，用户会将声明提供给您的应用程序，然后您的应用程序会对其进行检查。 每个声明均由颁发者做出，您可以像信任颁发者一样信任此声明。 例如，您对由您公司的域控制器做出的声明的信任程度比对用户自身做出的声明的信任程度更高。 WIF 表示具有 <xref:System.Security.Claims.Claim> 类型的声明，此类型拥有一个允许您查明此声明的颁发者的 <xref:System.Security.Claims.Claim.Issuer%2A> 属性。  
  
### <a name="security-token"></a>安全令牌  
 用户会将一组声明随请求一起提供给您的应用程序。 在 Web 服务中，SOAP 信封的安全标头中携带了这些声明。 在基于浏览器的 Web 应用程序中，这些声明会通过来自用户浏览器的 HTTP POST 到达，且稍后可能缓存在 Cookie 中（如果需要会话）。 不管这些声明是如何到达的，都必须对其进行序列化，从而产生安全令牌。 安全令牌是由颁发机构进行数字签名的一组序列化的声明。 签名很重要：它可以为您确保用户不只是构建一组声明并将其发送给您。 在不需要加密的安全性较低的情况下，您可以使用未签名的标记，但本主题中不描述此情况。  
  
 WIF 中的一项核心功能是可以创建和读取安全令牌。 WIF 和 .NET Framework 将处理所有加密工作，并使用可读取的一组声明来呈现您的应用程序。  
  
### <a name="issuing-authority"></a>签发机构  
 有很多不同类型的签发机构，范围从颁发 Kerberos 票证的域控制器到颁发 X.509 证书的证书颁发机构，而本主题中讨论的特定类型的颁发机构可颁发包含声明的安全令牌。 此签发机构是了解如何颁发安全令牌的 Web 应用程序或 Web 服务。 它必须具备了足够的知识才能发出适当的声明（给定发出请求的目标依赖方和用户的情况下），并且可能负责与用户存储进行交互以查找声明并对用户本身进行身份验证。  
  
 无论您选择哪个签发机构，它都会在您的标识解决方案中起到重要作用。 当您通过依赖声明将身份验证分解出应用程序时，您便将责任传递给此机构并要求它代表您对用户进行身份验证。  
  
### <a name="security-token-service-sts"></a>安全令牌服务 (STS)  
 安全令牌服务 (STS) 是根据 WS-Trust 和 WS 联合身份验证协议生成、签名并颁发安全令牌的服务组件。 尽管实现这些协议需要做大量工作，但 WIF 会为您完成所有这些工作，使得协议中的非专业人士只需做极少量的工作即可启动并运行 STS。 可以使用预生成的 STS（如 [Active Directory® 联合身份验证服务 (AD FS) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516)）和云 STS（如 [Microsoft Azure 访问控制服务 (ACS)](http://go.microsoft.com/fwlink/?LinkID=247517)），或者如果要发布自定义标记或提供自定义身份验证或授权，则可使用 WIF 生成自定义 STS。 利用 WIF，您可以轻松生成自己的 STS。  
  
### <a name="relying-party-application"></a>依赖方应用程序  
 在生成依赖声明的应用程序时，您将生成依赖方 (RP) 应用程序。 RP 的同义词包括“声明感知应用程序”和“基于声明的应用程序”。 Web 应用程序和 Web 服务都可以成为 RP。 RP 应用程序使用 STS 颁发的令牌，并从令牌中提取声明以将其用于与标识相关的任务。 WIF 提供可帮助您生成 RP 应用程序的功能。  
  
### <a name="standards"></a>标准  
 为了使所有这些功能能够进行互操作，上一个方案中使用了多个 WS-* 标准。 使用 WS-MetadataExchange 检索策略，并根据 WS-Policy 规范构造策略本身。 STS 公开了实现 WS-Trust 规范的终结点，此规范描述了如何请求和接收安全令牌。 现在，大多数 STS 都颁发使用安全断言标记语言 (SAML) 进行格式化的令牌。 SAML 是行业认可的 XML 词汇表，可用于以可互操作的方式表示声明。 或者，在多平台情况下，这将允许您在完全不同的平台上与 STS 进行通信并跨所有应用程序实现单一登录，不论平台如何。  
  
### <a name="browser-based-applications"></a>基于浏览器的应用程序  
 智能客户端不是可使用基于声明的标识模型的唯一对象。 基于浏览器的应用程序（也称为被动客户端）也可使用该模型。 以下方案描述了其工作原理。  
  
 首先，用户指向声明感知 Web 应用程序（依赖方应用程序）上的浏览器。 Web 应用程序会将该浏览器重定向到 STS，以便能够对用户进行身份验证。 此 STS 承载于一个简单的 Web 应用程序中，此应用程序读取传入请求、使用标准 HTTP 机制对用户进行身份验证，然后创建 SAML 令牌并通过一段 JavaScript 代码进行回复（此代码会使浏览器启动将 SAML 令牌发送回 RP 的 HTTP POST）。 此 POST 的主体包含 RP 请求的声明。 此时，RP 通常会将声明打包到 Cookie 中，这样一来，便无需为每个请求重定向用户。  
  
<a name="BKMK_2"></a>   
## <a name="basic-scenario-for-a-claims-based-identity-model"></a>基于声明的标识模型的基本方案  
 以下是基于声明的系统的示例。  
  
 ![信赖方身份验证流](../../../docs/framework/security/media/conc-relying-partner-processc.png "conc_relying_partner_processc")  
  
 此关系图显示一个已配置为使用 WIF 进行身份验证的网站（依赖方应用程序，RP）、一个客户端和一个要使用该网站的 Web 浏览器。  
  
1.  当未经过身份验证的用户请求页时，其浏览器将重定向到标识提供程序 (IP) 页。  
  
2.  此 IP 要求用户提供其凭据，例如，用户名/密码、Kerberos 等。  
  
3.  IP 会将令牌发送回已返回到浏览器的页。  
  
4.  浏览器现在将重定向回最初请求的页，其中 WIF 将确定此令牌是否满足访问该页的要求。 如果是这样，则会发出一个 cookie 以建立会话，以便只需进行一次身份验证并将控制传递给应用程序。

