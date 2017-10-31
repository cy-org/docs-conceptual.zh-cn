---
title: "使用跟踪对应用程序进行故障排除 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 使用跟踪对应用程序进行故障排除
使用 [!INCLUDE[wf](../../../includes/wf-md.md)]，可以跟踪与工作流有关的信息，以提供有关执行 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 应用程序或服务的详细信息。[!INCLUDE[wf2](../../../includes/wf2-md.md)] 主机能够在执行工作流实例期间捕获工作流事件。如果您的工作流产生错误或异常，则可以使用 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 跟踪详细信息以诊断其处理故障。  
  
## 使用 WF 跟踪对 WF 进行故障诊断  
 若要检测 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 活动处理过程中的错误，可以使用一个跟踪配置文件查询状态为“Faulted”的 <xref:System.Activities.Tracking.ActivityStateRecord>，从而启用跟踪。在以下代码中指定了相应的查询。  
  
```  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 如果某个错误发生传播并且在错误处理程序（如 <xref:System.Activities.Statements.TryCatch> 活动）中得到了处理，则可以使用 <xref:System.Activities.Tracking.FaultPropagationRecord> 检测到此错误。<xref:System.Activities.Tracking.FaultPropagationRecord> 可指示错误的源活动以及错误处理程序的名称。<xref:System.Activities.Tracking.FaultPropagationRecord> 包含错误的异常堆栈形式的错误详细信息。用于订阅 <xref:System.Activities.Tracking.FaultPropagationRecord> 的查询如以下示例中所示。  
  
```  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
  
```  
  
 如果某个错误未在工作流中处理，则它会导致工作流实例出现未经处理的异常并且工作流实例被中止。若要了解未经处理的异常的详细信息，跟踪配置文件必须查询具有以下示例中指定的 `state name=”UnhandledException”` 的工作流实例记录。  
  
```  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 当工作流实例遇到未经处理的异常时，如果已启用 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 跟踪，则发出 <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> 对象。  
  
 此跟踪记录包含异常堆栈形式的错误详细信息。它包含发生错误并且导致未经处理的异常的错误源（例如某个活动）的详细信息。若要订阅 [!INCLUDE[wf2](../../../includes/wf2-md.md)] 中的错误事件，可通过添加跟踪参与者来启用跟踪。通过查询 `ActivityStateQuery (state=”Faulted”)`、<xref:System.Activities.Tracking.FaultPropagationRecord> 和 `WorkflowInstanceQuery (state=”UnhandledException”)` 的跟踪配置文件配置此参与者。  
  
 如果使用 ETW 跟踪参与者启用跟踪，则会向 ETW 会话发出错误事件。可以使用事件查看器查看这些事件。可以在分析通道中的**“事件查看器”\-\>“应用程序和服务日志”\-\>“Microsoft”\-\>“Windows”\-\>“应用程序服务器”\-\>“应用程序”**节点下找到这些事件。  
  
## 请参阅  
 [Windows Server App Fabric 监视](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [使用 App Fabric 监视应用程序](http://go.microsoft.com/fwlink/?LinkId=201275)