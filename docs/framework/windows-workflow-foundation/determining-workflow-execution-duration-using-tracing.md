---
title: "使用跟踪确定工作流执行持续时间 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f04ad0fd-edc7-4cbc-8979-356f2a1131c4
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 使用跟踪确定工作流执行持续时间
本主题演示如何使用工作流跟踪来确定执行成功完成的自承载工作流所需的时间。  
  
### 使用工作流跟踪来确定工作流应用程序执行的持续时间  
  
1.  打开 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)]。依次选择**“文件”**、**“新建”**和**“项目”**。在**“C\#”**下，选择**“工作流”**节点。从模板列表中选择**“工作流控制台应用程序”**。将新项目命名为 `WorkflowDurationTracing`，并单击**“确定”**。  
  
2.  打开 Workflow1.xaml。将 <xref:System.Activities.Statements.Delay> 活动拖动到设计器图面上。将值 00:00:10（10 秒）分配给活动的“持续时间”属性。  
  
3.  通过单击**“开始”**、**“运行”**并输入 `eventvwr.exe` 来打开事件查看器。  
  
4.  如果尚未启用工作流跟踪，请依次展开**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。选择**“视图”**、**“显示分析和调试日志”**。右键单击**“调试”**，并选择**“启用日志”**。使事件查看器保持打开状态，以便在工作流运行后可以查看跟踪。  
  
5.  按 Ctrl\+Shift\+B 执行工作流应用程序。  
  
6.  在事件查看器中，查找 ID 为 1009 的最新事件和类似于以下内容的消息。记下记录消息的时间。  
  
 **父 Activity ''、DisplayName: ''、InstanceId: '' 安排了子 Activity“WorkflowDurationTracking.Workflow1”、DisplayName“Workflow1”、InstanceId“1”。**  
  
7.  查找另一个 ID 为 1001 的最新事件和类似于以下内容的消息。从此消息的记录值中减去以前的消息时间，以确定工作流执行的持续时间，应该大约为 10 秒钟。  
  
 **WorkflowInstance Id“1bbac57b\-3322\-498e\-9e27\-8833fda3a5bf”在“已关闭”状态下完成。**  
  
## 请参阅  
 [工作流跟踪](../../../docs/framework/windows-workflow-foundation//workflow-tracing.md)   
 [Windows Server App Fabric 监控](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [使用 App Fabric 监控应用程序](http://go.microsoft.com/fwlink/?LinkId=201275)