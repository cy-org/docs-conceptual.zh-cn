---
title: "ASP.NET 缓存集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ASP.NET 缓存集成
此示例演示如何通过 WCF WEB HTTP 编程模型使用 ASP.NET 输出缓存。  请参见[基本资源服务](../../../../docs/framework/wcf/samples/basic-resource-service.md)示例，该示例是此方案的自承载版本，深入讨论了服务实现。  本主题重点介绍 ASP.NET 输出缓存集成功能。  
  
## 演示  
 与 ASP.NET 输出缓存的集成  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`  
  
## 讨论  
 该示例使用 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>，以通过 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务来利用 ASP.NET 输出缓存。  <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 应用于服务操作，并在应该应用于给定操作的响应的配置文件中提供缓存配置文件的名称。  
  
 在示例服务项目的 Service.cs 文件中，`GetCustomer` 和 `GetCustomers` 操作都使用 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 进行了标记，这可提供缓存配置文件名称“CacheFor60Seconds”。  在服务项目的 Web.config 文件中，\<`system.web`\> 的 \<`caching`\> 元素下提供了缓存配置文件“CacheFor60Seconds”。  对于此缓存配置文件，`duration` 特性的值为“60”，因此与此配置文件关联的响应在 ASP.NET 输出缓存中缓存 60 秒。  此外，对于此缓存配置文件，`varmByParam` 特性设置为“format”，因此具有不同 `format` 查询字符串参数值的请求会分别缓存其响应。  最后，缓存配置文件的 `varyByHeader` 特性设置为“Accept”，因此具有不同 Accept 标头值的请求会分别缓存其响应。  
  
 客户端项目中的 Program.cs 演示如何使用 <xref:System.Net.HttpWebRequest> 编写此类客户端。  请注意，这只是访问 WCF 服务的一种方式。  还可以使用其他 .NET Framework 类（如 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道工厂和 <xref:System.Net.WebClient>）来访问该服务。  SDK 中的其他示例（如[基本 HTTP 服务](../../../../docs/framework/wcf/samples/basic-http-service.md)示例和[自动格式选择](../../../../docs/framework/wcf/samples/automatic-format-selection.md)示例）演示如何使用这些类与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务通信。  
  
## 运行示例  
 该示例由三个项目组成：  
  
-   **服务**：一个 Web 应用程序项目，它包含在 ASP.NET 中承载的 WCF HTTP 服务。  
  
-   **客户端**：一个对服务进行调用的控制台应用程序项目。  
  
-   **通用**：一个共享库，包含客户端和服务使用的客户类型。  
  
 在客户端控制台应用程序运行时，客户端会对服务进行请求，并将响应中的相关信息写入控制台窗口。  
  
#### 运行示例  
  
1.  打开 ASP.NET 缓存集成示例的解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  如果尚未打开**“解决方案资源管理器”**窗口，请按 Ctrl\+W\+S。  
  
4.  在**“解决方案资源管理器”**窗口中，右击**“服务”**项目，然后选择**“启动新实例”**。  这将启动承载服务的 ASP.NET 开发服务器。  
  
5.  在**“解决方案资源管理器”**窗口中，右击**“客户端”**项目，然后选择**“启动新实例”**。  
  
6.  出现客户端控制台窗口，该窗口提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。  可随时通过在浏览器中键入 HTML 帮助页的 URI 来查看该帮助页。  
  
7.  在示例运行时，客户端将写入当前活动的状态。  
  
8.  按任意键可终止客户端控制台应用程序。  
  
9. 按 Shift\+F5 可停止调试服务。  
  
10. 在 Windows 通知区域中，右击 ASP.NET 开发服务器图标，然后选择**“停止”**。