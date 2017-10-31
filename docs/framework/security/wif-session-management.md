---
title: "WIF 会话管理"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98bce126-18a9-401b-b20d-67ee462a5f8a
caps.latest.revision: 7
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d71b83231140dcc18e6d2351091fbfd4985e90a2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="wif-session-management"></a>WIF 会话管理
客户端首次尝试访问信赖方托管的受保护资源时，客户端应先向信赖方信任的安全令牌服务 (STS) 验证自身身份。 然后，STS 向客户端颁发安全令牌。 客户端向信赖方出示此令牌，然后信赖方授予客户端访问受保护资源的权限。 但是，不希望客户端针对每个请求重新向 STS 进行身份验证，特别是因为它甚至可能与依赖方不在同一台计算机上或同一个域中。 相反，Windows Identity Foundation (WIF) 中客户端和信赖方建立一个会话，该会话中客户端为首次请求后的所有请求使用会话安全令牌向信赖方验证自身身份。 信赖方可以使用 cookie 中存储的此会话安全令牌重构客户端的 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>。  
  
 STS 定义客户端应提供的身份验证类型。 但是，客户端可能有多个用于向 STS 验证自身身份的凭据。 例如，它可能有来自 Windows Live 的令牌、用户名和密码、证书和智能密钥。 在这种情况下，STS 会向客户端授予多个标识，每个标识对应客户端出示的凭据之一。 信赖方决定授予客户端哪一等级的访问时，可以使用一个或多个此类标识。  
  
 使用 <xref:System.IdentityModel.Tokens.SessionSecurityToken?displayProperty=fullName> 重新构造客户端的 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>其中包含 <xref:System.Security.Claims.ClaimsPrincipal.Identities%2A> 中的所有客户端标识。 集合中的每个 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> 都包含与该标识相关联的启动令牌。  
  
 如果同时颁发新会话令牌和原始会话令牌的会话 ID，<xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler?displayProperty=fullName> 将不会更新令牌缓存中的新会话令牌。 应始终使用唯一的会话 ID 实例化会话令牌。  
  
> [!NOTE]
>  如果 Session.SecurityTokenHandler.ReadToken 收到无效的输入（例如，如果包含会话令牌的 cookie 损坏），会引发 <xref:System.Xml.XmlException> 异常。 我们建议捕捉此异常并提供特定于应用程序的行为。  
  
 如果受保护网页包含大量同样位于受保护域的资源（如小图形），那么客户端必须项信赖方重新验证自身身份以下载这些资源。 使用会话身份验证令牌可避免每次请求都需要向 STS 验证身份的情况，但仍意味着在发送许多 cookie。 你可能希望设置网页以使重要数据和资源存储在受保护的域中，同时次要项存储在不受保护的域中并从主网页创建链接。 此外，将 cookie 路径设置为只引用受保护的域。  
  
 若要在引用模式下操作，Microsoft 建议为“global.asax.cs”文件中的 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SessionSecurityTokenCreated> 事件提供一个处理程序，并在 <xref:System.IdentityModel.Services.SessionSecurityTokenCreatedEventArgs.SessionToken%2A> 属性中传递的令牌上设置“IsReferenceMode”属性。 这些更新将确保会话令牌在每个请求的引用模式下运行，并更倾向于仅在会话身份验证模块上设置 <xref:System.IdentityModel.Services.SessionAuthenticationModule.IsReferenceMode%2A> 属性。  
  
## <a name="extensibility"></a>扩展性  
 可以扩展会话管理机制。 原因之一是可提升性能。 例如，可以创建一个自定义 cookie 处理程序，该处理程序转换或优化内存中状态间的会话安全令牌和进入 cookie 中的内容。 为此，可以配置 <xref:System.IdentityModel.Services.SessionAuthenticationModule?displayProperty=fullName> 的 <xref:System.IdentityModel.Services.SessionAuthenticationModule.CookieHandler%2A?displayProperty=fullName> 属性以使用派生自 <xref:System.IdentityModel.Services.CookieHandler?displayProperty=fullName> 的自定义 cookie 处理程序。 <xref:System.IdentityModel.Services.ChunkedCookieHandler?displayProperty=fullName> 是默认 cookie 处理程序，因为 cookie 超过了超文本传输协议 (HTTP) 允许的大小；如果使用自定义 cookie 处理程序代替，必须进行分块。  
  
 有关更多信息，请参阅 [ClaimsAwareWebFarm](http://go.microsoft.com/fwlink/?LinkID=248408) (http://go.microsoft.com/fwlink/?LinkID=248408) 示例。 此示例演示场就绪会话缓存（相对于 tokenreplycache），以便可以通过引用而非交换大型 cookie 使用会话。此示例还演示保护群集中的 cookie 更简单的方法。 会话缓存基于 WCF。 至于会话保护，该示例演示 WIF 4.5 中基于 MachineKey 的 cookie 转换的新功能，只需在 web.config 中粘贴适当的代码片段即可激活。示例本身并未“场化”，但是它显示应用场就绪需要什么。

