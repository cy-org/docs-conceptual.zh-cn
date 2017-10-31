---
title: "如何：使用 WorkflowServiceHost 配置跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed1485fe-7529-4351-bca3-8bb915260b17
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：使用 WorkflowServiceHost 配置跟踪
本主题说明如何为 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中承载的 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]工作流配置跟踪。  可以通过指定服务行为使用 Web.config 文件进行配置。  
  
### 在配置中配置跟踪  
  
1.  在配置文件中使用 \<`behavior`\> 元素添加 <xref:System.Activities.Tracking.EtwTrackingParticipant>，如下面的示例所示。  
  
    ```  
    <behaviors>  
       <serviceBehaviors>  
         <behavior>  
           <etwTracking profileName="Sample Tracking Profile" />  
         </behavior>              
       </serviceBehaviors>  
    <behaviors>  
  
    ```  
  
    > [!NOTE]
    >  上面的配置示例使用的是简化配置。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [简化配置](../../../../docs/framework/wcf/simplified-configuration.md).  
  
     上面的配置示例添加一个 <xref:System.Activities.Tracking.EtwTrackingParticipant>，并指定一个跟踪配置文件名称。  跟踪配置文件是在 \<`tracking`\> 元素的 \<`trackingProfile`\> 元素中创建的。  跟踪配置文件包含跟踪查询，这些查询允许跟踪参与者订阅工作流实例的状态在运行时发生更改时发出的工作流事件。  下面的示例演示如何创建跟踪配置文件。  
  
    ```xml  
    <system.serviceModel>  
        <tracking>   
         <trackingProfile name="Sample Tracking Profile">  
            <workflow activityDefinitionId="*">  
               <workflowInstanceQueries>  
                 <workflowInstanceQuery>  
                    <states>  
                       <state name="Started"/>  
                       <state name="Completed"/>  
                    </states>  
                </workflowInstanceQuery>  
             </workflowInstanceQueries>  
           </workflow>  
         </trackingProfile>   
       </tracking>  
    </system.serviceModel>  
  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]跟踪配置文件的更多信息，请参见[跟踪配置文件](../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]跟踪的一般信息，请参见[工作流跟踪](../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)。  
  
### 在代码中配置跟踪  
  
1.  在代码中使用 <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior> 行为添加 <xref:System.Activities.Tracking.EtwTrackingParticipant>，如下面的示例所示。  
  
    ```csharp  
    host.Description.Behaviors.Add(new EtwTrackingBehavior { ProfileName = "Sample Tracking Profile" });  
    ```  
  
     上面的代码示例添加一个 <xref:System.Activities.Tracking.EtwTrackingParticipant>，并指定一个跟踪配置文件名称。  跟踪配置文件是在 \<`tracking`\> 元素的 \<`trackingProfile`\> 元素中创建的，如上一节所示。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]跟踪配置文件的更多信息，请参见[跟踪配置文件](../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]跟踪的一般信息，请参见[工作流跟踪](../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)。  有关如何以编程方式配置跟踪的示例，请参见[为工作流配置跟踪](../../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md)。  
  
## 请参阅  
 [WCF 服务的简化配置](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)   
 [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [跟踪配置文件](../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)