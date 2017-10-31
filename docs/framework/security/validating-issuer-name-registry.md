---
title: "验证颁发者名称注册表"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4644dd1-dead-48ff-abeb-7bffae69a6ac
caps.latest.revision: 4
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c6c1b72048f1f7cb421e5a19d34c2c2dea5463ce
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="validating-issuer-name-registry"></a>验证颁发者名称注册表
Windows Identity Foundation 的验证颁发者名称注册表 (VINR) 可启用多租户应用程序，以确保传入标记已由受信任的租户和标识提供者颁发。 此功能对于使用 Microsoft Azure Active Directory 的多租户应用程序尤其有用，因为由 Microsoft Azure AD 颁发的所有标记都使用同一证书进行签名。 为了区分来自使用同一证书的多个租户的请求（它们具有相同的指纹），您的应用程序必须保持每个租户的颁发者名称以便执行验证逻辑。 VINR 可提供此功能，除了配置文件之外，还使您能够在位置中添加自定义验证逻辑或存储颁发者注册表数据。 该扩展可添加到应用程序的 WIF 管道中，也可单独进行使用。  
  
 VINR 作为 NuGet 程序包提供。 请参阅[下载验证颁发者名称注册表包](../../../docs/framework/security/downloading-the-validating-issuer-name-registry-package.md)，了解详细信息。  
  
## <a name="scenarios"></a>方案  
 VINR 支持以下关键方案：  
  
-   在多租户应用程序中验证标记：在此方案中，一家名为 Litware 的公司开发了一个使用标识提供者（如 Microsoft Azure AD）的多租户应用程序。 此应用程序为两个客户提供服务：Contoso 和 Fabrikam。 当针对 Litware 的应用程序对来自 Fabrikam 的用户进行身份验证时，将使用其标准证书对 Microsoft Azure AD 的结果标记进行签名并且 Fabrikam 将发出请求。 应用程序需要验证颁发者名称和标记是否有效，并且需要区分使用来自 Microsoft Azure AD 的同一证书进行签名的 Contoso 请求。 VINR 使得 Litware 的应用程序能够轻松区分和验证来自多个租户（例如 Contoso 和 Fabrikam）的请求。  
  
## <a name="features"></a>功能  
 VINR 具有以下功能：  
  
-   颁发者名称和多租户应用程序的标记验证：通过确认颁发者名称（租户）来验证传入标记，并验证是否已使用来自标识提供者的有效证书对标记进行签名。  
  
-   自定义验证逻辑和数据存储的扩展性：除了默认配置文件之外，还提供扩展性以插入自己的验证逻辑并指定数据存储。

