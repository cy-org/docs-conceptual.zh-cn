---
title: "WF 中的事务活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb33378e-82c6-4ea0-870f-76dc77e7f0fe
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# WF 中的事务活动
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 有几个系统提供的活动，为建模事务、赔偿和取消。这些编程模型允许继续向前发展变化中的业务逻辑和错误处理的事件中的工作流。[!INCLUDE[crabout](../../../includes/crabout-md.md)] 事务、补偿和取消，请参见 [事务](../../../docs/framework/windows-workflow-foundation//workflow-transactions.md)、[补偿](../../../docs/framework/windows-workflow-foundation//compensation.md) 和 [取消](../../../docs/framework/windows-workflow-foundation//modeling-cancellation-behavior-in-workflows.md)。  
  
## 事务活动  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.CancellationScope>|以活动形式将取消逻辑与执行的主路径相关联（也表示为活动）。|  
|<xref:System.Activities.Statements.CompensableActivity>|支持对其子活动的补偿。|  
|<xref:System.Activities.Statements.Compensate>|显式调用 <xref:System.Activities.Statements.CompensableActivity> 的补偿处理程序。|  
|<xref:System.Activities.Statements.Confirm>|显式调用 <xref:System.Activities.Statements.CompensableActivity> 的确认处理程序。|  
|<xref:System.Activities.Statements.TransactionScope>|划分事务边界。|  
|<xref:System.ServiceModel.Activities.TransactedReceiveScope>|用于限定由收到的消息发起的事务的生存期范围。事务可以流入发起消息的工作流中，也可以在收到消息时由调度程序创建。 **Note:**  设置的其余部分位于 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 中**”消息传递“”工具箱“**部分下。|