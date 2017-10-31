---
title: "&lt;generatePublisherEvidence&gt; 元素 | Microsoft Docs"
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
  - "<generatePublisherEvidence> 元素"
  - "generatePublisherEvidence 元素"
ms.assetid: 7d208f50-e8d5-4a42-bc1a-1cf3590706a8
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# &lt;generatePublisherEvidence&gt; 元素
指定运行时是否为代码访问安全性 \(CAS\) 创建 <xref:System.Security.Policy.Publisher> 证据。  
  
## 语法  
  
```  
<generatePublisherEvidence    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否创建 <xref:System.Security.Policy.Publisher> 证据。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|不会创建 <xref:System.Security.Policy.Publisher> 证据。|  
|`true`|创建 <xref:System.Security.Policy.Publisher> 证据。  这是默认设置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 和更高版本中，此元素对程序集加载时间没有影响。  有关更多信息，请参见 [安全更改](../../../../../docs/framework/security/security-changes.md)中的“安全策略简化”一节。  
  
 公共语言运行时 \(CLR\) 尝试在加载时验证 Authenticode 签名，以便为程序集创建 <xref:System.Security.Policy.Publisher> 证据。  但在默认情况下，大部分应用程序都不需要 <xref:System.Security.Policy.Publisher> 证据。  标准的 CAS 策略不依赖于 <xref:System.Security.Policy.PublisherMembershipCondition>。  除非在使用自定义 CAS 策略的计算机上执行应用程序或者应用程序要满足部分信任环境中对 <xref:System.Security.Permissions.PublisherIdentityPermission> 的要求，否则应避免与验证发行者签名相关的不必要的启动成本。（在完全受信任的环境中，标识权限的要求总是会成功。）  
  
> [!NOTE]
>  建议服务使用 `<generatePublisherEvidence>` 元素来改进启动性能。使用此元素还有助于避免会导致超时和取消服务启动的延迟。  
  
## 配置文件  
 此元素只可用于应用程序配置文件中。  
  
## 示例  
 下面的示例演示如何使用 `<generatePublisherEvidence>` 元素为应用程序禁用 CAS 发行者策略检查。  
  
```  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)