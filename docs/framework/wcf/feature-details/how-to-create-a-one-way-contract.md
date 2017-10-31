---
title: "如何：创建单向协定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 如何：创建单向协定
本主题演示了创建使用单向协定的方法所需的基本步骤。这些方法从客户端调用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务上的操作但不期待答复。例如，可以使用这种类型的协定将通知发布给许多订户。在创建双工（双向）协定（可使得客户端和服务器可以独立地相互通信，这样双方都可以启动对另一方的呼叫）时，还可以使用单向协定。具体而言，这样做可允许服务器对客户端进行单向呼叫，而客户端可以将这些呼叫视为事件。有关指定单向方法的详细信息，请参见 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 属性和 <xref:System.ServiceModel.OperationContractAttribute> 类。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建用于双工协定的客户端应用程序的更多信息，请参见[如何：使用单向和请求\-答复协定访问服务](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)。有关可运行的示例，请参见[单向](../../../../docs/framework/wcf/samples/one-way.md)示例。  
  
### 创建单向协定  
  
1.  通过将 <xref:System.ServiceModel.ServiceContractAttribute> 类应用到定义服务将要实现的方法的接口，创建服务协定。  
  
2.  通过将 <xref:System.ServiceModel.OperationContractAttribute> 类应用到相应的方法，指示客户端可以调用接口中的哪些方法。  
  
3.  通过将 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 属性设置为 `true`，可将不得具有输出（没有返回值且没有 out 参数或 ref 参数）的操作指定为单向操作。注意，默认情况下，使用 <xref:System.ServiceModel.OperationContractAttribute> 类的操作都满足请求\-答复协定，原因是默认情况下 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 属性为 `false`。因此，如果需要对方法使用单向协定，则必须将 attribute 属性的值显式指定为 `true`。  
  
## 示例  
 下面的代码示例定义一个服务协定，其中包括几个单向方法。除了 `Equals` 默认设置为请求\-答复并返回结果之外，所有的方法都具有单向协定。  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 [设计和实现服务](../../../../docs/framework/wcf/designing-and-implementing-services.md)   
 [如何：定义服务协定](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)   
 [会话](../../../../docs/framework/wcf/samples/session.md)   
 [如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)