---
title: "&lt;appDomainResourceMonitoring&gt; 元素 | Microsoft Docs"
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
  - "<appDomainResourceMonitoring> 元素"
  - "appDomainResourceMonitoring 元素"
ms.assetid: 02119ab6-1e91-448e-97ad-e7b2e5c4bbbd
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# &lt;appDomainResourceMonitoring&gt; 元素
指示运行时在进程的生存期内收集有关进程中所有应用程序域的统计信息。  
  
## 语法  
  
```  
<appDomainResourceMonitoring    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否收集有关应用程序域资源监控的统计信息。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`true`|收集有关应用程序域资源监控的统计信息。|  
|`false`|不收集有关应用程序域资源监控的统计信息。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 通过托管应用程序域类、承载 [ICLRAppDomainResourceMonitor](../../../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md) 接口和 Windows 事件跟踪 \(ETW\)，可提供应用程序域资源监控。  在启用监控后，在进程的生存期内将收集有关进程中所有应用程序域的统计信息。  
  
 若要通过托管代码启用监控，请使用 <xref:System.AppDomain.MonitoringIsEnabled%2A> 属性。  
  
 此配置元素仅在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]和更高版本中可用。  
  
## 示例  
 下面的示例演示如何启用应用程序域资源监控。  
  
```  
<configuration>  
   <runtime>  
      <appDomainResourceMonitoring enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName>   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)