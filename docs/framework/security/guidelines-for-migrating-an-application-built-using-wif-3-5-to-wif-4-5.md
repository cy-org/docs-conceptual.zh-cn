---
title: "使用 WIF 3.5 至 WIF 4.5 构建的应用程序迁移指南"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7a32fe6e-5f68-4693-9371-19411fa8063c
caps.latest.revision: 12
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 151a46a1d0f5ae5ae58508bdb3cab5bbb86f07ef
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="guidelines-for-migrating-an-application-built-using-wif-35-to-wif-45"></a>使用 WIF 3.5 至 WIF 4.5 构建的应用程序迁移指南
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF) 3.5 和 4.5。  
  
## <a name="overview"></a>概述  
 Windows Identity Foundation (WIF) 最初发布于 .NET 3.5 SP1 的使用阶段。 那个版本的 WIF 称为 WIF 3.5。 它作为单独的运行时和 SDK 发布，这意味着启用 WIF 的应用程序在其上运行的每台计算机需要安装有 WIF 运行时，并且开发人员需要下载并安装 WIF SDK 以获取用于支持开发启用 WIF 的应用程序的 Visual Studio 模板和工具。 从 .NET 4.5 开始，WIF 已完全集成到 .NET Framework 中。 因此不再需要单独的运行时，并且可以使用 Visual Studio 扩展管理器在 Visual Studio 2012 中安装 WIF 工具。 此版本的 WIF 称为 WIF 4.5。  
  
 WIF 到 .NET 的集成需要对 WIF API 图面做出一些更改。 WIF 4.5 包括新的命名空间、配置元素的一些更改以及适用于 Visual Studio 的新工具。 本主题提供可用于帮助将使用 WIF 3.5 生成的应用程序迁移到 WIF 4.5 的指南。 在某些情况下，可能需要在运行 Windows 8 或 Windows Server 2012 的计算机上运行使用 WIF 3.5 生成的旧版应用程序。 本主题也提供有关如何为这些操作系统启用 WIF 3.5 的指南。  
  
## <a name="changes-required-for-wif-45"></a>针对 WIF 4.5 所需的更改  
 本部分介绍将 WIF 3.5 应用程序迁移到 WIF 4.5 所需进行的更改。  
  
### <a name="assembly-and-namespace-changes"></a>程序集和命名空间更改  
 在 WIF 3.5 中，所有的 WIF 类都包含在 `Microsoft.IdentityModel` 程序集 (microsoft.identitymicrosoft.identitymodel.dll) 中。 在 WIF 4.5 中，已将 WIF 类拆分在以下程序集中：`mscorlib` (mscorlib.dll)、`System.IdentityModel` (System.IdentityModel.dll)、`System.IdentityModel.Services` (System.IdentityModel.Services.dll) 和 `System.ServiceModel` (System.ServiceModel.dll)。  
  
 WIF 3.5 类都包含在其中一个 `Microsoft.IdentityModel` 命名空间中；例如，`Microsoft.IdentityModel`、`Microsoft.IdentityModel.Tokens` 和 `Microsoft.IdentityModel.Web` 等。 在 WIF 4.5 中，WIF 类现已分布在 [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004) 命名空间、<xref:System.Security.Claims?displayProperty=fullName> 命名空间和 <xref:System.ServiceModel.Security?displayProperty=fullName> 命名空间中。 除此重组外，一些 WIF 3.5 类已被放置在 WIF 4.5 中。  
  
 下表显示了一些更重要的 WIF 4.5 命名空间以及它们所包含的类的类型。 有关命名空间在 WIF 3.5 和 WIF 4.5 之间的映射关系以及有关已被放置在 WIF 4.5 中的命名空间和类的详细信息，请参阅 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)。  
  
|WIF 4.5 命名空间|描述|  
|-----------------------|-----------------|  
|<xref:System.IdentityModel?displayProperty=fullName>|包含表示 cookie 转换、安全令牌服务和专业 XML 字典读取器的类。 包含来自以下 WIF 3.5 命名空间的类：`Microsoft.IdentityModel`、`Microsoft.IdentityModel.SecurityTokenService` 和 `Microsoft.IdentityModel.Threading`。|  
|<xref:System.Security.Claims?displayProperty=fullName>|包含表示声明、基于声明的标识、基于声明的主体和其他基于声明的标识模型项目的类。 包含来自 `Microsoft.IdentityModel.Claims` 命名空间的类。|  
|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|包含表示安全令牌、安全令牌处理程序和其他安全令牌项目的类。 包含来自以下 WIF 3.5 命名空间的类：`Microsoft.IdentityModel.Tokens`、`Microsoft.IdentityModel.Tokens.Saml11` 和 `Microsoft.IdentityModel.Tokens.Saml2`。|  
|<xref:System.IdentityModel.Services?displayProperty=fullName>|包含被动（WS 联合身份验证）方案中使用的类。 包含来自 `Microsoft.IdentityModel.Web` 命名空间的类。|  
|<xref:System.ServiceModel.Security?displayProperty=fullName>|表示 WCF 协定、通道、服务主机和主动 (WS-Trust) 方案中使用的其他项目的类现在都在此命名空间中。 在 WIF 3.5 中，这些类位于 `Microsoft.IdentityModel.Protocols.WSTrust` 命名空间中。|  
  
> [!IMPORTANT]
>  以下 `System.IdentityModel` 命名空间包含实现 WCF 基于声明的标识模型的类：<xref:System.IdentityModel.Claims?displayProperty=fullName>、<xref:System.IdentityModel.Policy?displayProperty=fullName> 和 <xref:System.IdentityModel.Selectors?displayProperty=fullName>。 WCF 基于声明的标识模型已被 WIF 取代。 在基于 WIF 生成解决方案时，不应该使用这三个命名空间中的类。  
  
### <a name="changes-due-to-net-integration"></a>因 .NET 集成而进行的更改  
 WIF 现已集成到 .NET Framework 中。 大多数 .NET 标识和主体类现在都派生自 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> 和 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>。 在 WIF 4.5 中进行了以下更改：  
  
-   表示声明、标识和主体的 WIF 类现存在于 <xref:System.Security.Claims?displayProperty=fullName> 命名空间中。  
  
    > [!IMPORTANT]
    >  <xref:System.IdentityModel.Claims?displayProperty=fullName> 命名空间包含表示 WCF 基于声明的标识模型中的项目的类。 许多这些类拥有与 WIF 类相同的名称，如 `Claims`。 在基于 WIF 生成解决方案时，请不要使用这些类。  
  
-   .NET 标识和主体类现在直接派生自 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> 和 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>，表示基于声明的标识和主体。 因此，不再需要 WIF 3.5 接口 `IClaimsIdentity` 和 `IClaimsPrincipal`，并且 WIF 4.5 中也不再支持这两个接口。  
  
-   因为 .NET 标识和主体类（如 <xref:System.Security.Principal.WindowsIdentity?displayProperty=fullName> 和 <xref:System.Security.Principal.WindowsPrincipal?displayProperty=fullName>）现在派生自 <xref:System.Security.Claims.ClaimsIdentity> 和 <xref:System.Security.Claims.ClaimsPrincipal>，所以它们内置有声明功能。 因此，不再需要之前存在于 WIF 3.5 中特定于声明的标识和主体类（如 `WindowsClaimsIdentity` 和 `WindowsClaimsPrincipal`），并且它们也不存在于 WIF 4.5 中。  
  
### <a name="other-changes-to-wif-functionality"></a>对 WIF 功能的其他更改  
 除命名空间更改和由于与 .NET 集成而进行的更改之外，还在 WIF 4.5 中进行了以下 WIF 功能的常规更改。  
  
-   删除了 `Microsoft.IdentityModel.ExceptionMapper` 类，它提供使你能够将异常映射到特定 SOAP 错误的功能。  
  
-   大幅度地减少了异常图面。  
  
-   删除了许多定义协议或特定于 WS-* 的常数的类，例如 `Microsoft.IdentityModel.WSAddressing10Constants` 类，它定义与 WS-Addressing 1.0 相关的常数的。  
  
-   删除了 `Microsoft.IdentityModel.WindowsTokenService` 命名空间中的声明为 Windows 令牌服务 (c2wts) 以及其关联的类。  
  
### <a name="wif-configuration-changes"></a>WIF 配置更改  
 配置文件中的许多更改是由 WIF 4.5 中的命名空间更新所造成的。 例如，以 `<httpModules>` 部分中的以下 WIF 3.5 条目为例，将 WS 联合身份验证管理器添加到应用程序：  
  
```xml  
<add name="WSFederationAuthenticationModule" type="Microsoft.IdentityModel.Web.WSFederationAuthenticationModule, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=abcd … 5678" />  
```  
  
 WIF 4.5 中更新了此条目来包括新的命名空间和程序集版本：  
  
```xml  
<add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcd … 5678"/>  
```  
  
 以下列表枚举了针对 WIF 4.5 的配置文件进行的主要更改。  
  
-   `<microsoft.identityModel>` 部分现在为 [\<system.identityModel>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 部分。  
  
-   `<service>` 元素现在为 [\<identityConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 元素。  
  
-   已将新的部分 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 添加到在被动（WS 联合身份验证）方案中控制行为的特定设置。  
  
-   已将 [\<federationConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 元素及其子元素从 WIF 3.5 中的 `<service>` 元素移动到新的 `<system.identityModel.services>` 元素。  
  
-   可以直接在 WIF 3.5 中的 `<service>` 元素下在服务级别处指定的多个元素已被限制为在 [\<securityTokenHandlerConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) 元素下指定。 （出于后向兼容性目的，仍可以在 WIF 4.5 中的 [\<identityConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 元素下指定它们。）  
  
 有关 WIF 4.5 配置元素的完整列表，请参阅 [WIF 配置架构](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/index.md)。  
  
### <a name="visual-studio-tooling-changes"></a>Visual Studio 工具更改  
 WIF 3.5 SDK 提供独立的 Federation Utility (FedUtil.exe (FedUtil))，用于将启用 WIF 的应用程序中的标识管理外包给安全令牌服务 (STS)。 此工具将 WIF 设置添加到应用程序配置文件，使应用程序能够从一个或多个 STS 获取安全令牌，并通过“添加 STS 服务引用”按钮出现在 Visual Studio 中。 FedUtil 不随附 WIF 4.5。 相反，WIF 4.5 支持名为用于 Visual Studio 2012 的标识和访问工具的新 Visual Studio 扩展，可用于通过将标识管理外包给 STS 所需的 WIF 设置修改应用程序的配置文件。 标识和访问工具也实现了名为本地 STS 的 STS，可用于测试启用 WIF 的应用程序。 在许多情况下，使用此功能便无需生成自定义 STS，通常需要在 WIF 3.5 中生成此 STS 以测试正在开发的解决方案。 因此，Visual Studio 2012 中不再支持此类 STS 模板；然而，支持 STS 开发的类仍然在 WIF 4.5 中可用。  
  
 可以从 Visual Studio 中的扩展和更新管理器安装标识和访问工具，或者从代码库中的以下页面进行下载：[代码库上用于 Visual Studio 2012 的标识和访问工具](http://go.microsoft.com/fwlink/?LinkID=245849)。 下表中汇总了 Visual Studio 工具更改：  
  
-   删除了“添加 STS 服务引用”功能。 替换为了标识和访问工具。  
  
-   删除了 Visual Studio STS 模板。 可以使用通过标识和访问工具所提供的本地 STS 来测试使用 WIF 开发的标识解决方案。 可以修改本地 STS 配置以自定义其服务的声明。  
  
-   WIF 4.5 中不提供独立的 Federation Utility (FedUtil)。 可以使用标识和访问工具修改配置文件，以将标识管理外包给 STS。  
  
 有关标识和访问工具的详细信息，请参阅[用于 Visual Studio 2012 的标识和访问工具](../../../docs/framework/security/identity-and-access-tool-for-vs.md)  
  
<a name="BKMK_ToolingChanges"></a>   
### <a name="passive-ws-federation-scenarios"></a>被动（WS 联合身份验证）方案：  
  
-   已将支持被动方案的类移动到 <xref:System.IdentityModel.Services?displayProperty=fullName> 命名空间中。 在 WIF 3.5 中，这些类位于 `Microsoft.IdentityModel.Web` 命名空间中。  
  
-   已将 `Microsoft.IdentityModel.Web.Configuration` 命名空间中的类移动到 <xref:System.IdentityModel.Services.Configuration?displayProperty=fullName> 中。 这些类表示被动方案中特定于配置的对象。  
  
-   不再支持 `FederatedPasssiveSignInControl`；在 WIF 4.5 中删除了 `Microsoft.IdentityModel.Web.Controls` 命名空间中的所有类。  
  
-   WS 联合身份验证模块 (<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>) 注销功能与 WIF 3.5 中的不同。 有关 WIF 4.5 中注销工作原理的详细信息，请参阅 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 类主题。  
  
### <a name="active-wcfws-trust-scenarios"></a>主动 (WCF/WS-Trust) 方案：  
  
-   在 WIF 4.5 中，`Microsoft.IdentityModel.Protocols.WSTrust` 命名空间主要被拆分为两个命名空间。 表示特定于 WS-Trust 协议的项目的类现位于 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> 中。 这包括如 <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken> 等类。 已将表示在 WCF 应用程序中使用 WS-Trust 所涉及的服务协定、通道、服务主机和其他项目的类移动到 <xref:System.ServiceModel.Security?displayProperty=fullName> 中，例如 <xref:System.ServiceModel.Security.IWSTrust13AsyncContract> 接口。  
  
-   极大地简化了为使用 WIF 而对 WCF 应用程序进行的配置。 之前必须将 `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` 添加为行为扩展，随后使用此功能通过指定 `<federatedServiceHostConfiguration>` 元素将 WIF 楔入服务行为。 WIF 4.5 已更紧密地与 WCF 集成。 现在，通过在 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>` 元素上指定 `useIdentityConfiguration` 特性可以在 WCF 服务上启用 WIF，如下列 XML 中所示：  
  
    ```xml  
    <serviceCredentials useIdentityConfiguration="true">  
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->  
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />  
    </serviceCredentials>  
    ```  
  
-   在 WIF 4.5 中，必须在服务主机上指定由主动 (WCF) 服务使用的服务证书。 在配置中，可以通过 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>`/`<serviceCertificate>` 元素来执行此操作，如之前的示例所示。 在 WIF 3.5 中，可以通过 WIF `<service>` 元素的 `<serviceCertificate>` 子元素指定服务证书。 WIF 4.5 中不存在此功能；请改为在 `<serviceCredentials>` 元素下指定 `<serviceCertificate>` 元素。  
  
-   用于将 WIF 3.5 楔入 WCF 的类不再存在。 这包括 `Microsoft.IdentityModel.Tokens` 命名空间中的以下类：`FederatedSecurityTokenManager`、`FederatedServiceCredentials`、`IdentityModelServiceAuthorizationManager` 和 `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` 类。  
  
## <a name="enabling-wif-35-in-windows-8"></a>在 Windows 8 中启用 WIF 3.5  
 由于 WIF 4.5 是 .NET 4.5 的一部分，所以它在运行 Windows 8 和 Windows Server 2012 的计算机上自动启用，并且使用 WIF 4.5 生成的应用程序将默认在 Windows 8 和 Windows Server 2012 下运行。 然而，你可能需要在运行 Windows 8 或 Windows Server 2012 的计算机上运行使用 WIF 3.5 生成的应用程序。 在此情况下，需要在目标计算机上启用 WIF 3.5。 在运行 Windows 8 的计算机上，可以使用部署映像服务和管理 (DISM) 工具来实现这点。 在运行 Windows Server 2012 的计算机上，可以使用 DISM 工具，或使用 Windows PowerShell `Add-WindowsFeature` cmdlet。 在这两种情况下，可以在命令行或从 Windows PowerShell 环境内部调用适当的命令。  
  
 以下命令将演示如何从命令行或 Windows PowerShell 环境内部使用 DISM 工具。 默认情况下，DISM PowerShell 模块包含在 Windows 8 和 Windows Server 2012 中，无需进行导入操作。 有关将 DISM 用于 Windows PowerShell 的详细信息，请参阅[如何在 Windows PowerShell 中使用 DISM](http://go.microsoft.com/fwlink/?LinkId=254419)。  
  
 使用 DISM 启用 WIF 3.5：  
  
```  
dism /online /enable-feature:windows-identity-foundation  
```  
  
 使用 DISM 禁用 WIF 3.5：  
  
```  
dism /online /disable-feature:windows-identity-foundation  
```  
  
 检查已使用 DISM 启用或禁用的功能：  
  
```  
dism /online /get-features  
```  
  
 或者，在运行 Windows Server 2012 的计算机上，可以使用 Windows PowerShell `Add-WindowsFeature` cmdlet 来启用 WIF 3.5。 若要通过命令行执行此操作，可以输入以下命令：  
  
```  
powershell "add-windowsfeature windows-identity-foundation"  
```  
  
 从 Windows PowerShell 环境内部可以直接输入命令：  
  
```  
add-windowsfeature windows-identity-foundation  
```  
  
> [!NOTE]
>  由于 WIF 3.5 和 WIF 4.5 中有许多类共享相同的名称，所以在同时使用 WIF 3.5 和 WIF 4.5 时，请确保使用完全限定的类名或使用命名空间别名，以区分 WIF 3.5 和 WIF 4.5 中的类。  
  
## <a name="see-also"></a>另请参阅  
 [WIF 配置架构](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/index.md)   
 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)   
 [Windows Identity Foundation 4.5 中的新增功能](../../../docs/framework/security/whats-new-in-wif.md)   
 [Identity and Access Tool for Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md)

