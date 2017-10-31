---
title: "如何：与 WCF 终结点和消息队列应用程序交换消息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62210fd8-a372-4d55-ab9b-c99827d1885e
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 如何：与 WCF 终结点和消息队列应用程序交换消息
通过使用 MSMQ 集成绑定，可以将现有消息队列 (MSMQ) 应用程序与 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序进行集成，从而在 MSMQ 消息与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息之间进行转换。 利用这一功能，可以在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端调用 MSMQ 接收方应用程序，也可以在 MSMQ 发送方应用程序中调用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
 在此部分中，我们将介绍如何使用<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>之间的排队通信 （1)[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端和使用 System.Messaging 以及 （2） MSMQ 应用程序客户端编写的 MSMQ 应用程序服务和一个[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务。  
  
 有关演示如何调用中的 MSMQ 接收方应用程序的完整示例[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端，请参阅[Windows Communication Foundation 到消息队列](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md)示例。  
  
 有关完整示例，演示如何调用[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]负责将服务从 MSMQ 客户端，请参阅[消息队列 Windows Communication foundation](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md)示例。  
  
### <a name="to-create-a-wcf-service-that-receives-messages-from-a-msmq-client"></a>创建从 MSMQ 客户端接收消息的 WCF 服务  
  
1.  定义一个接口，该接口为从 MSMQ 发送方应用程序接收排队消息的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务定义服务协定，如下面的示例代码所示。  
  
     [!code-csharp[S_MsmqToWcf#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmqtowcf/cs/service.cs#1)]
     [!code-vb[S_MsmqToWcf#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmqtowcf/vb/service.vb#1)]  
  
2.  实现接口，并且应用<xref:System.ServiceModel.ServiceBehaviorAttribute>属性类，如下面的代码示例中所示。  
  
     [!code-csharp[S_MsmqToWcf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmqtowcf/cs/service.cs#2)]
     [!code-vb[S_MsmqToWcf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmqtowcf/vb/service.vb#2)]  
  
3.  创建指定一个配置文件<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>。  
  
  
  
4.  实例化<xref:System.ServiceModel.ServiceHost>使用配置的绑定的对象。  
  
  
  
### <a name="to-create-a-wcf-client-that-sends-messages-to-a-msmq-receiver-application"></a>创建向 MSMQ 接收方应用程序发送消息的 WCF 客户端  
  
1.  定义一个接口，该接口为向 MSMQ 接收方发送排队消息的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端定义服务协定，如下面的示例代码所示。  
  
     [!code-csharp[S_WcfToMsmq#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/proxy.cs#6)]
     [!code-vb[S_WcfToMsmq#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/proxy.vb#6)]  
  
2.  定义一个客户端类，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端使用该类来调用 MSMQ 接收方。  
  
     [!code-csharp[S_WcfToMsmq#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/snippets.cs#2)]
     [!code-vb[S_WcfToMsmq#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/snippets.vb#2)]  
  
3.  创建一个配置文件，在该配置文件中指定 MsmqIntegrationBinding 绑定的用法。  
  
     [!code-csharp[S_WcfToMsmq#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/snippets.cs#3)]
     [!code-vb[S_WcfToMsmq#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/snippets.vb#3)]  
  
4.  创建该客户端类的一个实例，并调用消息接收服务所定义的方法。  
  
     [!code-csharp[S_WcfToMsmq#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/client.cs#4)]  
  
## <a name="see-also"></a>另请参阅  
 [队列概述](../../../../docs/framework/wcf/feature-details/queues-overview.md)   
 [如何︰ 使用 WCF 终结点交换排队消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)   
 [Windows Communication Foundation 到消息队列](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md)   
 [安装消息队列 (MSMQ)](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md)   
 [Windows Communication Foundation 到消息队列](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md)   
 [基于消息队列的消息安全性](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)