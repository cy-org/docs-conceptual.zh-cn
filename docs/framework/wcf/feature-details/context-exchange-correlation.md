---
title: "上下文交换相关 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e2852be-3601-45ae-b507-ccc465d45c60
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 上下文交换相关
上下文相关依据的是在 [.NET Context Exchange Protocol Specification](http://go.microsoft.com/fwlink/?LinkId=166059)（.NET 上下文交换协议规范）中描述的上下文交换机制。上下文相关使用已知的上下文头或 cookie 将消息与正确的实例相关。若要使用上下文相关，必须在提供给 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的终结点上使用诸如 <xref:System.ServiceModel.BasicHttpContextBinding>、<xref:System.ServiceModel.WSHttpContextBinding> 或 <xref:System.ServiceModel.NetTcpContextBinding> 之类的基于上下文的绑定。此主题说明如何在工作流服务中将上下文相关用于消息传送活动。  
  
## 使用上下文相关  
 如果客户端必须重复调用工作流服务，并且系统使用一个上下文绑定承载该服务，此时可以使用上下文相关。工作流服务中的 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对可初始化这种类型的相关。上下文将与答复一起发送回客户端，客户端随后将此上下文附加到对服务的后续调用。  
  
### 在工作流服务中配置上下文相关  
 使用与答复初始传入消息的 <xref:System.ServiceModel.Activities.SendReply> 活动相关联的 <xref:System.ServiceModel.Activities.ContextCorrelationInitializer> 初始化上下文相关。在下面的实例中，配置了 <xref:System.ServiceModel.Activities.SendReply> 来初始化上下文相关。  
  
```csharp  
Variable<string> Item = new Variable<string>();  
Variable<CorrelationHandle> OrderHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = "IOrderService",  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    CorrelationInitializers =  
    {  
        new ContextCorrelationInitializer  
        {  
            CorrelationHandle = OrderHandle  
        }  
    }  
};  
```  
  
> [!NOTE]
>  在此示例中，实际上使用了两种类型的相关：上下文相关和请求\-答复相关。使用上下文相关是为了将来自客户端的调用路由到正确的实例。请求\-答复相关由 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动一起使用，以实现这些活动建模的双向操作。在此示例中，仅显式配置了上下文相关，<xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对使用的是由 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的隐式 <xref:System.ServiceModel.Activities.CorrelationHandle> 管理提供的默认请求\-答复相关。当使用 **ReceiveAndSendReply** 活动模版的工作流设计器中，请求\-相关答复明确地配置。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 请求\-回复相关和隐式关联处理管理，请参阅 [请求\-答复](../../../../docs/framework/wcf/feature-details/request-reply-correlation.md) 和 [相关概述](../../../../docs/framework/wcf/feature-details/correlation-overview.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]**ReceiveAndSendReply** 活动模版，请参见 [ReceiveAndSendReply](../Topic/ReceiveAndSendReply%20Template%20Designer.md)。  
  
 工作流服务中的后续 <xref:System.ServiceModel.Activities.Receive> 活动可以引用由上一示例中的 <xref:System.ServiceModel.Activities.SendReply> 初始化的 <xref:System.ServiceModel.Activities.CorrelationHandle>。  
  
```csharp  
Receive AddItem = new Receive  
{  
    ServiceContractName = "IOrderService",  
    OperationName = "AddItem",  
    CorrelatesWith = OrderHandle  
};  
```  
  
 随后，在 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 上配置终结点以使用基于上下文的绑定，如 <xref:System.ServiceModel.BasicHttpContextBinding>。  
  
```xml  
<endpoint  
  contract=”IOrderContract”  
  binding = “basicHttpContextBinding”  
  address=”http://localhost:8080/OrderService” />  
```  
  
### 在工作流客户端中配置上下文相关  
 客户端为其他工作流时，也必须在客户端配置上下文相关。在客户端工作流上，必须使用 <xref:System.ServiceModel.Activities.ContextCorrelationInitializer> 来配置对工作流服务进行初始调用的 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对的 <xref:System.ServiceModel.Activities.ReceiveReply>。  
  
```csharp  
Variable<CorrelationHandle> cchandle = new Variable<CorrelationHandle>();  
Send request = new Send  
{  
    // Activity configuration omitted.  
};  
  
ReceiveReply reply = new ReceiveReply  
{  
    Request = request,  
    CorrelationInitializers =   
    {  
        new ContextCorrelationInitializer  
        {  
            CorrelationHandle = cchandle  
        }  
    }  
};  
```  
  
 初始化相关后，后续 <xref:System.ServiceModel.Activities.Send> 活动即可使用 <xref:System.ServiceModel.Activities.CorrelationHandle> 调用同一服务实例上的方法。  
  
```csharp  
Send request2 = new Send  
{  
    CorrelatesWith = cchandle,  
    // Remaining activity configuration omitted.  
};  
```  
  
 请注意，在上面这些示例中，已显式配置上下文相关。如果客户端工作流也未在 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中承载，除非活动都包含在一个 <xref:System.ServiceModel.Activities.CorrelationScope> 活动中，否则必须显式配置相关。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 上下文关联，请参见 [NetContextExchangeCorrelation](http://msdn.microsoft.com/zh-cn/93c74a1a-b9e2-46c6-95c0-c9b0e9472caf) 示例。  
  
 如果调用工作流服务的客户端不是工作流，则只要客户端将首次调用工作流服务时返回的上下文显式传递回去，它仍然可以进行重复调用。默认情况下，通过添加服务而生成的代理在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 存储中引用此上下文，并传递此上下文。