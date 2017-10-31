---
title: "工作流服务概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e536dda3-e286-441e-99a7-49ddc004b646
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# 工作流服务概述
工作流服务是使用工作流实现的基于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的服务。  工作流服务是使用消息传递活动发送和接收 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 消息的工作流。  .NET Framework 4.5 引入了多个消息传递活动，可用于从工作流中发送和接收消息。  有关 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] 消息传递活动以及如何使用这些活动实现不同的消息交换模式，请参阅[消息传递活动](../../../../docs/framework/wcf/feature-details/messaging-activities.md)。  
  
## 使用工作流服务的优势  
 随着应用程序的分布越来越广泛，各服务可负责调用其他服务来减轻工作负载。  作为异步操作实现这些调用会增加代码的复杂性。  错误处理需要处理异常和提供详细跟踪信息，从而进一步增加了这些形式的复杂性。  有些服务经常长时间运行，并且在等待输入时可能会占用宝贵的系统资源。  鉴于这些问题，分布式应用程序往往非常复杂，且难以编写和维护。  工作流很自然地表示异步工作的协调，特别是对外部服务的调用。  工作流也是表示长时间运行的业务流程的有效方式。  正是这些特性使得工作流成为了在分布式环境中生成服务的一笔宝贵财富。  
  
## 实现工作流服务  
 实现 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务时，您可以定义大量描述此服务及其收发的数据的协定。  这些数据表示为数据协定和消息协定。  WCF 和工作流服务均在服务说明中使用数据协定和消息协定定义。  服务自身以 WSDL 形式公开元数据，以便描述服务的操作。  在 WCF 中，服务协定和操作协定定义其支持的服务和操作。  但在工作流服务中，这些协定属于业务流程自身。  它们由称为协定推理的流程在元数据中公开。  使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载工作流服务时，将检查工作流定义，并根据在工作流中找到的消息传递活动集生成协定。  具体而言，是使用下面的活动和属性来生成协定：  
  
 <xref:System.ServiceModel.Activities.Receive> 活动  
  
-   <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.OperationContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.SendReply> 活动  
  
-   <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.SendReply.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动  
  
 协定推理的最终结果是使用与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务和操作协定相同的数据结构的服务说明。  然后，将使用此信息对工作流服务公开 WSDL。  
  
> [!NOTE]
>  [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 禁止使用不带某些附加工具支持的现有协定定义来编写工作流服务。  工作流服务协定由前面讨论的协定推理流程创建。  不过，消息协定和数据协定完全受到支持。  
  
## 工作流服务和基于 MSMQ 的绑定  
 WCF 定义了两个基于 MSMQ 的绑定：<xref:System.ServiceModel.NetMsmqBinding> 和 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>。  基于 MSMQ 的绑定具有长时间运行的性质，因此常常与工作流服务一起使用。  基于 MSMQ 的绑定具有一个 `ValidityDuration` 属性，该属性指定可以假定 MSMQ 消息有效的时间。  由于工作流服务具有长时间运行的性质，因此在工作流服务可以处理 MSMQ 消息之前，该消息可能已过期。  因此，将 MSMQ 绑定的有效期设置为一个适当值非常重要。  必须基于工作流及其对消息的处理方式选择此值。  例如，如果工作流具有一个 <xref:System.ServiceModel.Activities.Receive> 活动，后跟一个需要运行 10 分钟的自定义活动，再后跟另一个 <xref:System.ServiceModel.Activities.Receive> 活动，则 `ValidityDuration` 的正确值将大于 10 分钟。  
  
## 承载工作流服务  
 与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务一样，必须承载工作流服务。   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用 <xref:System.ServiceModel.ServiceHost> 类承载服务，工作流服务使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载服务。  与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务一样，可以通过多种方式承载工作流服务，例如：  
  
-   在托管 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序中。  
  
-   在 Internet Information Services \(IIS\) 中。  
  
-   在 Windows 进程激活服务 \(WAS\) 中。  
  
-   在托管 Windows 服务中。  
  
 托管 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序或托管 Windows 服务中承载的工作流服务创建一个 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 类的实例，并向该实例传递一个在 <xref:System.ServiceModel.Activities.WorkflowService> 属性中包含工作流定义的 <xref:System.ServiceModel.Activities.WorkflowService.Body%2A> 实例。  包含消息传递活动的工作流定义公开为工作流服务。  
  
 若要在 IIS 或 WAS 中承载工作流服务，请将包含工作流服务定义的 .xamlx 文件放置到虚拟目录中。  自动创建默认终结点（使用 <xref:System.ServiceModel.BasicHttpBinding>）[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][简化配置](../../../../docs/framework/wcf/simplified-configuration.md)。  也可以在虚拟目录中放置 Web.config 文件以指定您自己的终结点。  如果您的工作流定义位于程序集中，则可以在虚拟目录中放置一个 .svc 文件，并在 App\_Code 目录中放置该工作流程序集。  该 .svc 文件必须指定服务主机工厂以及实现该工作流服务的类。  下面的示例演示如何指定服务主机工厂以及实现该工作流服务的类。  
  
```  
<%@ServiceHost Factory=" System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory  
Service="EchoService"%>  
```