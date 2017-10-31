---
title: "设计和实现自定义活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e30e63d-6e33-4842-a7a4-ce807cef1fad
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# 设计和实现自定义活动
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 中自定义活动的创建途径有二：或是将系统提供的活动组装成组合活动，或是创建派生自 <xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity> 或 <xref:System.Activities.NativeActivity> 的新类型。  本节介绍如何使用任一方法来创建自定义活动。  
  
> [!IMPORTANT]
>  自定义活动在工作流设计器中默认显示为一个包含活动名称的简单矩形。  若要在工作流设计器中为您的活动提供自定义可视化表示形式，还必须创建自定义设计器。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][使用自定义活动设计器和模板](../../../docs/framework/windows-workflow-foundation//using-custom-activity-designers-and-templates.md)。  
  
## 本节内容  
 [活动创作选项](../../../docs/framework/windows-workflow-foundation//activity-authoring-options-in-wf.md)  
 讨论可在 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]中使用的创作样式。  
  
 [使用自定义活动](../../../docs/framework/windows-workflow-foundation//using-a-custom-activity.md)  
 描述如何将自定义活动添加到工作流项目。  
  
 [创建异步活动](../../../docs/framework/windows-workflow-foundation//creating-asynchronous-activities-in-wf.md)  
 描述如何创建异步活动。  
  
 [配置活动验证](../../../docs/framework/windows-workflow-foundation//configuring-activity-validation.md)  
 描述如何使用活动验证在执行活动之前发现并报告活动配置中的错误。  
  
 [在运行时创建活动](../../../docs/framework/windows-workflow-foundation//creating-an-activity-at-runtime-with-dynamicactivity.md)  
 讨论如何使用 <xref:System.Activities.DynamicActivity> 在运行时创建活动。  
  
 [工作流执行属性](../../../docs/framework/windows-workflow-foundation//workflow-execution-properties.md)  
 描述如何使用工作流执行属性将上下文特定属性添加到活动的环境中。  
  
 [使用活动委托](../../../docs/framework/windows-workflow-foundation//using-activity-delegates.md)  
 讨论如何编写和使用包含活动代理的活动。  
  
 [活动本地化](../../../docs/framework/windows-workflow-foundation//activity-localization.md)  
 描述如何在活动中使用本地化的字符串资源。  
  
 [使用活动扩展](../../../docs/framework/windows-workflow-foundation//using-activity-extensions.md)  
 描述如何编写和使用活动扩展。  
  
 [使用工作流中的 OData 源](../../../docs/framework/windows-workflow-foundation//consuming-odata-feeds-from-a-workflow.md)  
 描述从工作流中调用 WCF 数据服务的几种方法。  
  
 [活动定义范围和可见性](../../../docs/framework/windows-workflow-foundation//activity-definition-scoping-and-visibility.md)  
 描述用于定义数据范围和活动成员可见性的选项和规则。