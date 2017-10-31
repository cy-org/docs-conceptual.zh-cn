---
title: "使用 ServiceThrottlingBehavior 控制 WCF 服务性能 | Microsoft Docs"
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
  - "行为 [WCF]，服务性能"
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 使用 ServiceThrottlingBehavior 控制 WCF 服务性能
<xref:System.ServiceModel.Description.ServiceThrottlingBehavior>类公开的属性可用于限制实例数，或在应用程序级别上创建会话。 使用此行为，您可以精细调整 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序的性能。  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a>控制服务实例和并发调用  
 使用<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>属性指定的最大活动处理整个消息数<xref:System.ServiceModel.ServiceHost>类，和<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>属性来指定最大数目<xref:System.ServiceModel.InstanceContext>服务中的对象。  
  
 因为确定这些属性的设置通常发生在之后运行针对应用程序的实际经验加载时，设置<xref:System.ServiceModel.Description.ServiceThrottlingBehavior>属性通常指定在应用程序配置文件中使用[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/servicethrottling.md)元素。  
  
 下面的代码示例演示如何使用<xref:System.ServiceModel.Description.ServiceThrottlingBehavior>设置的应用程序配置文件中的类<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>， <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>，和<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>属性设置为 1 作为最小示例。 实际体验确定任何特定应用程序的最佳设置。  
  
 <!-- TODO: review snippet reference [!code-csharp[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  -->  
  
 确切的运行时行为取决于的值<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>和<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>属性，控制多少条消息可操作内执行的上一次以及服务的生存期<xref:System.ServiceModel.InstanceContext>有关传入通道会话，分别。  
  
 有关详细信息，请参阅<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>，和<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>   
 <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>