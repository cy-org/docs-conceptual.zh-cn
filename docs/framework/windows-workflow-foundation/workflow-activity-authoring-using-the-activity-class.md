---
title: "使用 Activity 类的工作流活动创作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b7b1c66-f093-43c3-b4d1-7173b46516da
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 使用 Activity 类的工作流活动创作
使用 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]中的 [!INCLUDE[wf](../../../includes/wf-md.md)] 创建活动的最基本方法是创建一个从 <xref:System.Activities.Activity>（它通过组合自定义活动或 [内置活动库](../../../docs/framework/windows-workflow-foundation//net-framework-4-5-built-in-activity-library.md)中的活动创建功能）继承的类。本主题演示如何创建向控制台写入两个消息的活动。  
  
### 使用活动设计器创建自定义活动  
  
1.  打开 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]。  
  
2.  依次选择“文件”、“新建”和“项目”。在**“项目类型”**窗口中的**“Visual C\#”**下，选择**“Workflow 4.0”**，然后选择**“v2010”**节点。在**“模板”**窗口中选择**“活动库”**。将新项目命名为 HelloActivity。  
  
3.  打开新的活动。将 <xref:System.Activities.Statements.Sequence> 活动从工具箱拖到设计器图面。  
  
4.  将 <xref:System.Activities.Statements.WriteLine> 活动拖到 <xref:System.Activities.Statements.Sequence> 活动中。将 `“Hello World”`（带引号）输入到**“文本”**字段中。  
  
5.  将第二个 <xref:System.Activities.Statements.WriteLine> 活动拖到 <xref:System.Activities.Statements.Sequence> 活动中并将其放置在第一个活动的下面。将 `“Goodbye”`（带引号）输入到**“文本”**字段中。