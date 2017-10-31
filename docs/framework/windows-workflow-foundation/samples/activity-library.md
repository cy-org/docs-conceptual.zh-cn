---
title: "活动库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5323e9d4-71d6-47eb-bfa6-31feac62044d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 活动库
本节包含了演示 [!INCLUDE[wf](../../../../includes/wf-md.md)] 中的高级自定义活动的示例。  
  
## 本节内容  
 [.NET Framework 4.5 中的策略活动](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md)  
 演示 Policy4 活动如何通过使用在 WF 3.5 中提供的规则引擎，允许在 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF 4.5\) 的 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 中直接执行 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF 3.5\) 中的现有 [!INCLUDE[wf2](../../../../includes/wf2-md.md)]<xref:System.Workflow.Activities.Rules.RuleSet> 对象。  
  
 [要基于一系列值进行切换的自定义活动](../../../../docs/framework/windows-workflow-foundation/samples/custom-activity-to-switch-on-a-range-of-values.md)  
 演示如何创建扩展对 <xref:System.Activities.Statements.Switch%601> 的使用的自定义活动。  
  
 [LINQ to Objects 活动](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-objects-activity.md)  
 演示如何创建活动以使用 LINQ to Objects 查询集合中的元素。  
  
 [LINQ to SQL](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-sql-sample.md)  
 演示如何创建活动以使用 LINQ to SQL 查询 SQL Server 数据库的表中的实体。  
  
 [使用 InvokePowerShell 活动](../../../../docs/framework/windows-workflow-foundation/samples/using-the-invokepowershell-activity.md)  
 演示如何使用 InvokePowerShell 活动调用 Windows PowerShell 命令。  
  
 [RangeEnumeration 活动](../../../../docs/framework/windows-workflow-foundation/samples/rangeenumeration-activity.md)  
 演示如何创建可循环访问数字集合的自定义活动。  
  
 [正则表达式活动](../../../../docs/framework/windows-workflow-foundation/samples/regular-expression-activities.md)  
 演示如何创建一组公开 <xref:System.Text.RegularExpressions> 命名空间的正则表达式功能的活动。  
  
 [SendMail 自定义活动](../../../../docs/framework/windows-workflow-foundation/samples/sendmail-custom-activity.md)  
 演示如何创建派生自 <xref:System.Activities.AsyncCodeActivity> 的自定义活动，以使用 SMTP 发送邮件供在工作流应用程序内使用。  
  
 [For 活动](../../../../docs/framework/windows-workflow-foundation/samples/for-activity.md)  
 演示如何生成一个从 <xref:System.Activities.NativeActivity> 继承的自定义活动，以及如何在工作流中使用它来循环访问一个值范围。  
  
 [等待输入活动](../../../../docs/framework/windows-workflow-foundation/samples/wait-for-input-activity.md)  
 演示如何在工作流中创建命名书签。  
  
 [限制并行 ForEach](../../../../docs/framework/windows-workflow-foundation/samples/throttled-parallel-foreach.md)  
 演示 `ThrottleParallelForEach` 活动与 <xref:System.Activities.Statements.ParallelForEach%601> 活动的相似之处，二者的不同之处在于，前者允许设置一个并发因子来限制要同时执行的分支的数量。  
  
 [实体活动](../../../../docs/framework/windows-workflow-foundation/samples/entity-activities.md)  
 演示如何结合使用 ADO.NET Entity Framework 和 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 来简化数据访问。  
  
 [数据库访问活动](../../../../docs/framework/windows-workflow-foundation/samples/database-access-activities.md)  
 演示如何创建具有以下用途的活动：允许访问数据库以检索或修改信息，并使用 [ADO.NET](http://go.microsoft.com/fwlink/?LinkId=166081) 访问数据库。  
  
 [CommentOut 活动](../../../../docs/framework/windows-workflow-foundation/samples/commentout-activity.md)  
 演示如何编写一个自定义活动，该活动从执行路径中移除其他活动，从而有效注释掉这些活动。  
  
 [.NET Framework 4.5 中的外部化策略活动](../../../../docs/framework/windows-workflow-foundation/samples/externalized-policy-activity-in-net-framework-4-5.md)  
 演示 ExternalizedPolicy4 活动如何通过使用在 WF 3.5 中提供的规则引擎，允许在 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF 4.5\) 的 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 中直接执行 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF 3.5\) <xref:System.Workflow.Activities.Rules.RuleSet> 对象中的现有 [!INCLUDE[wf2](../../../../includes/wf2-md.md)]。  
  
 [NoPersistScope 活动](../../../../docs/framework/windows-workflow-foundation/samples/nopersistscope-activity.md)  
 演示如何操作工作流中的不可序列化且可释放的状态。  
  
 [非泛型 ForEach](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-foreach.md)  
 演示如何创建非泛型版本的 <xref:System.Activities.Statements.ForEach%601> 活动。  
  
 [非泛型 ParallelForEach](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-parallelforeach.md)  
 演示了如何创建非泛型版本的 <xref:System.Activities.Statements.ParallelForEach%601> 活动。  
  
 [获取 WorkflowInstanceId](../../../../docs/framework/windows-workflow-foundation/samples/get-workflowinstanceid.md)  
 演示如何使用自定义活动 `GetWorkflowInstanceId` 返回工作流实例 ID。