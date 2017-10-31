---
title: "什么是 Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Windows Communication Foundation (WCF), 技术概述"
  - "技术概述 [WCF]"
  - "WCF [WCF], 技术概述"
ms.assetid: 40e1009d-ef15-450b-9848-62eabe5e5738
caps.latest.revision: 51
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 49
---
# 什么是 Windows Communication Foundation
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 是用于构建面向服务的应用程序的框架。 借助 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]，可以将数据作为异步消息从一个服务终结点发送至另一个服务终结点。 服务终结点可以是由 IIS 承载的持续可用的服务的一部分，也可以是应用程序中承载的服务。 终结点可以是从服务终结点请求数据的服务客户端。 简单消息可以是作为 XML 发送的单个字符或单个单词，复杂消息可以是二进制数据流。 一些示例方案包括：  
  
-   处理企业事务的安全服务。  
  
-   将当前数据提供给其他服务（例如流量报告或其他监视服务）的服务。  
  
-   使两个人能够实时通信或交换数据的聊天服务。  
  
-   轮询一个或多个服务以查找数据并将其以逻辑表现形式展示出来的面板应用程序。  
  
-   将使用 Windows Workflow Foundation 实现的工作流作为 WCF 服务公开。  
  
-   轮询服务以查找最新数据源的 Silverlight 应用程序。  
  
 虽然在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 存在之前就可以创建此类应用程序，但 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 使终结点的开发比以前更容易。 总之，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 设计提供一种用于创建 Web 服务和 Web 服务客户端的可管理的方式。  
  
## WCF 的功能  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包括以下功能集。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 功能详细信息](../../../docs/framework/wcf/feature-details/index.md).  
  
-   **服务导向**  
  
     使用 WS 标准的一个结果是，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 允许您创建面向服务的应用程序。 面向服务的体系结构 \(SOA\) 依赖 Web 服务发送和接收数据。 这些服务具有松耦合的常规优点，而不是从一个应用程序到另一个应用程序进行硬编码。 松耦合关系意味着只要符合基本协定，则在任何平台上创建的任何客户端均可连接到所有服务。  
  
-   **互操作性**  
  
     [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 实现了 Web 服务互操作性的现代行业标准。[!INCLUDE[crabout](../../../includes/crabout-md.md)]支持的标准，请参阅[互操作性和集成](../../../docs/framework/wcf/feature-details/interoperability-and-integration.md)。  
  
-   **多种消息模式**  
  
     采用多种模式之一交换消息。 最常用的模式是请求\/答复模式，其中一个终结点从另一个终结点请求数据， 另一个终结点进行答复。 还有其他模式，比如单向消息，其中只有一个终结点发送消息，而不期望得到答复。 更复杂的模式是双工交换模式，在该模式下，两个终结点建立连接并来回发送数据，类似于即时消息传递程序。[!INCLUDE[crabout](../../../includes/crabout-md.md)]如何使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 实现不同的消息交换模式，请参阅[协定](../../../docs/framework/wcf/feature-details/contracts.md)。  
  
-   **服务元数据**  
  
     [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 支持使用行业标准（如 WSDL、XML 架构和 WS\-Policy）中指定的格式发布服务元数据。 该元数据可用于自动生成并配置客户端，以便访问 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务。 可通过 HTTP 和 HTTPS 来发布元数据，也可使用 Web 服务元数据交换标准来发布元数据。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [元数据](../../../docs/framework/wcf/feature-details/metadata.md).  
  
-   **数据协定**  
  
     由于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 是使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 生成的，因此它也包括代码友好的方法，用于提供希望强制执行的协定。 数据协定就是其中一种通用类型的协定。 实质上，当您使用 Visual C\# 或 Visual Basic 对服务进行编码时，处理数据的最简单方法是使用属于数据实体的属性创建表示该数据实体的类。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包括一个以这种轻松的方式处理数据的综合系统。 在创建了表示数据的类之后，服务会自动生成使客户端能够符合所设计数据类型的元数据。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [使用数据协定](../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
  
-   **安全性**  
  
     可对消息进加密以保护隐私，而且可以要求用户对其自身进行身份验证，然后才允许接收消息。 可使用众所周知的标准（如 SSL 或 WS\-SecureConversation）实现安全性。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [安全性](../../../docs/framework/wcf/feature-details/security.md).  
  
-   **多种传输和编码方式**  
  
     可通过多种内置传输协议和编码中的任意一种发送消息。 最常用的协议和编码是使用超文本传输协议 \(HTTP\) 发送文本编码的 SOAP 消息，以便在万维网上使用。 此外，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 还允许通过 TCP、命名管道或 MSMQ 发送消息。 这些消息可以编码为文本，也可以使用优化的二进制格式。  使用 MTOM 标准可有效地发送二进制数据。 如果所提供的传输或编码都不符合您的需要，您可以创建自己的自定义传输或编码。[!INCLUDE[crabout](../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 支持的传输和编码，请参阅 [传输](../../../docs/framework/wcf/feature-details/transports.md)。  
  
-   **可靠的排队消息**  
  
     [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 支持使用通过 WS\-Reliable Messaging 实现的可靠会话和使用 MSMQ 进行可靠的消息交换。[!INCLUDE[crabout](../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中可靠和排队的消息支持，请参阅[队列和可靠会话](../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md)。  
  
-   **持久性消息**  
  
     持久性消息决不会由于通信中断而丢失。 持久性消息模式的消息会始终保存到数据库中。 如果发生中断，数据库将允许您在恢复连接后恢复消息交换。 此外，也可以使用 [!INCLUDE[wf](../../../includes/wf-md.md)] 来创建持久性消息。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [工作流服务](../../../docs/framework/wcf/feature-details/workflow-services.md).  
  
-   **事务**  
  
     WCF 还使用三个事务模型之一来支持事务：WS\-AtomicTtransactions、<xref:System.Transactions> 命名空间中的 API 以及 Microsoft 分布式事务协调器。[!INCLUDE[crabout](../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中的事务支持，请参阅[事务](../../../docs/framework/wcf/feature-details/transactions-in-wcf.md)。  
  
-   **AJAX 和 REST 支持**  
  
     REST 是不断发展的 Web 2.0 技术的一个示例。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 可以配置为处理未包装在 SOAP 信封中的“纯文本”XML 数据。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 还可以扩展以支持特定的 XML 格式，如 ATOM（流行的 RSS 标准），甚至支持非 XML 格式（如 JavaScript 对象表示法 \(JSON\)）。  
  
-   **扩展性**  
  
     [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 体系结构具有大量扩展点。 如果需要额外功能，它还提供许多入口点，允许您自定义服务的行为。[!INCLUDE[crabout](../../../includes/crabout-md.md)]可用扩展点，请参阅[扩展 WCF](../../../docs/framework/wcf/extending/extending-wcf.md)。  
  
## WCF 与其他 Microsoft 技术的集成  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 是一个灵活的平台。 由于这一极强的灵活性，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 还在 Microsoft 的一些其他产品中得以利用。 如果您也在使用这些产品中的任何产品，通过了解 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 的基础知识，您会立即受益。  
  
 与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配对的第一项技术是 Windows Workflow Foundation \(WF\)。 工作流通过将工作流中的步骤封装为“活动”来简化应用程序开发。 在 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 的第一个版本中，开发人员必须为工作流创建主机。[!INCLUDE[wf2](../../../includes/wf2-md.md)] 的下一版本与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 进行了集成， 从而允许在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务中轻松承载任何工作流；通过在 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 中自动选择 WF\/WCF 作为项目类型可实现此目的。  
  
 Microsoft BizTalk Server R2 还利用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 作为通信技术。 BizTalk 设计用于接收一种标准化格式的数据，然后将其转换为另一种格式。 必须将消息传递到其中央消息框，在这里可以使用严格的映射，也可以通过使用其中一种 BizTalk 功能（如其工作流引擎）来转换消息。 目前，BizTalk 可使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 业务线 \(LOB\) 适配器将消息传递到消息框。  
  
 Microsoft Silverlight 是一个用于创建可互操作的、丰富 Web 应用程序的平台，允许开发人员创建媒体密集的网站（如流视频）。 从版本 2 开始，Silverlight 加入了 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 作为通信技术，以将 Silverlight 应用程序连接到 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 终结点。  
  
 [!INCLUDE[dublin](../../../includes/dublin-md.md)] 应用程序服务器是针对部署和管理使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 进行通信的应用程序专门生成的。[!INCLUDE[dublin2](../../../includes/dublin2-md.md)] 包括丰富的工具和配置选项，专门设计用于启用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 的应用程序。  
  
## 请参阅  
 <xref:System.ServiceModel>   
 [Windows Communication Foundation 基础概念](../../../docs/framework/wcf/fundamental-concepts.md)   
 [Windows Communication Foundation 体系结构](../../../docs/framework/wcf/architecture.md)   
 [准则与最佳做法](../../../docs/framework/wcf/guidelines-and-best-practices.md)   
 [入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [文档指南](../../../docs/framework/wcf/guide-to-the-documentation.md)   
 [基本 WCF 编程](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Windows Communication Foundation Samples](http://msdn.microsoft.com/zh-cn/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)