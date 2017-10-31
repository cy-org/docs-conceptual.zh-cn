---
title: "AspNetRouteIntegration | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0638ce0e-d053-47df-a447-688e447a03fb
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# AspNetRouteIntegration
此示例演示如何使用 ASP.NET 路由来承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 服务。[基本资源服务](../../../../docs/framework/wcf/samples/basic-resource-service.md) 示例演示此方案的自承载版本，并深入讨论服务实现。本主题重点介绍 ASP.NET 集成功能。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] ASP.NET 路由的更多信息，请参见 <xref:System.Web.Routing>。  
  
## 示例详细信息  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务以面向资源的\/REST 方式公开客户集合。与基于 SOAP 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务一样，该服务可使用 .svc 文件在 ASP.NET 中承载。但是，这通常不是 HTTP 方案的首选，因为它要求该服务的 URL 中有 .svc。此外，它还需要与服务库一起部署 .svc 文件。通过使用 ASP.NET 路由承载该服务，可以避免这些限制，如此示例中所演示。  
  
 此示例通过在 Global.asax 文件中添加 <xref:System.ServiceModel.Activation.ServiceRoute> 而在 ASP.NET 中承载该服务。<xref:System.ServiceModel.Activation.ServiceRoute> 指定服务的类型（此例中为“Service”）、用于该服务的服务主机工厂的类型（此例中为 <xref:System.ServiceModel.Activation.WebServiceHostFactory>）和该服务的 HTTP 基址（此例中为“~\/Customers”）。  
  
 除此之外，此示例还包含一个用于添加 <xref:System.Web.Routing.UrlRoutingModule>（用于打开 ASP.NET 路由）的 Web.config，并包含该服务的配置。特别是，该配置使用 <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> 设置为 `true` 的默认 <xref:System.ServiceModel.Description.WebHttpEndpoint>来配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构在 `http://localhost/Customers/help` 上创建一个基于 HTML 的自动帮助页，该帮助页提供有关如何构造该服务的 HTTP 请求以及如何访问该服务的 HTTP 响应的信息 – 例如，有关如何以 XML 和 JSON 表示客户详细信息的示例。  
  
 通过以这种方式公开客户集合（一般来说是任何资源），客户端可以使用 URI 和 HTTP `GET`、`PUT`、`DELETE` 和 `POST` 以一种统一的方式与服务进行交互。  
  
 客户端项目中的 Program.cs 演示如何使用 <xref:System.Net.HttpWebRequest> 来创作这种客户端。请注意，这只是访问 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的一种方式。还可以使用其他 .NET Framework 类（如 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道工厂和 <xref:System.Net.WebClient>）来访问该服务。SDK 中的其他示例（如[基本 HTTP 服务](../../../../docs/framework/wcf/samples/basic-http-service.md)示例和[自动格式选择](../../../../docs/framework/wcf/samples/automatic-format-selection.md)示例）演示如何使用这些类与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务进行通信。  
  
 此示例由 3 个项目组成：  
  
 服务  
 一个 Web 应用程序项目，它包含在 ASP.NET 中承载的 WCF HTTP 服务。  
  
 客户端  
 一个对服务进行调用的控制台应用程序项目。  
  
 公共  
 一个共享库，它包含客户端和服务使用的 `Customer` 类型。在客户端控制台应用程序运行时，客户端会向服务发出请求，并将响应中的相关信息写入控制台窗口。  
  
#### 使用此示例  
  
1.  打开 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中 ASP.NET 路由集成示例解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  如果它尚未打开，请按“Ctrl\+W, S”打开**“解决方案资源管理器”**窗口。  
  
4.  在**“解决方案资源管理器”**中，右击**“服务”**项目，将光标放在**“调试”**上下文菜单选项上以显示**“启动新实例”**上下文菜单，然后选择**“启动新实例”**。这将启动承载该服务的 ASP.NET 开发服务器。  
  
5.  在**“解决方案资源管理器”**中，右击**“客户端”**项目，将光标放在**“调试”**上下文菜单选项上以显示**“启动新实例”**上下文菜单，然后选择**“启动新实例”**。  
  
6.  出现客户端控制台窗口，该窗口提供了正在运行的服务的 URI，以及该服务的 HTML 帮助页的 URI。可随时通过在浏览器中键入 HTML 帮助页的 URI 来查看该帮助页。在示例运行时，客户端将写入当前活动的状态。  
  
7.  按任意键可终止客户端控制台应用程序。  
  
8.  按 Shift\+F5 可停止调试服务，在 Windows 通知区域右击 ASP.NET 开发服务器图标，然后从上下文菜单中选择**“停止”**。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Web\AspNetRouteIntegration`  
  
## 请参阅