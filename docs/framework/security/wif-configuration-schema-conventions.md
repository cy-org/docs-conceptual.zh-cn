---
title: "WIF 配置架构约定"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f7864356-f72f-4cae-995c-18e0431f8a58
caps.latest.revision: 3
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 092f6f4544e308dae45636f447f75100512a916a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="wif-configuration-schema-conventions"></a>WIF 配置架构约定
本主题讨论 Windows Identity Foundation (WIF) 配置主题中使用的约定并描述 [\<system.identityModel>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 和 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 部分中使用的一些常见功能和属性。  
  
<a name="BKMK_Modes"></a>   
## <a name="modes"></a>模式  
 许多 WIF 配置元素都具有 `mode` 属性。 这一属性通常控制使用哪个类执行进程的特定部分，以及允许哪些配置元素作为当前元素的子元素。 如果配置文件中的元素因模式设置被忽略，会引发配置错误。  
  
<a name="BKMK_TimespanValues"></a>   
## <a name="timespan-values"></a>Timespan 值  
 其中 <xref:System.TimeSpan> 用作属性的类型，请参阅 <xref:System.TimeSpan.Parse%28System.String%29> 方法以查看允许的格式。 此格式符合以下规范。  
  
```  
[ws][-]{ d | [d.]hh:mm[:ss[.ff]] }[ws]  
```  
  
 例如，“30”、“30.00:00”、“30.00:00:00”都表示 30 天，并且“00:05”、“00:05:00”、“0.00:05:00.00”都表示 5 分钟。  
  
<a name="BKMK_CertificateReferences"></a>   
## <a name="certificate-references"></a>证书引用  
 多个元素使用 `<certificateReference>` 元素获取对证书的引用。 引用证书时，可使用以下属性。  
  
|||  
|-|-|  
|`storeLocation`|<xref:System.Security.Cryptography.X509Certificates.StoreLocation> 枚举的一个值：`CurrentUser` 或 `CurrentMachine`。|  
|`storeName`|<xref:System.Security.Cryptography.X509Certificates.StoreName> 枚举的一个值；对此上下文最有用的是 `My` 和 `TrustedPeople`。|  
|`x509FindType`|<xref:System.Security.Cryptography.X509Certificates.X509FindType> 枚举的一个值；对此上下文最有用的是 `FindBySubjectName` 和 `FindByThumbprint`。 若要消除错误的可能性，建议在生产环境中使用 `FindByThumbprint` 类型。|  
|`findValue`|用于查找证书的值，基于 `x509FindType` 属性。 若要消除错误的可能性，建议在生产环境中使用 `FindByThumbprint` 类型。 指定 `FindByThumbPrint` 时，此属性提取一个值，此值是证书指纹的十六进制字符串形式，如：“97249e1a5fa6bee5e515b82111ef524a4c91583f”。|  
  
<a name="BKMK_CustomTypeReferences"></a>   
## <a name="custom-type-references"></a>自定义类型引用  
 多个元素使用 `type` 属性引用自定义类型。 此属性应指定自定义类型的名称。 若要从全局程序集缓存 (GAC) 中引用类型，应使用强名称。 若要从 Bin/ 目录中引用类型，可使用简单的程序集限定的引用。 App_Code/ 目录中定义的类型也可以在没有限定程序集时仅通过指定类型名称引用。  
  
 自定义类型应从指定类型中派生，同时应提供 `public` 默认（0 参数）构造函数。  
  
## <a name="see-also"></a>另请参阅  
 [\<system.identityModel>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md)   
 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)

