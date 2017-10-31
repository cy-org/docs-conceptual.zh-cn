---
title: "WSFederation 身份验证模块概述"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02c4d5e8-f0a7-49ee-9cf5-3647578510ad
caps.latest.revision: 6
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a53900d8305352a1122efda1abc75ce2b1626fe6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="wsfederation-authentication-module-overview"></a>WSFederation 身份验证模块概述
Windows Identity Foundation (WIF) 包括通过 WS-联合身份验证模块 (WS-FAM) 对 ASP.NET 应用程序中联合身份验证的支持。 本主题有助于理解联合身份验证的工作原理和使用方法。  
  
### <a name="overview-of-federated-authentication"></a>联合身份验证概述  
 当两个信任域之间存在信任关系时，联合身份验证允许一个信任域中的安全令牌服务 (STS) 向另一个信任域中的 STS 提供身份验证信息。 下图显示了此情况的示例。  
  
 ![联合身份验证方案](../../../docs/framework/security/media/federatedauthentication.gif "FederatedAuthentication")  
  
1.  Fabrikam 信任域中的客户端向 Contoso 信任域中的信赖方 (RP) 应用发送请求。  
  
2.  RP 将客户端重定向到 Contoso 信任域中的 STS。 此 STS 完全不了解该客户端。  
  
3.  Contoso STS 将该客户端重定向到 Fabrikam 信任域中的 STS，此信任域与 Contoso 信任域之间存在信任关系。  
  
4.  Fabrikam STS 验证客户端的标识，并向 Contoso STS 颁发安全令牌。  
  
5.  Contoso STS 使用 Fabrikam 令牌来创建自己的令牌（可由 RP 使用）并将其发送到 RP。  
  
6.  RP 从安全令牌中提取客户端声明并做出授权决策。  
  
### <a name="using-the-federated-authentication-module-with-aspnet"></a>将联合身份验证模块与 ASP.NET 搭配使用  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (WS-FAM) 是一个可以将联合身份验证添加到 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 应用程序的 HTTP 模块。 联合身份验证将身份验证逻辑交由 STS 处理，让你可以集中注意力编写业务逻辑。  
  
 可以配置 WS-FAM 来指定未经身份验证的请求应重定向到的 STS。 使用 WIF，可采用两种方式对用户进行身份验证：  
  
1.  被动重定向：如果未经身份验证的用户尝试访问受保护的资源，且你希望在无需登录页的情况下将它们重定向到 STS，则这是正确的方法。 STS 验证用户标识，并颁发包含适合该用户的声明的安全令牌。 此选项需要将 WS-FAM 添加到 HTTP 模块管道。 可以使用用于 Visual Studio 2012 的标识和访问工具修改应用程序配置文件，以便使用 WS FAM 以及与 STS 联合。 有关详细信息，请参阅[用于 Visual Studio 2012 的标识和访问工具](../../../docs/framework/security/identity-and-access-tool-for-vs.md)。  
  
2.  对于信赖方应用程序中的登录页，可以从代码隐藏调用 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignIn%2A?displayProperty=fullName> 方法或 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectToIdentityProvider%2A> 方法。  
  
 在被动重定向中，所有通信通过来自客户端（通常为浏览器）的响应/重定向执行。 可将 WS-FAM 添加到应用程序的 HTTP 管道，它将在管道中监视未经身份验证的用户请求并将用户重定向到指定的 STS。  
  
 WS-FAM 也会引发几个事件，可以通过这些事件在 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 应用程序中自定义它的功能。  
  
### <a name="how-the-ws-fam-works"></a>WS-FAM 的工作原理  
 WS-FAM 在 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 类中实现。 通常情况下，将 WS-FAM 添加到 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 信赖方应用的 HTTP 管道。 未经身份验证的用户尝试访问受保护资源时，RP 将返回 HTTP 响应“401 拒绝授权”。 WS-FAM 截获此响应，而不是让客户端接收它，然后将用户重定向到指定的 STS。 STS 颁发安全令牌，WS-FAM 再次将其截获。 WS-FAM 使用该令牌为经过身份验证的用户创建 <xref:System.Security.Claims.ClaimsPrincipal> 实例，从而常规 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 授权机制得以运行。  
  
 因为 HTTP 无状态，所以需要一种方法来避免在每次用户尝试访问另一个受保护资源时重复上述过程。 这时 <xref:System.IdentityModel.Services.SessionAuthenticationModule> 便可派上用场。 当 STS 向用户颁发安全令牌时，<xref:System.IdentityModel.Services.SessionAuthenticationModule> 也会为该用户创建会话安全令牌并将其放置于 Cookie 中。 在后续请求中，<xref:System.IdentityModel.Services.SessionAuthenticationModule> 将截获此 Cookie 并使用它来重新构造用户的 <xref:System.Security.Claims.ClaimsPrincipal>。  
  
 下方的关系图展示了被动重定向事例中整体信息流。 通过 STS 自动重定向请求，无需登录页便可建立凭据：  
  
 ![使用被动重定向登录的执行时序图](../../../docs/framework/security/media/signinusingpassiveredirect.gif "SignInUsingPassiveRedirect")  
  
 下方的关系图展示了用户经过身份验证访问 STS 且由 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 处理其安全令牌后的更多详细信息：  
  
 ![使用被动重定向处理令牌的时序](../../../docs/framework/security/media/signinusingpassiveredirect-tokenprocessing.gif "SignInUsingPassiveRedirect_TokenProcessing")  
  
 下方的关系图展示了将用户的安全令牌串行化成 Cookie 并由 <xref:System.IdentityModel.Services.SessionAuthenticationModule> 截获后的更多详细信息：  
  
 ![显示使用控件登录的 SAM 时序图](../../../docs/framework/security/media/signinusingconrols-sam.gif "SignInUsingConrols_SAM")  
  
### <a name="events"></a>事件  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>、<xref:System.IdentityModel.Services.SessionAuthenticationModule> 和它们的父类 <xref:System.IdentityModel.Services.HttpModuleBase> 在处理 HTTP 请求的各个阶段引发事件。 可以在 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 应用程序的 `global.asax` 文件中处理这些事件。  
  
-   ASP.NET 基础结构调用模块的 <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> 方法来初始化模块。  
  
-   ASP.NET 基础结构首次在派生于 <xref:System.IdentityModel.Services.HttpModuleBase> 的某个应用程序模块上调用 <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> 方法时将引发 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated?displayProperty=fullName> 事件。 此方法访问静态 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName> 属性，导致从 Web.config 文件加载配置。 仅在首次访问此属性时引发该事件。 可以通过事件处理程序中的 <xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=fullName> 属性访问从配置中初始化的 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 对象。 可以在将配置应用到任何模块前使用此事件修改配置。 可以在 Application_Start 方法中为此事件添加处理程序：  
  
    ```  
    void Application_Start(object sender, EventArgs e)  
    {  
        FederatedAuthentication.FederationConfigurationCreated += new EventHandler<FederationConfigurationCreatedEventArgs>(FederatedAuthentication_FederationConfigurationCreated);  
    }  
    ```  
  
     每个模块替代 <xref:System.IdentityModel.Services.HttpModuleBase.InitializeModule%2A?displayProperty=fullName> 和 <xref:System.IdentityModel.Services.HttpModuleBase.InitializePropertiesFromConfiguration%2A?displayProperty=fullName> 抽象方法。 第一种方法为与模块相关的 ASP.NET 管道事件添加处理程序。 大多数情况下，模块的默认实现便已足够。 第二种方法从模块的 <xref:System.IdentityModel.Services.HttpModuleBase.FederationConfiguration%2A?displayProperty=fullName> 属性初始化其各个属性。 （这是之前加载的配置的副本。）如果要支持从派生自 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 或 <xref:System.IdentityModel.Services.SessionAuthenticationModule> 的类中的配置初始化新属性，则需要替代第二种方法。 在此情况下，也需要从相应的配置对象进行派生，从而支持添加的配置属性；例如，从 <xref:System.IdentityModel.Configuration.IdentityConfiguration>、<xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> 或 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 派生。  
  
-   WS-FAM 截获由 STS 颁发的安全令牌时引发 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenReceived> 事件。  
  
-   WS-FAM 在验证令牌后引发 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenValidated> 事件。  
  
-   <xref:System.IdentityModel.Services.SessionAuthenticationModule> 在为用户创建会话安全令牌时，引发 <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenCreated> 事件。  
  
-   <xref:System.IdentityModel.Services.SessionAuthenticationModule> 使用包含会话安全令牌的 Cookie 截获后续请求时，引发 <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenReceived> 事件。  
  
-   在 WS-FAM 将用户重定向到颁发者之前引发 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> 事件。 事件中传递的 <xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs> 的 <xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs.SignInRequestMessage%2A> 属性提供 WS 联合身份验证登录请求。 可选择在将请求发送到颁发者之前修改请求。  
  
-   成功写入 Cookie 且用户登录后，WS-FAM 引发 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignedIn> 事件。  
  
-   为每个用户关闭会话时，WS FAM 将对每个会话引发一次 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SigningOut> 事件。 如果在客户端上关闭会话（例如，通过删除会话 Cookie 的方式），则不会引发该事件。 在 SSO 环境中，IP-STS 也可以请求每个 RP 注销。 这也将引发此事件，这时 <xref:System.IdentityModel.Services.SigningOutEventArgs.IsIPInitiated%2A> 设置为 `true`。  
  
> [!NOTE]
>  不应在由 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 或 <xref:System.IdentityModel.Services.SessionAuthenticationModule> 引发的任何事件期间使用 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性。 这是因为 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 是在身份验证进程后设置的，而事件是在身份验证进程中引发的。  
  
### <a name="configuration-of-federated-authentication"></a>联合身份验证的配置  
 WS-FAM 和 SAM 通过 [\<federationConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 元素进行配置。 [\<wsFederation>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/wsfederation.md) 子元素配置 WS-FAM 属性的默认值；例如 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Issuer%2A> 属性和 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Realm%2A> 属性。 （可以通过为一些 WS-FAM 事件提供处理程序来按请求更改这些值；例如 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider>。）由 SAM 使用的 Cookie 处理程序通过 [\<cookieHandler>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md) 子元素进行配置。 WIF 提供在 <xref:System.IdentityModel.Services.ChunkedCookieHandler> 类中实现的默认 Cookie 处理程序，可以通过 [\<chunkedCookieHandler>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/chunkedcookiehandler.md) 元素设置该处理程序的区块大小。 `<federationConfiguration>` 元素引用 <xref:System.IdentityModel.Configuration.IdentityConfiguration>，为在应用程序中使用的其他 WIF 组件提供配置，如 <xref:System.Security.Claims.ClaimsAuthenticationManager> 和 <xref:System.Security.Claims.ClaimsAuthorizationManager>。 可以通过指定 `<federationConfiguration>` 元素的 `identityConfigurationName` 属性中名为 [\<identityConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 的元素显式引用标识配置。 如果未显式引用标识配置，则将使用默认标识配置。  
  
 以下 XML 演示 ASP.NET 信赖方 (RP) 应用的配置。 <xref:System.IdentityModel.Configuration.SystemIdentityModelSection> 和 <xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection> 配置部分添加在 `<configSections>` 元素之下。 SAM 和 WS-FAM 添加到 `<system.webServer>`/`<modules>` 元素下的 HTTP 模块。 最后，WIF 组件在 `<system.identityModel>`/`<identityConfiguration>` 和 `<system.identityModel.services>`/`<federationConfiguration>` 元素下进行配置。 此配置指定分块 Cookie 处理程序（因为它是默认 Cookie 处理程序），且 `<cookieHandler>` 元素中没有指定的 Cookie 处理程序类型。  
  
> [!WARNING]
>  在以下示例中，`<wsFederation>` 元素的 `requireHttps` 属性和 `<cookieHandler>` 元素的 `requireSsl` 属性皆为 `false`。 这表示潜在的安全威胁。 在生产中，这两个值都应设置为 `true`。  
  
```xml  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  ...  
  
  <system.webServer>  
    <modules>  
      <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
    </modules>  
  </system.webServer>  
  
  <system.identityModel>  
    <identityConfiguration>  
      <audienceUris>  
        <add value="http://localhost:50969/" />  
      </audienceUris>  
      <certificateValidation certificateValidationMode="None" />  
      <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
        <trustedIssuers>  
          <add thumbprint="9B74CB2F320F7AAFC156E1252270B1DC01EF40D0" name="LocalSTS" />  
        </trustedIssuers>  
      </issuerNameRegistry>  
    </identityConfiguration>  
  </system.identityModel>  
  <system.identityModel.services>  
    <federationConfiguration>  
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:15839/wsFederationSTS/Issue" realm="http://localhost:50969/" reply="http://localhost:50969/" requireHttps="false" />  
      <cookieHandler requireSsl="false" />  
    </federationConfiguration>  
  </system.identityModel.services>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>   
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 [\<federationConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)

