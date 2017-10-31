---
title: "配置活动验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 25a4eccb-b8fc-4857-a01d-2683b6341219
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 配置活动验证
活动验证启用活动作者和用户，以在执行任何活动配置之前标识和报告此配置中的错误的方法。[!INCLUDE[wf](../../../includes/wf-md.md)] 提供了以下三种类型的操活动验证：  
  
-   `RequiredArgument` 和 `OverloadGroup` 特性。  
  
-   基于命令性代码的验证。  
  
-   声明性约束。  
  
 `RequiredArgument` 和 `OverloadGroup` 特性指示活动中的特定参数是必需的。基于命令性代码的验证为活动提供围绕其自身进行验证的简单方法，声明性约束支持围绕活动及其与包含工作流之间的关系进行验证。如果未根据验证要求正确配置活动，将返回验证错误和警告。如果包含工作流是使用工作流设计器创建的，则会在设计器中显示所有验证错误和警告。如果工作流不是使用工作流设计器创建的，则会在调用工作流时返回任何验证错误。不管工作流的创建方式如何，绝不允许执行带有验证错误的工作流。本节概述了这些活动验证类型及其调用方法。  
  
## 本节内容  
 [必需参数和重载组](../../../docs/framework/windows-workflow-foundation//required-arguments-and-overload-groups.md)  
 介绍如何使用 `RequiredArgument` 和 `OverloadGroup` 特性提供验证。  
  
 [基于命令性代码的验证](../../../docs/framework/windows-workflow-foundation//imperative-code-based-validation.md)  
 介绍如何对基于 <xref:System.Activities.CodeActivity> 和 <xref:System.Activities.NativeActivity> 的活动使用基于代码的验证。  
  
 [声明性约束](../../../docs/framework/windows-workflow-foundation//declarative-constraints.md)  
 介绍如何使用声明性约束提供复杂活动验证。  
  
 [调用活动验证](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md)  
 讨论何时自动调用活动验证以及如何显式调用验证。  
  
## 参考  
  
## 相关章节