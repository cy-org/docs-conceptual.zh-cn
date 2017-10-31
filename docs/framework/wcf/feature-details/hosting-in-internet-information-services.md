---
title: "在 Internet 信息服务中承载 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "承载服务 [WCF], IIS"
ms.assetid: ddae14e8-143c-442d-b660-2046809b2d43
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 在 Internet 信息服务中承载
若要承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务，一种选择是在 Internet 信息服务 \(IIS\) 应用程序内部承载。  此承载模型与 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 和 ASP.NET Web 服务 \(ASMX\) 使用的模型类似。  
  
## IIS 的版本  
 可以在下列操作系统上的以下 IIS 版本上承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]：  
  
-   [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] 上的 IIS 5.1。  此环境对于设计和开发 IIS 承载的应用程序非常有用，这些应用程序稍后将部署在 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 等服务器操作系统上。  
  
-   [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 上的 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 提供了一种高级进程模型，这种模型可提供更好的可伸缩性、可靠性和应用程序隔离。  此环境适合对以独占方式使用 HTTP 通信的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务进行成品部署。  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)] 和 [!INCLUDE[lserver](../../../../includes/lserver-md.md)] 上的 IIS 7.0。  IIS 7.0 提供了与 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 相同的高级进程模型，但它使用 Windows 进程激活服务 \(WAS\) 来允许通过 HTTP 之外的协议进行激活和网络通信。  此环境适合开发可通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的任何网络协议（包括 HTTP、net.tcp、net.pipe 和 net.msmq）进行通信的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] WAS 的更多信息，请参见[在 Windows 进程激活服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)。  
  
-   [Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=196496)（可能为英文网页）与 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 和 Windows 进程激活服务 \(WAS\) 一起工作，为 NET4 WCF 和 WF 服务提供丰富的应用程序宿主环境。  这些优点包括进程生命周期管理、进程回收、共享承载、快速失败保护、进程孤立、按需激活和运行状况监视。  有关详细信息，请参见 [AppFabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=196494)（可能为英文网页）和 [AppFabric 承载概念](http://go.microsoft.com/fwlink/?LinkId=196495)（可能为英文网页）。  
  
## IIS 承载的好处  
 在 IIS 中承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务具有以下几个好处：  
  
-   可像处理其他任何类型的 IIS 应用程序（包括 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序和 ASMX）一样，部署和管理 IIS 中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
-   IIS 提供进程激活、运行状况管理和回收功能以提高承载的应用程序的可靠性。  
  
-   像 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 一样，[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以利用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 共享宿主模型。在此模型中，多个应用程序驻留在一个公共辅助进程中以提高服务器密度和可伸缩性。  
  
-   IIS 中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务与 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 使用相同的动态编译模型，该模型简化了承载的服务的开发和部署。  
  
 当决定在 IIS 中承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务时，一定要记住 IIS 5.1 和 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 仅限于 HTTP 通信。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]选择宿主环境的更多信息，请参见[承载服务](../../../../docs/framework/wcf/hosting-services.md)。  
  
## 部署 IIS 承载的 WCF 服务  
 开发和部署 IIS 承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务由以下任务组成：  
  
-   请确保正确安装和注册 IIS、ASP.NET、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] HTTP 激活组件。  
  
-   创建新的 IIS 应用程序，或重新使用现有的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序。  
  
-   为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务创建 .svc 文件。  
  
-   将服务实现部署到 IIS 应用程序。  
  
-   配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
 有关上述每一项任务的讨论，请参见[部署承载于 Internet 信息服务中的 WCF 服务](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)。  
  
## WCF 服务和 ASP.NET  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务既可以与 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 并行承载，也可以在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 兼容模式中承载。在该模式下，服务可以充分利用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序平台提供的功能。  有关这些功能的讨论，请参见 [WCF 服务和 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)。  
  
## 请参阅  
 [使用 ServiceHostFactory 扩展宿主](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)   
 [部署承载于 Internet 信息服务中的 WCF 服务](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)   
 [WCF 服务和 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)   
 [Internet 信息服务承载最佳实践](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)   
 [为 Windows Communication Foundation 配置 Internet Information Services 7.0](../../../../docs/framework/wcf/feature-details/configuring-iis-for-wcf.md)   
 [Windows Server App Fabric 承载功能 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=201276)