---
title: "WF 中的状态机活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 93312eaf-07e0-4a55-b4f7-4cdbbc4dee2d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# WF 中的状态机活动
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 提供几个系统提供的活动和用于创建状态机工作流的活动设计器。  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.StateMachine>|使用熟悉的状态机范例执行包含的活动。|  
|<xref:System.Activities.Statements.State>|表示状态机中的状态。|  
|<xref:System.Activities.Core.Presentation.FinalState>|表示状态机中的终止状态。<xref:System.Activities.Core.Presentation.FinalState> 是在创建预配置为终止状态的 <xref:System.Activities.Statements.State> 时所使用的活动设计器。有关更多信息，请参见 [FinalState 活动设计器](../Topic/FinalState%20Activity%20Designer.md)。|  
|<xref:System.Activities.Statements.Transition>|表示两个状态间的转换。如果没有 <xref:System.Activities.Statements.Transition> 的**“工具箱”** 项；转换将通过拖动和放置在二个状态间的线或拖放三角形上在工作流设计器上创建转换有关更多信息，请参见 [事务活动设计器](../Topic/Transition%20Activity%20Designer.md)。|  
  
## 请参阅  
 [入门教程](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)