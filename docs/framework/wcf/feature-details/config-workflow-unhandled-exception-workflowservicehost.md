---
title: "如何：针对 WorkflowServiceHost 配置工作流的未经处理异常行为 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 如何：针对 WorkflowServiceHost 配置工作流的未经处理异常行为
<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 行为可用于指定 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载的工作流中出现未经处理的异常时所采取的操作。本主题演示如何在配置文件中配置此行为。  
  
### 配置 WorkflowUnhandledExceptionBehavior  
  
1.  将 \<`workflowUnhandledException`\> 元素添加到 \<`serviceBehaviors`\> 元素中的 \<`behavior`\> 元素，并使用 `action` 特性指定出现未经处理的异常时所采取的操作，如下面的示例所示。  
  
    ```  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>   
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    ```  
  
    > [!NOTE]
    >  上面的配置示例使用的是简化配置。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][简化配置](../../../../docs/framework/wcf/simplified-configuration.md).  
  
     可在代码中配置该行为，如下面的示例所示。  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
  
    ```  
  
     可以将 \<`workflowUnhandledException`\> 元素的 `action` 特性设置为以下值之一：  
  
     **abandon**  
     中止内存中的实例，而不影响保存的实例状态（即回滚到上一个保存点）。  
  
     **abandonAndSuspend**  
     中止内存中的实例并将保存的实例更新为挂起。  
  
     **cancel**  
     为实例调用取消处理程序，然后在内存中完成该实例，此操作也有可能将实例从实例存储区中移除。  
  
     **terminate**  
     在内存中完成实例并将其从实例存储区中移除。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 的更多信息，请参见[工作流服务主机可扩展性](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)。  
  
## 请参阅  
 [工作流服务主机可扩展性](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)   
 [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)