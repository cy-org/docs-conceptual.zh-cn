---
title: "&lt;system.web&gt; 元素（Web 设置） | Microsoft Docs"
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
  - "<system.Web> 元素"
  - "ASP.NET 配置系统"
  - "配置文件 [ASP.NET]"
  - "system.Web 元素"
  - "Web.config 配置文件 [ASP.NET]"
ms.assetid: 24c4cf4f-ad32-42b2-b040-8e4549e2855e
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# &lt;system.web&gt; 元素（Web 设置）
包含有关 ASP.NET 承载层如何管理进程范围的行为的信息。  
  
## 语法  
  
```  
<system.web>  
</system.web>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<applicationPool\>](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)|在 aspnet.config 文件中指定 IIS 应用程序池的配置设置。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|指定公共语言运行时和 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 应用程序所使用的每个配置文件中的根元素。|  
  
## 备注  
 从 [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] 开始，已将 `system.web` 元素及其子 `applicationPool` 元素添加到 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 中。  在以集成模式运行 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 或更高版本时，利用此元素组合，可以配置当 ASP.NET 承载于 IIS 应用程序池中时，ASP.NET 管理线程以及对请求进行排队的方式。  如果以经典模式或 ISAPI 模式运行 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 或更高版本，则将忽略这些设置。  
  
## 示例  
 下面的示例演示当 ASP.NET 承载于 IIS 应用程序池中时，如何在 aspnet.config 文件中配置 ASP.NET 进程范围的行为。  该示例假定 IIS 正在以集成模式运行，并且应用程序使用的是 [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] 或更高版本。  在 [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] 之前的各个版本的 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 中，此行为不会发生。  该示例中的值均为默认值。  
  
```  
<configuration>  
  <system.web>  
    <applicationPool   
        maxConcurrentRequestsPerCPU="5000"   
        maxConcurrentThreadsPerCPU="0"   
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## 元素信息  
  
|||  
|-|-|  
|命名空间||  
|架构名称||  
|验证文件||  
|可以为空||  
  
## 请参阅  
 [\<applicationPool\> 元素（Web 设置）](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)