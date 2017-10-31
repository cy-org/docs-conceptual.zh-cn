---
title: "Windows Identity Foundation 4.5 中的新增功能"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b381f04-593b-471f-bd33-0362be1aade5
caps.latest.revision: 13
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: ddd27a1609ea06bcd333d0a1927d1cd22495744b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="what39s-new-in-windows-identity-foundation-45"></a>Windows Identity Foundation 4.5 中的新增功能
Windows Identity Foundation (WIF) 的首个版本是作为单独的下载文件而发布的，因为在 .NET 3.5 SP1 期间推出，所以称为 WIF 3.5。 从 .NET 4.5 开始，WIF 便成为 .NET Framework 的一部分。 通过使 WIF 类直接在框架中可用，可以在 .NET 中更深度地集成基于声明的标识，从而更轻松地使用声明。 针对 WIF 3.5 而编写的应用程序需要进行修改才能利用新模型；有关信息，请参阅[使用 WIF 3.5 至 WIF 4.5 构建的应用程序的迁移指南](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)。  
  
 在下文中，你可以发现一些突出的主要更改。  
  
## <a name="wif-is-now-part-of-the-net-framework"></a>WIF 现在是 .NET Framework 的一部分  
 WIF 类现在涵盖多个程序集，主要包括 `mscorlib`、`System.IdentityModel`、`System.IdentityModel.Services` 和 `System.ServiceModel`。 同样，WIF 类涵盖多个命名空间：<xref:System.Security.Claims?displayProperty=fullName>、多个 [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004) 命名空间，以及 <xref:System.ServiceModel.Security?displayProperty=fullName>。 <xref:System.Security.Claims?displayProperty=fullName> 命名空间包含新的 <xref:System.Security.Claims.ClaimsPrincipal> 和 <xref:System.Security.Claims.ClaimsIdentity> 类（请参阅下文）。 .NET 中的所有主体现在均派生自 <xref:System.Security.Claims.ClaimsPrincipal>。 有关 WIF 命名空间及其包含的类种类的详细信息，请参阅 [WIF API 参考](../../../docs/framework/security/wif-api-reference.md)。 有关 WIF 3.5 和 WIF 4.5 之间命名空间映射方式的信息，请参阅 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)。  
  
## <a name="new-claims-model-and-principal-object"></a>新声明模型和主体对象  
 声明是 .NET Framework 4.5 的核心所在。 基声明类（<xref:System.Security.Claims.Claim>、<xref:System.Security.Claims.ClaimsIdentity>、<xref:System.Security.Claims.ClaimsPrincipal>、<xref:System.Security.Claims.ClaimTypes> 和 <xref:System.Security.Claims.ClaimValueTypes>）全部直接存在于 `mscorlib` 命名空间的 <xref:System.Security.Claims?displayProperty=fullName> 中。 现在已不再需要使用接口来将声明插入到 .NET 标识系统中：<xref:System.Security.Principal.WindowsPrincipal>、<xref:System.Security.Principal.GenericPrincipal> 和 <xref:System.Web.Security.RolePrincipal> 现在继承自 <xref:System.Security.Claims.ClaimsPrincipal>；而 <xref:System.Security.Principal.WindowsIdentity>、<xref:System.Security.Principal.GenericIdentity> 和 <xref:System.Web.Security.FormsIdentity> 现在继承自 <xref:System.Security.Claims.ClaimsIdentity>。 简言之，每个主体类现在都服务于声明。 因此，WIF 3.5 集成类和接口（`WindowsClaimsIdentity`、`WindowsClaimsPrincipal`、`IClaimsPrincipal`、`IClaimsIdentity`）现在已被移除。 此外，<xref:System.Security.Claims.ClaimsIdentity> 类现在已将方法公开，以便更轻松地查询标识的声明集合。  
  
## <a name="changes-to-the-wif-45-visual-studio-experience"></a>WIF 4.5 Visual Studio 体验方面的更改  
  
-   **添加 STS 引用…** Visual Studio 功能（命令行实用工具 FedUtil）已不存在；现在，可以使用新的 Visual Studio 扩展：用于 Visual Studio 2012 标识和访问工具。 这可以让你与现有 STS 联合，或使用 LocalSTS 来测试你的解决方案。 在安装此扩展后，你可以右击项目并在上下文菜单中查找“标识和访问”。  
  
-   ASP.NET 和 STS 模板不再作为声明提供，可以直接在 ASP.NET、网站和 WCF 的现有项目模板中使用。  
  
-   `Microsoft.IdentityModel.Web.Controls` 命名空间中的控件（`SignInControl`、`FederatedPassiveSignInControl` 和 `FederatedPassiveSignInStatus`）不会转入到 WIF 4.5 中。  
  
## <a name="changes-to-the-wif-45-api"></a>WIF 4.5 API 的更改  
  
-   通常，与声明相关的类位于 <xref:System.Security.Claims?displayProperty=fullName> 命名空间中；与 WCF 相关的类（服务协定、通道、通道工厂以及用于 WS-Trust 方案的服务主机）位于 <xref:System.ServiceModel.Security?displayProperty=fullName> 中；而所有其他 WIF 类分布于各个 [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004) 命名空间，其中包括表示 WS-* 和 SAML 项目的类、令牌处理程序和相关类，以及用于 WS 联合身份验证方案的类。 有关更多信息，请参阅 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)和 [WIF API 参考](../../../docs/framework/security/wif-api-reference.md)。  
  
-   已启用计算机密钥，以便用于 Web 场方案的会话 Cookie。 有关更多信息，请参阅 [WIF 和 Web 场](../../../docs/framework/security/wif-and-web-farms.md)。  
  
-   现在可以以声明的方式在 [\<system.identityModel>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 和 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 元素下配置 WIF。 有关 WIF 配置的详细信息，请参阅 [WIF 配置参考](../../../docs/framework/security/wif-configuration-reference.md)。  
  
## <a name="other-notable-net-changes-or-features-that-are-caused-by-the-integration-of-wif-into-net"></a>其他由于 WIF 集成到 .NET 而引起的重要更改或功能  
  
-   现在，执行基于声明的授权 (CBAC) 这种可能性是 .NET Framework 的必要组成部分。 你可以配置 <xref:System.Security.Claims.ClaimsAuthorizationManager> 对象，然后使用 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> 和 <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> 类在你的代码中执行命令式和声明式访问检查。 与传统基于角色的访问检查 (RBAC) 相比，CBAC 可提供更大的灵活性和精细度。 它还允许将授权策略与业务逻辑进行更大程度的分离，因为业务逻辑可以使访问检查基于特定的声明或声明组，而这些声明的授权策略可以在 [\<claimsAuthorizationManager>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md) 元素下以声明方式进行配置。  
  
## <a name="wcf-changes-as-a-result-of-wif-integration"></a>因 WIF 集成而导致的 WCF 更改：  
  
-   WCF 基于声明的标识模型已被 WIF 取代。 这意味着应放弃 <xref:System.IdentityModel.Claims?displayProperty=fullName>、<xref:System.IdentityModel.Policy?displayProperty=fullName> 和 <xref:System.IdentityModel.Selectors?displayProperty=fullName> 命名空间中的类，以便使用 WIF 类。  
  
-   现在，通过指定 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>` 元素上的 `useIdentityConfiguration` 特性，可以在 WCF 服务上启用 WIF，如下列 XML 中所示：  
  
    ```xml  
    <serviceCredentials useIdentityConfiguration="true">  
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->  
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />  
    </serviceCredentials>  
    ```  
  
     使用用于 Visual Studio 2012 标识和访问工具时（请参阅上文 Visual Studio 体验方面的更改），此工具会添加一个 `<serviceCredentials>` 元素，该元素具有 `useIdentityConfiguration` 特性，并且此特性设置为你的配置文件。 它还会添加一个包含 WIF 配置设置的对应 [\<system.identityModel>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 元素，并添加一个绑定以及其他必要的设置，以便将身份验证外包给你所选择的 STS。  
  
## <a name="see-also"></a>另请参阅  
 [使用 WIF 3.5 至 WIF 4.5 生成的应用程序的迁移指南](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)   
 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)   
 [WIF API 参考](../../../docs/framework/security/wif-api-reference.md)   
 [WIF 配置参考](../../../docs/framework/security/wif-configuration-reference.md)

