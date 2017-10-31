---
title: "生成我的第一个声明感知 ASP.NET Web 应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ee8ee7f-caba-4267-9343-e313fae2876d
caps.latest.revision: 5
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: aa25f163199652618e35399c6548a9864a17370a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="building-my-first-claims-aware-aspnet-web-application"></a>生成我的第一个声明感知 ASP.NET Web 应用程序
## <a name="applies-to"></a>适用于  
  
-   Windows Identity Foundation (WIF)  
  
-   ASP.NET  
  
 本主题概述了使用 WIF 生成声明感知 ASP.NET Web 应用程序的方案。 声明感知应用程序方案通常涉及三个参与者：应用程序本身、最终用户和安全令牌服务 (STS)。 下图描述了此方案：  
  
 ![WIF 基本 Web 应用](../../../docs/framework/security/media/wifbasicwebapp.gif "WIFBasicWebApp")  
  
1.  声明感知应用程序使用 WIF 来标识未经身份验证的请求并将这些请求重定向到 STS。  
  
2.  最终用户向 STS 提供凭据，在成功完成身份验证后，STS 将向用户颁发令牌。  
  
3.  使用请求中的 STS 颁发的令牌将用户从 STS 重定向到声明感知应用程序。  
  
4.  声明感知应用程序将配置为信任此 STS 及其颁发的令牌。 声明感知应用程序使用 WIF 验证此令牌并对其进行分析。 开发人员使用适当的 WIF API 和类型（例如 ClaimsPrincpal）来满足应用程序的需要，如对其实现授权。  
  
 从 .NET 4.5 开始，WIF 便已成为 .NET Framework 包的一部分。 通过使 WIF 类直接在框架中可用，可以在 .NET 中更深度地集成基于声明的标识，从而更轻松地使用声明。 如果使用 WIF 4.5，则无需安装任何带外组件即可开始开发声明感知 Web 应用程序。 WIF 类现在分布在各种程序集中，主要为 System.Security.Claims、System.IdentityModel 和 System.IdentityModel.Services。  
  
 STS 是一项在身份验证成功后颁发令牌的服务。 Microsoft 提供两个行业标准 STS：  
  
-   [Active Directory 联合身份验证服务 (AD FS) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516) (http://go.microsoft.com/fwlink/?LinkID=247516)  
  
-   [Microsoft Azure 访问控制服务 (ACS)](http://go.microsoft.com/fwlink/?LinkID=247517) (http://go.microsoft.com/fwlink/?LinkID=247517)。  
  
 AD FS 2.0 是 Windows Server R2 的一部分并可用作本地方案的 STS。 ACS 是一项云服务，它作为 Microsoft Azure 平台的一部分提供。 出于测试或教学目的，你还可以使用其他 STS 以生成声明感知应用程序。 例如，可以使用联机免费提供的[用于 Visual Studio 的标识和访问工具](http://go.microsoft.com/fwlink/?LinkID=245849) (http://go.microsoft.com/fwlink/?LinkID=245849) 一部分的本地开发 STS。  
  
 若要使用 WIF 生成您的第一个声明感知 ASP.NET 应用程序，请按照下列主题之一中的说明进行操作：  
  
-   [如何：使用 WIF 生成声明感知 ASP.NET MVC Web 应用程序](../../../docs/framework/security/how-to-build-claims-aware-aspnet-mvc-web-app-using-wif.md)  
  
-   [如何：使用 WIF 生成声明感知 ASP.NET Web 窗体应用程序](../../../docs/framework/security/how-to-build-claims-aware-aspnet-web-forms-app-using-wif.md)  
  
-   [如何：使用基于表单的身份验证生成声明感知 ASP.NET 应用程序](../../../docs/framework/security/claims-aware-aspnet-app-forms-authentication.md)  
  
## <a name="see-also"></a>另请参阅  
 [WIF 入门](../../../docs/framework/security/getting-started-with-wif.md)

