---
title: "侦听器（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查询侦听器 [WCF 数据服务]"
  - "WCF 数据服务, 自定义"
ms.assetid: e33ae8dc-8069-41d0-99a0-75ff28db7050
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 侦听器（WCF 数据服务）
通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，应用程序可以侦听请求消息，以便能够为操作添加自定义逻辑。  使用此自定义逻辑可以验证传入消息中的数据，  还可以使用它进一步限制查询请求的范围，以便基于每个请求插入自定义授权策略。  
  
 侦听由数据服务中具有特殊特性的方法执行。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 在消息处理过程中的适当时刻调用这些方法。  侦听器基于每个实体集进行定义，侦听器方法无法像服务操作那样接受请求中的参数。  在处理 HTTP GET 请求时调用的查询侦听器方法必须返回一个 lambda 表达式，该表达式确定查询结果是否应当返回侦听器实体集的实例。  数据服务使用此表达式来进一步优化请求的操作。  下面是查询侦听器的定义示例。  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptordef)]
 [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
 有关详细信息，请参阅[如何：截获数据服务消息](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md)。  
  
 在处理非查询操作时调用的变更侦听器必须返回 `void`（在 Visual Basic 中为 `Nothing`）。  变更侦听器方法必须接受以下两个参数：  
  
1.  一个与实体集的实体类型相兼容的类型的参数。  数据服务调用变更侦听器时，此参数的值将反映请求发送的实体信息。  
  
2.  一个 <xref:System.Data.Services.UpdateOperations> 类型的参数。  数据服务调用变更侦听器时，此参数的值将反映请求试图执行的操作。  
  
 下面是变更侦听器的定义示例。  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptordef)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
 有关详细信息，请参阅[如何：截获数据服务消息](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md)。  
  
 支持使用以下特性进行侦听。  
  
 **\[QueryInterceptor\(** *EnitySetName* **\)\]**  
 当收到了针对目标实体集资源的 HTTP GET 请求时，将调用应用了 <xref:System.Data.Services.QueryInterceptorAttribute> 特性的方法。  这些方法必须始终返回一个 `Expression<Func<T,bool>>` 形式的 lambda 表达式。  
  
 **\[ChangeInterceptor\(** *EnitySetName* **\)\]**  
 当收到了针对目标实体集资源的 HTTP GET 请求以外的 HTTP 请求时，将调用应用了 <xref:System.Data.Services.ChangeInterceptorAttribute> 特性的方法。  这些方法必须始终返回 `void`（在 Visual Basic 中为 `Nothing`）。  
  
 有关详细信息，请参阅[如何：截获数据服务消息](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md)。  
  
## 请参阅  
 [服务操作](../../../../docs/framework/data/wcf/service-operations-wcf-data-services.md)