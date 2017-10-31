---
title: "JSON Web 标记处理程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9968f12e-e05d-4e6a-9b65-6896c0e31ab1
caps.latest.revision: 5
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6772d484fa4d0ed3948ecee26adb2cf886340f11
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="json-web-token-handler"></a>JSON Web 标记处理程序
Windows Identity Foundation 的 JSON Web 标记处理程序扩展使你能够在应用程序中创建和验证 JSON Web 标记 (JWT)。 可将 JWT 标记处理程序配置为像其他内置安全标记处理程序一样在 WIF 管线中运行，但也可以单独使用它来在轻型应用程序中执行标记验证。 在使用 OAuth 2.0 持有人标记方案（例如，对 Microsoft Azure Active Directory 进行身份验证）时，JWT 标记处理程序尤其有用。  
  
 JWT 标记处理程序将作为 NuGet 程序包提供。 有关详细信息，请参阅[下载 JSON Web 令牌处理程序包](../../../docs/framework/security/downloading-the-json-web-token-handler-package.md)。  
  
## <a name="scenarios"></a>方案  
 JWT 标记处理程序支持以下关键方案：  
  
-   **在服务器应用程序中验证 JWT 令牌**：在此方案中，一家名为 Litware 的公司具有使用 WIF 处理 Web 登录请求的服务器应用程序。 Litware 希望使其应用程序能够使用 JWT 标记进行身份验证。 应用程序与 JWT 标记处理程序一起更新，然后更新应用程序配置以在 WIF 管线中添加 JWT 标记处理程序。 在更新完成且新请求输入 WIF 管线后，会使用新的处理程序验证 JWT 标记，并且身份验证将获得成功。  
  
-   **在 REST Web 服务中验证 JWT 令牌**：在此方案中，一家名为 Litware 的公司具有由 Microsoft Azure Active Directory 保护的 REST Web 服务。 对 Web 服务的请求必须由 Microsoft Azure AD 进行身份验证，后者在身份验证成功完成后会发出 JWT 标记。 Litware 的客户端应用程序需要访问 Web 服务。 客户端向 Web 服务发出请求，并显示 Microsoft Azure AD 中的 JWT 标记，然后 Web 服务使用 JWT 标记处理程序验证此标记。 在 JWT 标记处理程序验证该标记之后，Web 服务会将所需的资源返回到客户端。  
  
## <a name="features"></a>功能  
 JWT 标记处理程序具有以下功能：  
  
-   **验证 JWT 令牌**：JWT 令牌可由令牌处理程序的验证逻辑轻松验证，后者可作为应用程序的 WIF 管线的一部分或独立于 WIF 进行调用  
  
-   **创建 JWT 令牌**：JWT 令牌处理程序可用于创建 JWT 标记以便在下游服务中进行授权

