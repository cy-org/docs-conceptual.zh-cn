---
title: "内置活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 31e1b8c2-7f74-458a-b2e2-fddc5b10eac1
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 内置活动
本节包含演示内置 [!INCLUDE[wf](../../../../includes/wf-md.md)] 活动的示例。  
  
## 本节内容  
 [使用 TryCatch 在 Flowchart 活动中进行错误处理](../../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
 演示如何在复杂控制流活动中使用 <xref:System.Activities.Statements.TryCatch> 活动。  
  
 [在 While 活动中模拟中断](../../../../docs/framework/windows-workflow-foundation/samples/emulating-breaking-in-a-while-activity.md)  
 演示如何中断下列活动的循环机制：<xref:System.Activities.Statements.DoWhile>、<xref:System.Activities.Statements.ForEach%601>、<xref:System.Activities.Statements.While> 和 <xref:System.Activities.Statements.ParallelForEach%601>。  
  
 [DynamicActivity 创建](../../../../docs/framework/windows-workflow-foundation/samples/dynamicactivity-creation.md)  
 演示在运行时使用 <xref:System.Activities.DynamicActivity> 活动来创建活动的两种不同方式。  
  
 [将变量用于 .NET Framework 3.5 规则集](../../../../docs/framework/windows-workflow-foundation/samples/using-variables-with-dotnet-ruleset.md)  
 演示如何创建一个工作流，该工作流使用 <xref:System.Activities.Statements.Interop> 活动集成在 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] 中编写的使用了策略和规则的自定义活动。  
  
 [从 XAML 加载](../../../../docs/framework/windows-workflow-foundation/samples/load-from-xaml.md)  
 演示如何在不运行 XamlBuildTask 工具的情况下动态加载 XAML 工作流。  
  
 [使用集合活动](../../../../docs/framework/windows-workflow-foundation/samples/using-collection-activities.md)  
 演示如何将集合活动（<xref:System.Activities.Statements.AddToCollection%601>、<xref:System.Activities.Statements.ClearCollection%601>、<xref:System.Activities.Statements.ExistsInCollection%601> 和 <xref:System.Activities.Statements.RemoveFromCollection%601>）与实现 <xref:System.Collections.ICollection> 接口的类一起使用，以及如何创建一个自定义活动，该活动循环访问集合以输出集合中每个元素的内容。  
  
 [使用 InvokeMethod 活动](../../../../docs/framework/windows-workflow-foundation/samples/using-the-invokemethod-activity.md)  
 演示如何使用 <xref:System.Activities.Statements.InvokeMethod> 活动调用公共类中的公共方法。  
  
 [使用 Pick 活动](../../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)  
 演示如何使用 <xref:System.Activities.Statements.Pick> 活动。  
  
 [使用过程性活动](../../../../docs/framework/windows-workflow-foundation/samples/using-procedural-activities.md)  
 演示如何使用 <xref:System.Activities.Statements.Sequence>、<xref:System.Activities.Statements.Assign>、<xref:System.Activities.Statements.If>、<xref:System.Activities.Statements.While>、<xref:System.Activities.Statements.Switch%601>、<xref:System.Activities.Statements.TryCatch> 和 <xref:System.Activities.Statements.WriteLine> 活动以实现猜谜游戏。  
  
 [使用 CancellationScope](../../../../docs/framework/windows-workflow-foundation/samples/using-cancellationscope.md)  
 演示如何使用 <xref:System.Activities.Statements.CancellationScope> 活动取消应用程序中的工作。  
  
 [InvokeMethod](../../../../docs/framework/windows-workflow-foundation/samples/invokemethod.md)  
 演示使用 <xref:System.Activities.Statements.InvokeMethod> 活动调用类的方法的不同方式。  
  
 [带自定义类型的切换活动的用法](../../../../docs/framework/windows-workflow-foundation/samples/usage-of-the-switch-activity-with-custom-types.md)  
 介绍如何使 <xref:System.Activities.Statements.Switch%601> 活动能够在运行时计算用户定义的复杂类型。  
  
 [与 3.5 规则集交互](../../../../docs/framework/windows-workflow-foundation/samples/interop-with-3-5-rule-set.md)  
 演示如何使用 <xref:System.Activities.Statements.Interop> 活动以便与 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] 中使用 <xref:System.Workflow.Activities.PolicyActivity> 和规则的自定义活动集成。