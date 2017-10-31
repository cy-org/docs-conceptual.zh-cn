---
title: "请求-答复相关 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf4379bf-2d08-43f3-9584-dfa30ffcb1f6
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 请求-答复相关
将请求\-答复相关与 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对配合使用可以在工作流服务中实现双向操作，而与 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对配合使用可以在其他 Web 服务中调用双向操作。  在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务中调用双向操作时，该服务可以是传统的基于命令性代码的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务，也可以是工作流服务。  若要使用请求\-答复相关，必须使用双向绑定，例如 <xref:System.ServiceModel.BasicHttpBinding>。  无论是调用还是实现双向操作，相关初始化步骤都非常相似，本节涵盖了这些步骤。  
  
## 在双向操作中配合使用相关和 Receive\/SendReply  
 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对用于在工作流服务中实现双向操作。  运行时使用请求\-答复相关，确保将答复调度到正确的调用方。  如果使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载工作流（这属于工作流服务），默认相关初始化足以满足需要。  在此方案中，工作流使用 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对，并且无需执行任何特定相关配置。  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
  
```  
  
### 显式初始化请求\-答复相关  
 如果存在其他并行的双向操作，则应显式配置相关。  可通过指定 <xref:System.ServiceModel.Activities.CorrelationHandle> 和 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer>，或者将 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 放置到 <xref:System.ServiceModel.Activities.CorrelationScope> 中来完成此操作。  在此示例中，在 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对中配置请求\-答复相关。  
  
```csharp  
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder",  
    CorrelationInitializers =  
    {  
        new RequestReplyCorrelationInitializer  
        {  
            CorrelationHandle = RRHandle  
        }  
    }  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
 可以使用 <xref:System.ServiceModel.Activities.CorrelationScope> 活动来取代显式配置关联。  <xref:System.ServiceModel.Activities.CorrelationScope> 向其包含的消息传递活动提供隐式 <xref:System.ServiceModel.Activities.CorrelationHandle>。  在此示例中，<xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对包含在 <xref:System.ServiceModel.Activities.CorrelationScope> 中。  无需执行任何显式相关配置。  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
CorrelationScope s = new CorrelationScope  
{  
    Body = new Sequence  
    {  
        Activities =   
        {  
            StartOrder,  
            // Activities that create the reply.  
            ReplyToStartOrder  
        }  
    }  
};  
  
// Construct a workflow using the CorrelationScope.  
```  
  
 如果需要其他相关，可以使用相应消息传递活动（使用所需 `CorrelationInitializer` 类型）的 <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> 属性来配置这些相关。  
  
## 在双向操作中配合使用相关和 Send\/ReceiveReply  
 <xref:System.ServiceModel.Activities.Receive> 活动只能用于由 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载的工作流服务，而 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对可用于必须调用 Web 服务上的方法的任何工作流。  如果使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载工作流，将应用上一节中介绍的默认相关，否则，必须显式使用所需 <xref:System.ServiceModel.Activities.CorrelationInitializer> 和 <xref:System.ServiceModel.Activities.CorrelationHandle>，或者使用 <xref:System.ServiceModel.Activities.CorrelationScope> 的隐式句柄管理来配置相关。  
  
 如果在具有双向操作的服务上使用**“添加服务引用”**，生成的活动将使用显式指定的请求\/答复相关在内部包装 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对活动。