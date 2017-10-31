---
title: "入门教程 [.NET Framework 4.5] | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WF [WF], 入门"
  - "Windows Workflow Foundation [WF], 入门"
ms.assetid: c2d3585f-6b1a-4d4f-9865-bd7cd31c5d42
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 入门教程 [.NET Framework 4.5]
本节包含一组介绍 [!INCLUDE[wf](../../../includes/wf-md.md)] 应用程序编程的演练主题。按照这些主题中的过程操作，将生成一个猜数游戏应用程序。本教程中的第一个主题将逐步引导您创建工作流所需的自定义活动。在第二个主题中，将这些活动与内置的工作流活动组合成一个流程图工作流。在第三个主题中，配置宿主应用程序以运行工作流，并在最后的主题中介绍持久性。此过程的每一步骤都依赖于前面的步骤，因此建议您按顺序完成这些步骤。  
  
## 本节内容  
 [如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)  
 介绍如何创建从 <xref:System.Activities.NativeActivity%601> 派生的自定义活动，以及如何使用活动设计器将此活动与内置的活动组合成一个复合活动。  
  
 [如何：创建工作流](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)  
 通过使用内置的活动和前面教程中的自定义活动，介绍如何创建流程图、顺序工作流和状态机工作流。  
  
 [如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)  
 介绍如何从宿主环境调用工作流、如何将数据传入和传出工作流以及如何继续书签。  
  
 [如何：创建和运行长时间运行的工作流](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md)  
 介绍如何向工作流应用程序添加持久性。  
  
 [如何：创建自定义跟踪参与者](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md)  
 介绍如何创建自定义跟踪参与者和跟踪配置文件。  
  
 [如何：并行承载多个版本的工作流](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md)  
 介绍如何使用 `WorkflowIdentity` 并行承载工作流的多个版本。  
  
 [如何：更新正在运行的工作流实例的定义](../../../docs/framework/windows-workflow-foundation//how-to-update-the-definition-of-a-running-workflow-instance.md)  
 介绍如何使用动态更新来修改运行的工作流实例。  
  
## 请参阅  
 [Windows Workflow Foundation 编程](../../../docs/framework/windows-workflow-foundation//programming.md)