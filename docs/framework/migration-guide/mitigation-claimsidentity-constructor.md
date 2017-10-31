---
title: "缓解：ClaimsIdentity 构造函数"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 946903f1-0fbf-4f67-805b-1eb48352024d
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a50cbd69aa1f2c72adc9fc4d10a070f5faa0cf54
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-claimsidentity-constructor"></a>缓解：ClaimsIdentity 构造函数
自 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 起，<xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=fullName> 构造函数设置 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=fullName> 属性的方式有所更改。 如果 <xref:System.Security.Principal.IIdentity> 参数是 <xref:System.Security.Claims.ClaimsIdentity> 对象，且该 <xref:System.Security.Claims.ClaimsIdentity> 对象的 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A> 属性不为 `null`，则 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A> 属性是使用 <xref:System.Security.Claims.ClaimsIdentity.Clone%2A?displayProperty=fullName> 方法附加的。 在 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 中，<xref:System.Security.Claims.ClaimsIdentity.Actor%2A> 属性以现有引用的形式附加。  
  
## <a name="impact"></a>影响  
 自 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 起，新对象 <xref:System.Security.Claims.ClaimsIdentity> 的 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=fullName> 属性与构造函数 <xref:System.Security.Principal.IIdentity> 参数的 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=fullName> 属性不相等。 在 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 及更低版本中，属性是相等的。  
  
## <a name="mitigation"></a>缓解操作  
 如果不需要此行为，可以在应用程序配置文件中将 `Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity` 开关设置为 `true`，从而还原旧行为。 为此，必须在 web.config 文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加以下内容：  
  
```xml  
<configuration>  
   <runtime>  
      <AppContextSwitchOverrides value="Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity=true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)

