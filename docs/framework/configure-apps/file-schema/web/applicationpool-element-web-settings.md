---
title: "&lt;applicationPool&gt; 元素（Web 设置） | Microsoft Docs"
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
  - "<applicationPool> 元素"
  - "applicationPool 元素"
ms.assetid: 46d1baaa-e343-4639-b70d-2a43a9f62b2a
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# &lt;applicationPool&gt; 元素（Web 设置）
指定配置设置，当 ASP.NET 应用程序在 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 或更高版本上以集成模式运行时，ASP.NET 可以使用这些设置来管理进程范围的行为。  
  
> [!IMPORTANT]
>  此元素及其支持的功能仅在 ASP.NET 应用程序承载于 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 或更高版本上时才起作用。  
  
## 语法  
  
```  
<applicationPool   
    maxConcurrentRequestsPerCPU="5000"   
    maxConcurrentThreadsPerCPU="0"   
    requestQueueLimit="5000" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`maxConcurrentRequestsPerCPU`|指定 ASP.NET 允许对每个 CPU 同时发出的请求数。|  
|`maxConcurrentThreadsPerCPU`|指定可为每个 CPU 的单个应用程序池同时运行的线程数。  这提供了一种用于控制 ASP.NET 并发的备选方法，因为您可以限制每个 CPU 为服务请求而允许使用的托管线程的数量。  默认情况下此设置为 0，这表示 ASP.NET 不限制每个 CPU 可创建的线程数量，尽管 CLR 线程池限制了可创建的线程数量。|  
|`requestQueueLimit`|指定在单个进程中可为 ASP.NET 排队的请求的最大数目。  当两个或两个以上的 ASP.NET 应用程序在单个应用程序池中运行时，对应用程序池中的任何应用程序所发出的请求的累积集受此设置的制约。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<system.web\>](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)|包含有关 ASP.NET 如何与宿主应用程序进行交互的信息。|  
  
## 备注  
 在以集成模式运行 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 或更高版本时，利用此元素组合，可以配置当应用程序承载于 IIS 应用程序池中时，ASP.NET 管理线程和对请求进行排队的方式。  如果运行 IIS 6 或以经典模式或 ISAPI 模式运行 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)]，则将忽略这些设置。  
  
 `applicationPool` 设置适用于在特定版本的 .NET Framework 上运行的所有应用程序池。  这些设置包含在 aspnet.config 文件中。  对于版本 2.0 和版本 4 的 .NET Framework，有一个版本的此文件适用。（版本 3.0 和版本 3.5 的 .NET Framework 与版本 2.0 的 .NET Framework 共享 aspnet.config 文件。）  
  
> [!IMPORTANT]
>  如果在 [!INCLUDE[win7](../../../../../includes/win7-md.md)] 上运行 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)]，则可以为每个应用程序池配置单独的 aspnet.config 文件。  这样做可让您为每个应用程序池调整线程的性能。  
  
 对于 `maxConcurrentRequestsPerCPU` 设置，[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 中的默认设置“5000”可有效关闭由 ASP.NET 控制的请求限制，除非每个 CPU 实际拥有的请求数为 5000 或更多。  默认设置改为依赖于 CLR 线程池来自动管理每个 CPU 的并发。  对于大量使用异步请求处理的应用程序或具有很多在网络 I\/O 上阻塞长时间运行的请求的应用程序，增大 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 中的默认限制将使它们受益。  将 `maxConcurrentRequestsPerCPU` 设置为零将禁止使用托管线程来处理 ASP.NET 请求。  当应用程序在 IIS 应用程序池中运行时，请求将停留在 IIS I\/O 线程上，从而使并发受到 IIS 线程设置的限制。  
  
 `requestQueueLimit` 设置的工作方式与 [processModel](http://msdn.microsoft.com/zh-cn/4b8fe20e-74c8-4566-b72c-ce5f83c8e32d) 元素的 `requestQueueLimit` 特性的工作方式相同，该特性是在 ASP.NET 应用程序的 Web.config 文件中设置的。  但 aspnet.config 文件中的 `requestQueueLimit` 设置会重写 Web.config 文件中的 `requestQueueLimit` 设置。  换言之，如果同时设置了这两个特性（默认情况下为此情形），则 aspnet.config 文件中的 `requestQueueLimit` 设置优先。  
  
## 示例  
 下面的示例演示在以下环境中，如何在 aspnet.config 文件中配置 ASP.NET 进程范围的行为：  
  
-   应用程序承载于 [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 应用程序池中。  
  
-   [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 正在以集成模式运行。  
  
-   应用程序使用的是 [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] 或更高版本。  
  
 该示例中的值均为默认值。  
  
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
 [\<system.web\> 元素（Web 设置）](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)