---
title: "&lt;bypassTrustedAppStrongNames&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypassTrustedAppStrongNames> 元素"
  - "bypassTrustedAppStrongNames 元素"
  - "强名称跳过功能"
  - "具有强名称的程序集, 加载到信任的应用程序域中"
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# &lt;bypassTrustedAppStrongNames&gt; 元素
指定是否跳过对载入完全信任 <xref:System.AppDomain> 中的完全信任程序集的强名称验证。  
  
## 语法  
  
```  
<bypassTrustedAppStrongNames    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定是否启用避免对完全信任程序集进行强名称验证的跳过功能。  如果启用此功能，则在加载程序集时不验证强名称是否正确。  默认值为 `true`。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`true`|将完全信任程序集载入完全信任 <xref:System.AppDomain> 中时，不验证这些程序集上的强名称签名。  这是默认值。|  
|`false`|将完全信任程序集载入完全信任 <xref:System.AppDomain> 中时，验证这些程序集上的强名称签名。  只检查强名称签名是否正确；不比较它与另一个强名称是否匹配。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 强名称跳过功能可避免对完全信任程序集进行强名称签名验证所产生的开销。  
  
 该跳过功能适用于用强名称签名并具有以下特征的任何程序集：  
  
-   完全受信任而没有 <xref:System.Security.Policy.StrongName> 证据（例如，具有 `MyComputer` 区域证据）。  
  
-   加载到完全受信任的 <xref:System.AppDomain> 中。  
  
-   从该 <xref:System.AppDomain> 的 <xref:System.AppDomainSetup.ApplicationBase%2A> 属性下的位置加载。  
  
-   未经延迟签名。  
  
> [!NOTE]
>  如果已使用注册表项对计算机上的所有应用程序关闭了该跳过功能，则此配置文件设置将无效。  有关更多信息，请参见 [如何：禁用强名称跳过功能](../../../../../docs/framework/app-domains/how-to-disable-the-strong-name-bypass-feature.md)。  
  
## 示例  
 下面的示例演示如何指定对完全信任程序集上的强名称签名进行验证的行为。  
  
```  
<configuration>  
   <runtime>  
      <bypassTrustedAppStrongNames enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [如何：禁用强名称跳过功能](../../../../../docs/framework/app-domains/how-to-disable-the-strong-name-bypass-feature.md)