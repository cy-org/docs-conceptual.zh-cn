---
title: "如何：使用客户端应用程序服务来实现用户登录"
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
- validating users [client application services]
- validation [.NET Framework], client application services
- client application services, authenticate users
ms.assetid: 5431a671-eb02-4e18-a651-24764fccec9a
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9acd7e677b981c68b4aad7d10b41d7cef2e2eb06
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-implement-user-login-with-client-application-services"></a>如何：使用客户端应用程序服务来实现用户登录
可以通过现有 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 配置文件服务，使用客户端应用程序服务来验证用户。 有关如何设置 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 配置文件服务的信息，请参阅[将 Forms 身份验证用于 Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)。  
  
 以下过程介绍如何在应用程序配置为使用客户端身份验证服务提供程序之一时，通过身份验证服务验证用户。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。  
  
 通常，可通过 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法执行所有验证。 此方法通过配置的身份验证提供程序管理与身份验证服务进行的交互。 有关详细信息，请参阅[客户端应用程序服务概述](../../../docs/framework/common-client-technologies/client-application-services-overview.md)。  
  
 Forms 身份验证过程需要访问正在运行的 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 身份验证服务。 有关客户端应用程序服务功能端到端测试的指南，请参阅[演练：使用客户端应用程序服务](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)。  
  
### <a name="to-authenticate-a-user-with-forms-authentication-using-a-membership-credentials-provider"></a>使用成员资格凭据提供程序通过 Forms 身份验证对用户进行身份验证  
  
1.  实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 接口。 下面的代码示例演示从 <xref:System.Windows.Forms.Form?displayProperty=fullName> 派生的登录对话框类的 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A?displayProperty=fullName> 实现。 此对话框中具有用于输入用户名和密码的文本框，以及一个“记住我”复选框。 客户端身份验证提供程序调用 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 方法时，会显示窗体。 用户在登录对话框中填写信息并单击“确定”时，会在新 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials> 对象中返回指定值。  
  
     [!code-csharp[ClientApplicationServices#210](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Login.cs#210)][!code-vb[ClientApplicationServices#210](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#210)]  
  
2.  调用 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法并传入空字符串作为参数值。 指定空字符串时，此方法针对为应用程序配置的凭据提供程序在内部调用 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 方法。 下面的代码示例调用此方法以限制对整个 Windows 窗体应用程序的访问。 可以将此代码添加到 <xref:System.Windows.Forms.Form.Load?displayProperty=fullName> 处理程序。  
  
     [!code-csharp[ClientApplicationServices#317](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#317)][!code-vb[ClientApplicationServices#317](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#317)]  
  
### <a name="to-authenticate-a-user-with-forms-authentication-without-using-a-membership-credentials-provider"></a>在不使用成员资格凭据提供程序的情况下通过 Forms 身份验证对用户进行身份验证  
  
-   调用 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法并传入从用户检索的用户名和密码值。  
  
     [!code-csharp[ClientApplicationServices#318](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#318)][!code-vb[ClientApplicationServices#318](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#318)]  
  
### <a name="to-authenticate-a-user-with-windows-authentication"></a>使用 Windows 身份验证对用户进行身份验证  
  
-   调用 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法并传递空字符串用作参数。 此方法调用将始终返回 `true`，并会将 cookie 添加到包含 Windows 标识的用户 cookie 缓存。  
  
     [!code-csharp[ClientApplicationServices#319](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#319)][!code-vb[ClientApplicationServices#319](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#319)]  
  
## <a name="robust-programming"></a>可靠编程  
 本主题中的代码示例演示 Windows 客户端应用程序中的身份验证的最简单用法。 但是，对客户端应用程序服务和窗体身份验证调用 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法时，代码可能会引发 <xref:System.Net.WebException>。 这指示身份验证服务不可用。 有关如何处理此异常的示例，请参阅[演练：使用客户端应用程序服务](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [客户端应用程序服务](../../../docs/framework/common-client-technologies/client-application-services.md)   
 [客户端应用程序服务概述](../../../docs/framework/common-client-technologies/client-application-services-overview.md)   
 [如何：配置客户端应用程序服务](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)   
 [演练：使用客户端应用程序服务](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)   
 [将 Forms 身份验证用于 Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)

