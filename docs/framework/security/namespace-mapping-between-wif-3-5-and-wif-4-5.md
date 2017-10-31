---
title: "WIF 3.5 和 WIF 4.5 之间的命名空间映射"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a092d98c-444d-4336-a644-63c2e11e96c8
caps.latest.revision: 4
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9c3d726ee5b6da733ddaa79ec23943bb6faa43e5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="namespace-mapping-between-wif-35-and-wif-45"></a>WIF 3.5 和 WIF 4.5 之间的命名空间映射
从 .NET 4.5 开始，Windows Identity Foundation (WIF) 已完全集成到 .NET Framework 中。 这种集成引起了名称更改及 WIF 命名空间和 API 表面的某些合并。 本主题提供一些指导以及 WIF 3.5 命名空间和 WIF 4.5 命名空间之间的常规映射。 它的目的并不是提供详尽的说明，而是提供一些常规信息，说明在 WIF 4.5 中的什么位置可以找到熟悉的 WIF 3.5 类。 有关 WIF 3.5 和 WIF 4.5 之间差异的更多详细信息，请参阅 [Windows Identity Foundation 4.5 中的新增功能](../../../docs/framework/security/whats-new-in-wif.md)。 有关如何将使用 WIF 3.5 生成的应用程序迁移到 WIF 4.5 的指南，请参阅[将使用 WIF 3.5 生成的应用程序迁移到 WIF 4.5 的指南](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)。  
  
## <a name="wif-35-to-wif-45-namespace-map"></a>WIF 3.5 至 WIF 4.5 命名空间映射  
 在 WIF 3.5 中的 `Microsoft.IdentityModel` 命名空间下收集的 WIF 类现分布在 WIF 4.5 中的以下命名空间中：`System.Security.Claims`、`System.ServiceModel.Security` 和 `System.IdentityModel`。 此外，WIF 4.5 中已合并或完全删除了某些 WIF 3.5 命名空间。  
  
> [!IMPORTANT]
>  以下 `System.IdentityModel` 命名空间包含实现 WCF 基于声明的标识模型的类：<xref:System.IdentityModel.Claims?displayProperty=fullName>、<xref:System.IdentityModel.Policy?displayProperty=fullName> 和 <xref:System.IdentityModel.Selectors?displayProperty=fullName>。 WCF 基于声明的标识模型已被 WIF 取代。 在基于 WIF 生成解决方案时，不应该使用这三个命名空间中的类。  
  
 下表提供有关在 WIF 4.5 中的什么位置可找到 WIF 3.5 类的信息。  
  
|**WIF 3.5 命名空间**|**WIF 4.5 命名空间**|**注释**|  
|-|-|-|  
|`Microsoft.IdentityModel`|<xref:System.IdentityModel?displayProperty=fullName>|- 未实现大部分表示常数的类。<br />- 用于生成安全令牌服务的类已从 `Microsoft.IdentityModel.SecurityTokenService` 移到 <xref:System.IdentityModel?displayProperty=fullName>。<br />- `Microsoft.IdentityModel.Threading` 中的类已移到 <xref:System.IdentityModel?displayProperty=fullName>。<br />- 未实现 `ExceptionMapper` 类和 `MruSecurityTokenCache` 类。|  
|`Microsoft.IdentityModel.Claims`|<xref:System.Security.Claims?displayProperty=fullName>|- 在 WIF 4.5 中未实现 `IClaimsPrincipal` 和 `IClaimsIdentity` 接口。 相反，<xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName> 和 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> 现在是基类，从中派生了大多数 .NET 主体和标识类。 这意味着在 WIF 4.5 中无需 `Microsoft.IdentityModel.Claims.WindowsClaimsPrincipal` 和 `Microsoft.IdentityModel.Claims.WindowsClaimsIdentity` 等专用声明主体和标识类，而是使用 <xref:System.Security.Principal.WindowsPrincipal?displayProperty=fullName> 和 <xref:System.Security.Principal.WindowsIdentity?displayProperty=fullName>。 同样适用于其他针对 WIF 3.5 中存在的其他专用声明主体和标识类。<br />- 在 WIF 4.5 中未实现 `Microsoft.IdentityModel.Claims.ClaimsCollection` 类。 相反，将集合声明作为 <xref:System.Security.Claims.Claim?displayProperty=fullName> 类型的可枚举集合公开。<br />-   <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName> 和 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> 提供现完全支持 LINQ 的方法。|  
|`Microsoft.IdentityModel.Configuration`|<xref:System.IdentityModel.Configuration?displayProperty=fullName>|在 WIF 4.5 中，某些元素和类发生了名称变化，还有一些已被删除；例如 `Microsoft.IdentityModel.Configuraiton.ServiceConfiguration` 现在是 <xref:System.IdentityModel.Configuration.IdentityConfiguration?displayProperty=fullName>。|  
|`Microsoft.IdentityModel.Protocols`|<xref:System.IdentityModel.Services?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Protocols.WSFederation`|<xref:System.IdentityModel.Services?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Protocols.WSFederation.Metadata`|<xref:System.IdentityModel.Metadata?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Protocols.WSIdentity`|在 WIF 4.5 中未实现|WIF 3.5 中包含支持 CardSpace 的类，在 WIF 4.5 中未实现。|  
|`Microsoft.IdentityModel.Protocols.WSTrust`|在 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> 和 <xref:System.ServiceModel.Security?displayProperty=fullName> 命名空间之间拆分。|表示 WS-Trust 项目的类位于 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> 命名空间中，例如 <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken> 类。 代表 WCF 服务协定的类、服务主机、允许 WCF 服务使用 WS-Trust 协议进行通信的通道位于 <xref:System.ServiceModel.Security?displayProperty=fullName> 命名空间中；例如，<xref:System.ServiceModel.Security.WSTrustServiceHost> 类。|  
|`Microsoft.IdentityModel.Protocols.WSTrust.Bindings`|在 WIF 4.5 中未实现|-|  
|`Microsoft.IdentityModel.Protocols.XmlEncryption`|在 WIF 4.5 中未实现|包含在 WIF 3.5 中表示 XML 加密常数的类。 WIF 4.5 中未实现这些常数。|  
|`Microsoft.IdentityModel.Protocols.XmlSignature`|<xref:System.IdentityModel?displayProperty=fullName>|未实现 `EnvelopingSignature` 类和代表常数的类。|  
|`Microsoft.IdentityModel.SecurityTokenService`|在 <xref:System.IdentityModel?displayProperty=fullName>、<xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> 和 <xref:System.IdentityModel.Tokens?displayProperty=fullName> 命名空间之间拆分。|-|  
|`Microsoft.IdentityModel.Threading`|<xref:System.IdentityModel?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Tokens`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Tokens.Saml11`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Tokens.Saml2`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Web`|<xref:System.IdentityModel.Services?displayProperty=fullName>|-|  
|`Microsoft.IdentityModel.Web.Configuration`|<xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>|大部分为被动（WS 联合身份验证）方案提供配置的类已移动到 <xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>；然而，其中某些还位于 <xref:System.IdentityModel.Services?displayProperty=fullName>.中。|  
|`Microsoft.IdentityModel.Web.Controls`|在 WIF 4.5 中未实现|`Microsoft.IdentityModel.Web.Controls` 中的类实现了联合被动登录控制，在 WIF 4.5 中不存在这种控制。|  
|`Microsoft.IdentityModel.WindowsTokenService`|在 WIF 4.5 中未实现|-|  
  
## <a name="see-also"></a>另请参阅  
 [Windows Identity Foundation 4.5 中的新增功能](../../../docs/framework/security/whats-new-in-wif.md)   
 [使用 WIF 3.5 至 WIF 4.5 生成的应用程序的迁移指南](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)

