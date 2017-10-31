---
title: "Windows Identity Foundation 4.5 概述"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f723345-7270-49e2-b638-b3a34bd40517
caps.latest.revision: 11
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1e23b0261625efb1e6da070e4b5f8334b1ef7488
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="windows-identity-foundation-45-overview"></a>Windows Identity Foundation 4.5 概述
Windows Identity Foundation 4.5 是一组用于在您的应用程序中实施基于声明的标识的 .NET Framework 类。 利用 Windows Identity Foundation 4.5，您可以轻松获得声明感知应用程序和服务的好处。 WIF 4.5 可在使用 .NET Framework 4.5 版或更高版本的所有 Web 应用程序或 Web 服务中使用。 WIF 只是 Microsoft 的联合身份软件系列的一部分，它实现了基于开放式标准的共享行业愿景。 联合身份包含三个组件：[Active Directory® 联合身份验证服务](http://go.microsoft.com/fwlink/?LinkID=247516) (AD FS) 2.0、[Microsoft Azure 访问控制服务](http://go.microsoft.com/fwlink/?LinkID=247517) (ACS) 和 WIF。 这三个组件共同构成了 Microsoft 的新的基于声明的云标识和访问平台的核心。  
  
 有关 WIF 的详细信息，请参阅 MSDN 上安全开发人员中心的 [Windows Identity Foundation 网站](http://go.microsoft.com/fwlink/?LinkId=149009) (http://go.microsoft.com/fwlink/?LinkId=149009)。 有关使用 WIF 创建应用程序的简介，请参阅 Vittorio Bertocci 撰写（由 Microsoft Press 出版）的 [Windows Identity Foundation 编程](http://go.microsoft.com/fwlink/?LinkId=210158) (http://go.microsoft.com/fwlink/?LinkId=210158)。  
  
## <a name="wif-45-features"></a>WIF 4.5 功能  
 WIF 4.5 是用于生成标识感知应用程序的框架。 此框架使 WS-Trust 和 WS 联合身份验证协议抽象化，并为开发人员提供用于生成声明感知应用程序和安全令牌服务 (STS)（如果需要）的 API。 应用程序可使用 WIF 处理从 STS 颁发的令牌（如 AD FS 2.0 和 ACS），并在 Web 应用程序或 Web 服务中做出基于标识的决策。  
  
 WIF 4.5 具有以下主要功能：  
  
-   生成声明感知应用程序（依赖方应用程序）。 WIF 可帮助开发人员生成声明感知应用程序。 除了提供声明模型之外，它还为应用程序开发人员提供一组丰富的 API 以帮助根据声明做出用户访问决策。  WIF 还为开发人员提供了一致的编程体验，无论他们选择在 ASP.NET 中还是在 WCF 环境中生成其应用程序。  
  
-   将标识委托支持融入声明感知应用程序中。  利用 WIF，可以跨多个服务边界保留原始请求者的标识。 可使用框架中的“ActAs”或“OnBehalfOf”功能实现此功能，此功能使开发人员能够将标识委托支持添加到其声明感知应用程序中。  
  
-   生成自定义 STS。  WIF 使得生成支持 WS-Trust 协议的自定义 STS 变得更加轻松。 此类 STS 也称为“活动 STS”。  
  
     此外，该框架还提供对生成支持 WS 联合身份验证的 STS 的支持以启用 Web 浏览器客户端。 此类 STS 也称为“被动 STS”。  
  
-   利用适用于 Visual Studio 11 的新的标识和访问工具，您可以使用基于声明的标识保护您的应用程序，并接受来自多个标识提供程序的用户。 可以从以下 URL：[http://go.microsoft.com/fwlink/?LinkID=245849](http://go.microsoft.com/fwlink/?LinkID=245849) 下载此 WIF 工具，或者直接在扩展管理器中搜索“标识”，从 Visual Studio 11 中下载。 有关详细信息，请参阅[用于 Visual Studio 2012 的标识和访问工具](../../../docs/framework/security/identity-and-access-tool-for-vs.md)。  
  
 WIF 支持以下主要方案：  
  
-   联合身份验证。  利用 WIF，可以在两个或更多合作伙伴之间启用联合身份验证。 它为生成声明感知应用程序 (RP) 和自定义 STS 提供支持，可帮助开发人员实现此方案。  
  
-   标识委托。  利用 WIF，可以轻松跨服务边界保留标识，以便开发人员能够实现标识委托方案。  
  
-   升级身份验证。 应用程序中不同资源的身份验证要求可能有所不同。 WIF 使开发人员能够生成具有逐渐提高的身份验证（例如：使用用户名/密码身份验证进行初始登录，然后升级到智能卡身份验证）要求的应用程序。  
  
 通过使用 WIF，您可以更轻松地获得基于声明的标识模型的好处。 有关详细信息，请参阅[面向开发人员的 Windows Identity Foundation 白皮书](http://go.microsoft.com/fwlink/?LinkId=122266)。

