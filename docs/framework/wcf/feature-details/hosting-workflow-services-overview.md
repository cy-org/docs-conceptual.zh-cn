---
title: "承载工作流服务概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19f3704f-06bf-4eeb-8724-5224e02d7ead
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 承载工作流服务概述
工作流服务必须进行承载才能执行。<xref:System.ServiceModel.WorkflowServiceHost> 是现成的工作流主机，可支持多个实例、配置和 WCF 消息传递（虽然工作流无需使用消息传递即可进行承载）。它还通过一组服务行为集成了持久性、跟踪和实例控件。正如 WCF 的 <xref:System.ServiceModel.ServiceHost> 一样，<xref:System.ServiceModel.WorkflowServiceHost> 可以在任何托管 .NET 应用程序中自承载，或是在 IIS\/WAS 中进行 Web 承载（作为 .xamlx 文件）。本节中的主题描述如何承载工作流服务。  
  
## 本节内容  
 [承载工作流服务](../../../../docs/framework/wcf/feature-details/hosting-workflow-services.md)  
 描述承载工作流服务。  
  
 [工作流服务主机内部机制](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)  
 描述 <xref:System.ServiceModel.WorkflowServiceHost> 如何处理传入消息。  
  
 [工作流服务主机可扩展性](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)  
 描述如何扩展工作流服务主机的功能。  
  
 [工作流控制终结点](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)  
 描述如何定义使您可以创建工作流实例的终结点。  
  
 [如何：在 IIS 中承载非服务工作流](../../../../docs/framework/wcf/feature-details/how-to-host-a-non-service-workflow-in-iis.md)  
 演示在 IIS 中承载不是工作流服务的工作流。  
  
 [如何：使用 Windows Server App Fabric 承载工作流服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-workflow-service-with-windows-server-app-fabric.md)  
 演示如何在 Windows Server App Fabric 中承载现有工作流服务。  
  
 [配置 WorkflowServiceHost](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)  
 描述如何控制持久性、跟踪、空闲和未经处理的异常行为。  
  
## 参考  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
 <xref:System.ServiceModel.Activities.WorkflowService>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>  
  
 <xref:System.ServiceModel.Activation.WorkflowServiceHostFactory>  
  
## 相关章节  
 [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)