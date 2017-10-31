---
title: "使用 WIF 的基于声明的授权"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e24000a3-8fd8-4c0e-bdf0-39882cc0f6d8
caps.latest.revision: 6
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f1086958a56aadbddf54f20295b91e885adf71c4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="claims-based-authorization-using-wif"></a>使用 WIF 的基于声明的授权
在依赖方应用程序中，授权可确定允许已经过身份验证的标识访问的资源以及允许该标识对这些资源执行的操作。 授权不当会导致信息泄露和数据篡改。 本主题概述了可用于通过 Windows Identity Foundation (WIF) 和安全令牌服务 (STS) 来实现针对声明感知 ASP.NET Web 应用程序和服务（例如，Microsoft Azure 访问控制服务 (ACS)）的授权的方法。  
  
## <a name="overview"></a>概述  
 .NET Framework 自其第一个版本开始便已提供用于实现授权的灵活机制。 此机制基于两个简单接口 - IPrincipal 接口和 IIdentity 接口。 IIdentity 接口的具体实现表示已经过身份验证的用户。 例如，WindowsIdentity 实现表示已由 Active Directory 进行身份验证的用户，而 GenericIdentity 表示已经过自定义身份验证过程验证其身份的用户。 IPrincipal 接口的具体实现可帮助使用角色（具体取决于角色存储）检查权限。 例如，WindowsPrincipal 检查 Active Directory 组中 WindowsIdentity 的成员资格。 通过在 IPrincipal 接口上调用 IsInRole 方法执行此检查。 基于角色检查访问权称作基于角色的访问控制 (RBAC)。 有关详细信息，请参阅[基于角色的访问控制](../../../docs/framework/security/claims-based-authorization-using-wif.md#BKMK_1)。  声明可用于携带有关角色的信息以支持熟悉的、基于角色的授权机制。  
  
 声明还可用于启用超出角色范围的更复杂的授权决策。 声明可以基于用户的年龄、邮编、鞋码等几乎任何信息。基于任意声明的访问控制机制称为基于声明的授权。 有关详细信息，请参阅[基于声明的授权](../../../docs/framework/security/claims-based-authorization-using-wif.md#BKMK_2)。  
  
<a name="BKMK_1"></a>   
## <a name="role-based-access-control"></a>基于角色的访问控制  
 RBAC 是一种授权方法，其中的用户权限由基于用户角色的应用程序管理和强制实施。 如果用户具有执行操作所需的角色，则将授予访问权；否则，访问将被拒绝。  
  
### <a name="iprincipalisinrole-method"></a>IPrincipal.IsInRole 方法  
 若要在声明感知应用程序中实现 RBAC 方法，请在 IPrinicpal 接口中使用 IsInRole() 方法，与在非声明感知应用程序中执行的操作一样。 使用 IsInRole() 方法有好几种方式：  
  
-   对 IPrincipal.IsInRole(“Administrator”) 进行显式调用。 在此方法中，结果为布尔值。 在条件语句中使用它。 可在代码中的任意位置使用它。  
  
-   使用安全性要求 PrincipalPermission.Demand()。 在此方法中，如果未满足要求，则结果为异常。 这应适合您的异常处理策略。 从性能角度看，与停用布尔值相比，引发异常的代价更高。 可在代码中的任何位置进行使用。  
  
-   使用声明性特性 [PrincipalPermission(SecurityAction.Demand, Role = “Administrator”)]。 此方法称为声明性方法，因为它用于修饰方法。 它不能在方法实现中的代码块内使用。 如果未满足要求，则结果为异常。 您应确保它适合您的异常处理策略。  
  
-   使用 URL 授权，并使用 web.config 中的\<authorization> 部分。在 URL 级别上管理授权时，此方法很适用。 这是前面提到的方法中最粗糙的方法。 此方法的优点在于，更改是在配置文件中做出的，这意味着无需编译代码即可利用此更改。  
  
### <a name="expressing-roles-as-claims"></a>将角色表示为声明  
 调用 IsInRole() 方法时，会进行一次检查以查明当前用户是否拥有该角色。 在声明感知应用程序中，该角色由应在令牌中可用的角色声明类型表示。 使用以下 URI 表示此角色声明类型：  
  
 http://schemas.microsoft.com/ws/2008/06/identity/claims/role  
  
 可通过几种方法增强带角色声明类型的令牌：  
  
-   **在令牌颁发过程中**。 对用户进行身份验证时，可由标识提供程序 STS 或联合身份验证提供程序（如 Microsoft Azure 访问控制服务 (ACS)）发布角色声明。  
  
-   **使用 ClaimsAuthenticationManager 将任意声明转换为声明角色类型**。 ClaimsAuthenticationManager 是作为 WIF 的一部分附带的组件。 它允许在请求启动应用程序时拦截请求，并通过添加、更改或删除声明来检查并转换令牌。 有关如何使用 ClaimsAuthenticationManager 来转换声明的详细信息，请参阅[操作方法：在声明感知 ASP.NET 应用程序中使用 WIF 和 ACS 实施基于角色的访问控制 (RBAC)](http://go.microsoft.com/fwlink/?LinkID=247445) (http://go.microsoft.com/fwlink/?LinkID=247444)。  
  
-   使用 samlSecurityTokenRequirement 配置节将任意声明映射到角色类型 - 一种声明性方法，其中仅使用配置完成声明转换且无需编码。  
  
<a name="BKMK_2"></a>   
## <a name="claims-based-authorization"></a>基于声明的授权  
 基于声明的授权是一种方法，其中授予访问权或拒绝访问的授权决策基于使用声明中的可用数据做出决策的任意逻辑。 请记住，对于 RBAC，仅使用角色类型声明。 角色类型声明用于检查用户是否属于特定角色。 若要阐释使用基于声明的授权方法做出授权决策的过程，请考虑以下步骤：  
  
1.  应用程序收到要求对用户进行身份验证的请求。  
  
2.  WIF 将用户重定向到其标识提供程序，在对用户进行身份验证后，使用关联的安全令牌（表示包含有关声明的用户）发出应用程序请求。 WIF 将这些声明与表示用户的主体相关联。  
  
3.  应用程序将声明传递给决策逻辑机制。 它可以是内存中的代码、对 Web 服务的调用、对数据库的查询、复杂的规则引擎或使用 ClaimsAuthorizationManager。  
  
4.  决策机制根据声明计算结果。  
  
5.  如果结果为 true，则授予访问权；如果结果为 false，则拒绝访问。 例如，规则可能是年龄为 21 岁或以上且居住在华盛顿州的用户。  
  
 <xref:System.Security.Claims.ClaimsAuthorizationManager> 有助于在应用程序中具体化基于声明的授权的决策逻辑。 ClaimsAuthorizationManager 是作为 .NET 4.5 的一部分附带的 WIF 组件。 ClaimsAuthorizationManager 允许您拦截传入请求，并实现选定的任何逻辑以根据传入声明做出授权决策。 在需要更改授权逻辑时，这变得非常重要。 在这种情况下，使用 ClaimsAuthorizationManager 将不会影响应用程序的完整性，从而降低了更改导致应用程序错误的可能性。 了解有关如何使用 ClaimsAuthorizationManager 实现基于声明的访问控制的详细信息，请参阅[操作方法：使用 WIF 和 ACS 在声明感知 ASP.NET 应用程序中实现声明授权](http://go.microsoft.com/fwlink/?LinkID=247446)。

