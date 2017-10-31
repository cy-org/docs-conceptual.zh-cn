---
title: "采用 Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49ba71e2-9468-4082-84c5-cf8daf95e34a
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 采用 Windows Communication Foundation
您可以选择使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 来完成新的开发工作，同时继续维护现有的使用 ASP.NET 开发的应用程序。因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的目的是在任何方案中都能成为与使用 .NET Framework 生成的应用程序之间实现成功通信的最佳选择，所以它可以充当以 ASP.NET 无法实现的方式来解决各种软件通信问题的标准工具。  
  
 新的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以和现有的 ASP.NET Web 服务部署在相同的计算机上。如果现有 ASP.NET Web 服务使用的 .NET Framework 版本早于 2.0 版，那么可以借助于 ASP.NET IIS 注册工具，有选择地将 .NET Framework 2.0 部署到将要承载新 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的 IIS 应用程序。[ASP.NET IIS Registration Tool \(Aspnet\_regiis.exe\)](http://go.microsoft.com/fwlink/?LinkId=94687)（ASP.NET IIS 注册工具 \(Aspnet\_regiis.exe\)）中介绍了该工具，并且该工具具有内置于 IIS 6.0 管理控制台中的用户界面。  
  
 使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以将配置为在 ASP.NET 兼容模式下运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务添加到 IIS 中现有的 ASP.NET Web 服务应用程序，从而向现有的 ASP.NET Web 服务中添加新功能。由于采用 ASP.NET 兼容模式，新的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的代码可以通过使用 <xref:System.Web.HttpContext> 类，访问和更新与之前存在的 ASP.NET 代码一样的应用程序状态信息。这些应用程序还可以共享相同的类库。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端可以使用 ASP.NET Web 服务。ASP.NET Web 服务客户端可以使用配置了 <xref:System.ServiceModel.BasicHttpBinding> 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。ASP.NET Web 服务可以和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序共存，甚至可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 向现有的 ASP.NET Web 服务添加功能。在拥有上述所有可以将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 ASP.NET Web 服务一起使用的方法之后，只有在需要 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 能够提供而 ASP.NET Web 服务无法提供的功能时，才需要将 ASP.NET Web 服务迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
 即使在需要进行迁移的少数几种情况下，也请仔细考虑一下，因为将代码从一种技术迁移到另一种技术很少成为一种正确的方法。采用新技术的原因是为了满足早期技术无法满足的新要求。在上述情况下，正确的做法是设计一个新的解决方案来满足刚刚扩展的需求集。新的设计将受益于您对现有系统所拥有的经验以及您自该系统被设计以来获得的智慧。此外，新设计还可以利用新技术的所有功能，而不是在新平台上再现旧设计。在建立新设计的关键元素的原型之后，可以更轻松地在新系统中重用现有系统中的代码。  
  
 对于从 ASP.NET Web 服务移植到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 是正确的解决方案的少数几种情况，下一节提供了一些有关如何实施的指导。其中就如何迁移服务以及如何迁移客户端提出了建议。  
  
 有关针对如何将现有 ASP.NET Web 服务迁移到 WCF 的完整分析，请参见 [ASP.NET Web Services and the Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkID=71761)（ASP.NET Web 服务和 Windows Communication Foundation）。本节介绍如何根据 ASP.NET Web 服务的元数据实现兼容 WCF 服务，以及如何将 ASP.NET Web 服务和客户端代码迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
## 请参阅  
 [如何：检索元数据并实现兼容服务。](../../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)   
 [如何：将 ASP.NET Web 服务代码迁移到 Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/migrate-asp-net-web-service-to-wcf.md)   
 [如何：将 ASP.NET Web 服务客户端代码迁移到 Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/migrate-asp-net-web-service-client-to-wcf.md)