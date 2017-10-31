---
title: "将 ASP.NET Web 服务迁移到 WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1adbb931-f0b1-47f3-9caf-169e4edc9907
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 将 ASP.NET Web 服务迁移到 WCF
ASP.NET 提供 .NET Framework 类库和工具，用于生成网站\/网页服务，以及承载服务内 Internet 信息服务 \(IIS\) 的设施。[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供了 .NET Framework 和工具的承载设施，使软件实体使用任何协议，包括使用的网站\/网页服务通信。将 ASP.NET Web 服务迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以让应用程序充分利用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 特有的新功能和改进。  
  
 对于 ASP.NET Web 服务，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 具有多个重要优势。ASP.NET Web 服务工具仅用于生成 Web 服务，如果必须使软件实体之间相互通信，则可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的工具。这会减少开发人员为适应不同软件通信方案而必需了解的技术的数量，从而降低软件开发资源的成本及完成软件开发项目所需的时间。  
  
 即使对于 Web 服务开发项目，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的 Web 服务协议也比 ASP.NET Web 服务支持的协议多。这些附加协议提供更完善的解决方案，涉及可靠会话和事务等其他内容。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的消息传输协议比 ASP.NET Web 服务支持的协议更多。ASP.NET Web 服务仅支持使用超文本传输协议 \(HTTP\) 发送消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通过使用 HTTP，以及传输控制协议 \(TCP\)，命名管道和 Microsoft 消息队列（消息队列）发送邮件的支持。更重要的是，可以扩展 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 以支持其他传输协议。因此，使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 开发的软件适合于与更广泛的其他软件一起使用，从而提高潜在的投资回报。  
  
 与 ASP.NET Web 服务相比，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的用于部署和管理应用程序的工具要多得多。除了 ASP.NET 也具有的配置系统外，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还提供配置编辑器、通过任意数目的媒介在发送方和接收方之间来回进行的活动跟踪、跟踪查看器、消息日志记录、大量性能计数器和对 Windows Management Instrumentation 的支持。  
  
 对于 ASP.NET Web 服务，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 具有这些潜在的好处，如果您正在使用或正在考虑使用 ASP.NET Web 服务，您可以进行以下几种选择：  
  
-   继续使用 ASP.NET Web 服务，放弃 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的好处。  
  
-   继续使用 ASP.NET Web 服务，并打算在未来的某时采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。本节中的主题说明如何最大化与未来 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序一起使用新 ASP.NET Web 服务应用程序的前景。本节中的主题还说明如何生成新的 ASP.NET Web 服务以便于将这些服务迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。不过，如果必须要保证服务的安全，或者需要可靠性或事务保证，或者必须构造自定义管理工具，则最好选择采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 正是为这样的方案而设计的。  
  
-   采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 以进行新开发，同时继续保持现有的 ASP.NET Web 服务应用程序。这种选择很可能是最佳选择。它提供 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的好处，同时可节省修改现有应用程序的成本。在这种方案中，新的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以与现有 ASP.NET 应用程序共存。新 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序将能够使用现有的 ASP.NET Web 服务，并且可以借助于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ASP.NET 兼容模式使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将新操作功能编程到现有的 ASP.NET 应用程序中。  
  
-   采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 并将现有 ASP.NET Web 服务应用程序迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。您可以选择此选项以增强现有的应用程序，使其具有 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的功能，或者在新的、功能更强大的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中重现现有 ASP.NET Web 服务的功能。  
  
> [!NOTE]
>  如果 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务由 IIS 5.x 承载，则在卸载 ASP.NET 时必须小心。如果 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务由 IIS 5.x 承载，则在卸载 ASP.NET 时，可能会请求该服务的代码。在已卸载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的情况下，在运行 IIS 5.x 的操作系统上卸载 ASP.NET 时，会将带有 .svc 扩展名的文件视为文本文件，其内容（包括任何源代码）会返回给请求者。  
  
 本节详细说明这些选项，将 ASP.NET Web 服务与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 进行对比，并提供有关如何将 ASP.NET Web 服务代码迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的说明。  
  
## 请参阅  
 [Windows Communication Foundation 使用展望：使未来迁移轻而易举](../../../../docs/framework/wcf/feature-details/anticipating-adopting-wcf-migration.md)   
 [预期采用 Windows Communication Foundation：便于以后集成](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)   
 [采用 Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/adopting-wcf.md)   
 [基于目标和使用的标准比较 ASP.NET Web 服务与 WCF](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)   
 [从开发的角度比较 ASP.NET Web 服务与 WCF](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)