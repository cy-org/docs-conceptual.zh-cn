---
title: "Deprecated types in Windows Workflow Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4aebe928-a964-4c1c-abf7-0dbbd3604b13
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Deprecated types in Windows Workflow Foundation
在 .NET 4 中，工作流团队在 <xref:System.Activities> 命名空间中发布了一个全新的工作流引擎。  发布 .NET 4.5 Beta 后，我们将“WF 3”<xref:System.Workflow.Activities>、<xref:System.Workflow.ComponentModel> 和 <xref:System.Workflow.Runtime> 命名空间中的大多数类型标记为已过时。  
  
## 过时的命名空间和工具  
 以下程序集具有将被弃用的一个或多个公共类型：  
  
-   System.Workflow.Activities.dll  
  
-   System.Workflow.ComponentModel.dll  
  
-   System.Workflow.Runtime.dll  
  
-   System.WorkflowServices.dll  
  
-   Microsoft.Workflow.DebugController.dll  
  
-   Microsoft.Workflow.Compiler.exe  
  
-   Wfc.exe  
  
 因此，使用已弃用的 WF 3 API 的客户将会遇到生成警告，其中包含如下消息：  
  
  **警告 BC40000：X 已过时：WF 3 类型已过时。  请改用 WF 4。**  我们将在将来的版本中从 .NET Framework 移除这些类型，但我们尚未确定有关时间范围（不在 4.5 中移除）。  借助于当前这个步骤，我们可以将我们的方向传达给客户，使他们能够有充裕的时间转移到新的 WF4 模型。  当然，我们将继续基于 [Microsoft 支持生命周期策略](http://aka.ms/MicrosoftSupportLifecycle)（可能为英文网页）支持这些 WF 3 类型。  现有 WF3 应用程序仍将会在 .NET 4.5 上正常运行，并且 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 将支持新的和现有的基于 WF3 的解决方案。  
  
 <xref:System.Workflow.Activities.Rules> 命名空间中与规则相关的类型（在 WF 4.5 中没有替代选项）尚不会被弃用。  
  
 想要将其应用程序迁移到 WF 4 的客户将会在 MSDN 上的 [Workflow 4 迁移指南](http://aka.ms/WF4MigrationGuidance)（可能为英文网页）文章以及 [WF Codeplex](http://aka.ms/WFCodeplex) 网站上的 [WF 4 迁移包](http://aka.ms/WF4MigrationKit)（可能为英文网页）中找到帮助。