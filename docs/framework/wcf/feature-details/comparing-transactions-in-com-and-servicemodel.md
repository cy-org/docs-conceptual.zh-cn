---
title: "比较 COM+ 和 ServiceModel 中的事务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e493bcdd-b91a-4486-853f-83dbcd1931b7
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 比较 COM+ 和 ServiceModel 中的事务
本主题讨论如何使用 <xref:System.ServiceModel> 命名空间提供的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 属性来模拟事务性 COM\+ 服务的行为。  
  
## 使用 ServiceModel 属性模拟 COM\+  
 下表比较用于创建 `EnterpriseServices` 事务的 <xref:System.EnterpriseServices.TransactionOption> 枚举，以及他们如何与 <xref:System.ServiceModel> 提供的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 属性关联。  
  
|COM\+ 属性|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 属性|  
|--------------|----------------------------------------------------------------|  
|RequiresNew|将 <xref:System.ServiceModel.TransactionFlowAttribute> 设置为 <xref:System.ServiceModel.TransactionFlowOption>。<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 为 `true`。<br /><br /> 绑定元素中的 `TransactionFlow` 属性为 `false`。|  
|必需|将 <xref:System.ServiceModel.TransactionFlowAttribute> 设置为 <xref:System.ServiceModel.TransactionFlowOption>。<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 为 `true`。<br /><br /> 绑定元素中的 `TransactionFlow` 属性为 `true`。|  
|支持|没有直接等效项。  通常，您应采用为 `Required` 指定的行为。|  
|NotSupported|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 为 `false`。<br /><br /> 绑定元素中的 `TransactionFlow` 属性为 `false`。|  
|Disabled|没有直接等效项。  通常，您应采用为 `NotSupported` 指定的行为。|