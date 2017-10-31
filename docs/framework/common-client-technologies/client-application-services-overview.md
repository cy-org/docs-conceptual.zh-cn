---
title: "客户端应用程序服务概述"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client application services, classes
- client application services, about client application services
ms.assetid: f0a2da13-e282-4fd7-88a1-f9102c9aeab1
caps.latest.revision: 25
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ed6264230579fa48903b26896c814d478950e184
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="client-application-services-overview"></a>客户端应用程序服务概述
使用客户端应用程序服务，可简便地从 Windows 窗体和 Windows Presentation Foundation (WPF) 应用程序访问 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 登录、角色和配置文件服务。 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 应用程序服务包含在 Microsoft ASP.NET 2.0 AJAX Extensions 中，而它又包含在 [!INCLUDE[vs_orcas_long](../../../includes/vs-orcas-long-md.md)] 和 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 中。 这些服务使多个基于 Web 和 Windows 的应用程序共享来自单个服务器的用户信息和用户管理功能。  
  
 客户端应用程序服务包括插入至 Web 服务扩展性模型以启用基于 Windows 的应用程序的以下功能的客户端服务提供程序：  
  
-   简单的客户端配置。 你可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 项目设计器或在项目的 App.config 文件中指定客户端服务提供程序以启用和配置登录、角色和配置文件服务。 有关详细信息，请参阅[如何：配置客户端应用程序服务](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。  
  
-   简单的可编程性。 启用和配置客户端应用程序服务后，可以通过现有的 [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] 成员资格、角色和应用程序设置类来间接访问服务提供程序。 也可以直接访问实现客户端应用程序服务的 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 类。 但是，在大多数情况下，没必要直接访问。 有关客户端应用程序服务类的详细信息，请参阅本主题的“客户端应用程序服务类”一节。  
  
-   脱机支持。 基于 Windows 的应用程序通常需要在偶尔连接的环境中运行。 当你的应用程序处于联机状态时，客户端服务提供商将缓存服务器中检索而来的值，以供应用程序处于脱机状态时使用。  
  
-   与 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 应用程序设置设计器集成。 当你向 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中的项目添加设置时，可以指定哪些设置需要通过客户端设置服务提供程序来访问。  
  
 以下章节对这些功能进行了详细介绍。 有关 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 应用程序服务的详细信息，请参阅 [ASP.NET 应用程序服务概述](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)。  
  
## <a name="authentication"></a>身份验证  
 你可以通过现有 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 身份验证服务，使用客户端应用程序服务来验证用户。 你可以通过使用 Windows 或Forms 身份验证来验证用户。 Windows 身份验证表示用户标识是在用户登录到计算机或域时，由操作系统在提供的标识。 通常会在部署于公司 Intranet 上的应用程序中使用 Windows 身份验证。 Forms 身份验证表示你必须将登录控件包括在应用程序内，并将所需的凭据传递给身份验证提供程序。 通常会在部署于 Internet 上的应用程序中使用 Forms 身份验证。  
  
 若要验证用户，请调用 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法。 此方法访问为你的应用程序配置的客户端服务提供程序，并返回 <xref:System.Boolean> 值，该值指示用户是否有效。 有关详细信息，请参阅[如何：使用客户端应用程序服务来实现用户登录](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)。  
  
 使用 Windows 身份验证时，必须传递空字符串或 `null`，以作为 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法的参数。 使用 Windows 身份验证时，此方法调用将始终返回 `true`。  
  
 利用 Forms 身份验证，<xref:System.Web.Security.Membership.ValidateUser%2A> 方法将返回一个值，该值指示远程服务是否已经对用户进行身份验证。 如果验证成功，将本地硬盘上存储身份验证 cookie。 访问角色和设置服务时，此 cookie 将用于确认验证。  
  
 使用 Forms 身份验证时，可以将用户名和密码传递到 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法。 你还可以传递空字符串或 `null`，以作为使用凭据提供程序的参数。 凭据提供程序是在你的应用程序配置中提供并指定的类。 凭据提供程序类必须实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 接口，该接口具有一个名为 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 的方法 。 使用凭据提供程序，让你可以在多个应用程序间共享单点登录对话框。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。  
  
 配置应用程序以将凭据提供程序与 Forms 身份验证一起使用时，必须传递空字符串或 `null`，以作为 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法的参数。 服务提供程序将调用 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A?displayProperty=fullName> 方法实现。 通常情况下，您将实现此方法以显示对话框并返回填充的 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials> 对象。  
  
 有关身份验证的详细信息，请参阅 [ASP.NET 身份验证](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1)。 有关如何设置 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 身份验证服务的信息，请参阅[将 Forms 身份验证用于 Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)。  
  
## <a name="roles"></a>角色  
 可以使用客户端应用程序服务从现有 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 角色服务中检索角色信息。 若要确定经过身份验证的当前用户是否属于特定角色，请调用 `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性中 <xref:System.Security.Principal.IPrincipal> 引用的 <xref:System.Security.Principal.IPrincipal.IsInRole%2A> 方法。 <xref:System.Security.Principal.IPrincipal.IsInRole%2A> 方法将角色名称作为参数，并返回 <xref:System.Boolean> 值以指示当前用户是否为指定角色。 如果用户未经过身份验证或不在指定的角色，则此方法将返回 `false`。  
  
 有关如何设置 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 角色服务的信息，请参阅[将角色信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d)。  
  
## <a name="settings"></a>设置  
 可以使用客户端应用程序服务从现有 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 配置文件服务中检索用户应用程序设置。 客户端应用程序服务 Web 设置功能与 [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] 提供的应用程序设置功能集成。 若要检索 Web 设置，首先使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 项目设计器的“设置”选项卡为项目生成一个 `Settings` 类（在 C# 中作为 `Properties.Settings.Default` 访问，在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中作为 `My.Settings` 访问）。 在“设置”选项卡上，可以使用“加载 Web 设置”按钮检索 Web 设置，并将它们添加到生成的 `Settings` 类。 你可以使用为所有已经过身份验证的用户或所有匿名用户的使用而配置的 Web 设置。  
  
 有关应用程序设置的详细信息，请参阅[应用程序设置概述](../../../docs/framework/winforms/advanced/application-settings-overview.md)。 有关如何实现你自己的设置类而不是在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中生成一个设置类的信息，请参阅[如何：创建应用程序设置](../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)。 有关如何设置 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 配置文件服务的信息，请参阅[将配置文件信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61)。  
  
## <a name="client-application-services-classes"></a>客户端应用程序服务类  
 下表介绍了实现客户端应用程序服务功能的类。  
  
 仅使用主身份验证、角色和设置功能的应用程序无需直接访问这些类。 相反，此类应用程序将使用应用程序配置和前面部分介绍的 API，间接访问客户端应用程序服务提供程序。 你将直接访问这些类以实现用户注销和脱机功能等其他功能。  
  
> [!NOTE]
>  所有客户端应用程序服务 API 是同步的。 客户端应用程序服务不直接支持异步行为。  
  
 客户端应用程序服务提供程序实现或扩展标准 [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] 类型，但不实现这些类型所定义的每个成员和功能。 例如，你无法使用客户端应用程序服务提供程序来实现用于创建新用户和管理角色成员身份的用户管理应用程序。 若要实现此功能，当前必须使用 Web 应用程序和服务器端代码。 若要确定哪些成员未实现，请参阅参考文档，你可以访问此表中的链接。  
  
|类|描述|  
|-----------|-----------------|  
|<xref:System.Web.ClientServices.ClientFormsIdentity>|此类管理用于 Forms 身份验证的用户标识和身份验证 cookie。<br /><br /> 直接访问此类的主要目的是调用 <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A> 方法，该方法以无提示方式重新验证用户（例如，从脱机切换到联机模式时）。<br /><br /> 使用 Forms 身份验证对用户进行身份验证后，你可以通过经 `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性检索的 <xref:System.Security.Principal.IPrincipal> 引用的 <xref:System.Security.Principal.IPrincipal.Identity%2A> 属性来检索此类的实例。|  
|<xref:System.Web.ClientServices.ClientRolePrincipal>|此类管理用户角色。<br /><br /> 此类不包含任何不能间接访问的成员。 但是，对用户进行身份验证后，你可以通过 `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性访问此类的实例。|  
|<xref:System.Web.ClientServices.ConnectivityStatus>|此类提供用于将应用程序切换到脱机模式的 `static` <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A> 属性。|  
|<xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>|此类表示用户凭据。<br /><br /> 实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 接口时，你只能将此类用作 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 方法的返回值类型。|  
|<xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider>|此类管理 Forms 身份验证的远程身份验证服务的访问。<br /><br /> 直接访问此类的主要目的是使用他的 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A> 和 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.UserValidated> 成员，它们未能由基类 <xref:System.Web.Security.MembershipProvider> 实现。 你还可以使用 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.ServiceUri%2A> 属性，以编程方式设置服务位置。<br /><br /> 你可以通过 `static` <xref:System.Web.Security.Membership.Provider%2A?displayProperty=fullName> 属性检索此类的实例。|  
|<xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider>|此类管理 Windows 身份验证。<br /><br /> 直接访问此类的主要目的是调用他的 <xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider.Logout%2A> 方法。 注销后，Windows 仍将保留对用户的身份验证，但将不能访问远程应用程序服务。<br /><br /> 你可以通过 `static` <xref:System.Web.Security.Membership.Provider%2A?displayProperty=fullName> 属性检索此类的实例。|  
|<xref:System.Web.ClientServices.Providers.ClientRoleProvider>|此类管理远程角色服务访问。<br /><br /> 访问此类的主要目的是调用他的 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A> 方法。 如果你的应用程序配置为使用非零角色服务缓存超时值，则这样做很有用。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。 你还可以使用 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ServiceUri%2A> 属性，以编程方式设置服务位置。<br /><br /> 你可以通过 `static` <xref:System.Web.Security.Roles.Provider%2A?displayProperty=fullName> 属性检索此类的实例。|  
|<xref:System.Web.ClientServices.Providers.ClientSettingsProvider>|此类管理远程 Web 设置服务访问。<br /><br /> 访问此类的主要目的是处理 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> 事件。 你还可以使用 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.ServiceUri%2A> 属性，以编程方式设置服务位置。|  
|<xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>|此接口为你的应用程序提供了一个间接获取用于验证的用户凭据的方法，如本主题的身份验证部分前面的说明所述。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。|  
|<xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs>|此类提供在 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved?displayProperty=fullName> 事件处理程序中使用的 <xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs.FailedSettingsList%2A> 属性。|  
|<xref:System.Web.ClientServices.Providers.UserValidatedEventArgs>|此类提供在 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.UserValidated> 事件处理程序中使用的 <xref:System.Web.ClientServices.Providers.UserValidatedEventArgs.UserName%2A> 属性。|  
  
## <a name="see-also"></a>另请参阅  
 [客户端应用程序服务](../../../docs/framework/common-client-technologies/client-application-services.md)   
 [如何：配置客户端应用程序服务](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)   
 [如何：使用客户端应用程序服务来实现用户登录](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)   
 [演练：使用客户端应用程序服务](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)   
 [应用程序设置概述](../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [ASP.NET 应用程序服务概述](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)   
 [将 Forms 身份验证用于 Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)   
 [将角色信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d)   
 [将配置文件信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61)   
 [ASP.NET 身份验证](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1)   
 [使用角色管理授权](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)   
 [为 SQL Server 创建和配置应用程序服务数据库](http://msdn.microsoft.com/library/ab894e83-7e2f-4af8-a116-b1bff8f815b2)

