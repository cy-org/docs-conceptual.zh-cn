---
title: "客户端应用程序服务"
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
- role-based security [.NET Framework], client application services
- client application services
- credentials [.NET Framework]
- Windows-based applications, client application services
- application settings, client application services
- profiles [ASP.NET], client application services
- logins [client application services]
- sharing information and functionality [client application services]
- Web settings [client application services]
- authentication [ASP.NET], client application services
- ASP.NET services, client application services
- client applications, ASP.NET services
- roles [.NET Framework], client application services
- client application services, about client application services
ms.assetid: 1487d8df-089e-4f21-abfb-a791a652b58e
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c776040786a51089c9aa988e9229805c06b28bae
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="client-application-services"></a>客户端应用程序服务
借助客户端应用程序服务，可以轻松使用 Microsoft ASP.NET 2.0 AJAX Extensions 中包含的 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 登录名、角色和配置文件应用程序服务，创建基于 Windows 的应用程序。 这些服务使多个基于 Web 和 Windows 的应用程序共享来自单个服务器的用户信息和用户管理功能。 例如，你可以使用这些服务来执行下列任务：  
  
-   对用户进行身份验证。 你可以使用身份验证服务验证用户的身份。  
  
-   确定经身份验证的用户的角色。 你可以根据用户的角色使用角色服务来更改应用程序的用户界面。 例如，你可以为管理员角色的用户提供其他功能。  
  
-   存储和访问位于服务器上的每用户应用程序设置。 你可以使用 Web 设置服务（也称为配置文件服务）跨多个应用程序和位置共享设置。  
  
 客户端应用程序服务通过可在应用程序配置文件中指定的客户端服务提供程序来利用 Web 服务扩展性模型。 网络连接不可用时，这些服务提供程序包括使用本地缓存进行身份验证、角色和设置数据等脱机功能。  
  
 有关 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 应用程序服务的详细信息，请参阅 [ASP.NET 应用程序服务概述](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)。  
  
## <a name="in-this-section"></a>本节内容  
 [客户端应用程序服务概述](../../../docs/framework/common-client-technologies/client-application-services-overview.md)  
 介绍可通过客户端应用程序服务提供程序提供的功能。  
  
 [如何：配置客户端应用程序服务](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)  
 介绍如何使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 项目设计器启用并配置应用程序服务。 还介绍了对 App.config 文件的相应更改。  
  
 [如何：使用客户端应用程序服务来实现用户登录](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 介绍如何在应用程序配置为使用客户端身份验证服务提供程序时验证用户。  
  
 [演练：使用客户端应用程序服务](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 介绍如何在单个应用程序中合并所有客户端应用程序服务功能。 本演练提供了端到端指导。 例如，它包括有关如何创建可用于测试客户端应用程序服务的 ASP.NET Web 服务应用程序的说明。  
  
## <a name="reference"></a>参考  
 <xref:System.Web.ClientServices.ClientFormsIdentity>  
 <xref:System.Web.ClientServices.ClientRolePrincipal>  
 <xref:System.Web.ClientServices.ConnectivityStatus>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>  
 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientRoleProvider>  
 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider>  
 <xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs>  
 <xref:System.Web.ClientServices.Providers.UserValidatedEventArgs>  
  
## <a name="see-also"></a>另请参阅  
 [ASP.NET 应用程序服务概述](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)   
 [将 Forms 身份验证用于 Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)   
 [将角色信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d)   
 [将配置文件信息用于 Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61)   
 [ASP.NET 身份验证](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1)   
 [使用角色管理授权](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)    
 [应用程序设置概述](../../../docs/framework/winforms/advanced/application-settings-overview.md)

