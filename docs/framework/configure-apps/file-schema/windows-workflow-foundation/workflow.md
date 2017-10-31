---
title: "&lt;workflow&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 560aa9b6-9cf3-460e-b798-f87d14b1d2de
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;workflow&gt;
一个配置元素，包含 **activityDefinitionId** 属性所标识的特定工作流的所有查询。  
  
 有关工作流跟踪及其配置的详细信息，请参阅 [工作流跟踪](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md) 和 [跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
## 语法  
  
```vb  
  
<system.serviceModel>  
  <tracking>    
    <trackingProfile name="String">  
      <workflow activityDefinitionId="String">  
          <activityScheduledQueries>  
             <activityScheduledQuery activityName="String"  
                 childActivityName="String"/>  
          </activityScheduledQueries>  
             <activityStateQuery activityName="String" />  
                <arguments>  
                   <argument name="String"/>  
                </arguments>  
                <states>  
                   <state name="String"/>  
                </states>  
                <variables>  
                   <variable name="String"/>  
                </variables>  
          </activityStateQueries>  
          <bookmarkResumptionQueries>  
             <bookmarkResumptionQuery name="String" />  
          </bookmarkResumptionQueries>  
          <cancelRequestQueries>  
             <cancelRequestQuery activityName="String"  
                 childActivityName="String"/>  
          </cancelRequestQueries>  
          <customTrackingQueries>  
             <customTrackingQuery activityName="String"  
                 name="String"/>  
          </customTrackingQueries>  
          <faultPropagationQueries>  
             <faultPropagationQuery activityName="String"  
                 faultHandlerActivityName="String"/>  
          </faultPropagationQueries>  
         <workflowInstanceQueries>  
            <workflowInstanceQuery>  
              <states>  
                 <state name="String"/>  
              </states>  
          </workflowInstanceQuery>  
        </workflowInstanceQueries>  
      </workflow>  
    </trackingProfile>          
   </profiles>  
  </tracking>  
</system.serviceModel>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|activityDefinitionId|一个字符串，指定所跟踪的工作流的活动定义 ID。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<activityScheduledQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activityscheduledqueries.md)|表示一个查询集合，这些查询用于跟踪安排给父活动来执行的活动。  跟踪参与者需要用此查询来订阅活动安排记录。|  
|[\<activityStateQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activitystatequeries.md)|表示一个查询集合，这些查询用于跟踪构成工作流实例的活动的生命周期更改。  例如，您可能希望对工作流实例中的“发送电子邮件”活动的每次完成进行跟踪。  跟踪参与者需要用此查询来订阅活动状态记录对象。  在 ActivityStates 中指定了要订阅的可用状态。|  
|[\<bookmarkResumptionQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/bookmarkresumptionqueries.md)|表示一个查询集合，这些查询用于跟踪工作流实例中的书签恢复。  跟踪参与者需要用此查询来订阅书签恢复记录。|  
|[\<cancelRequestedQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/cancelrequestedqueries.md)|表示一个查询集合，这些查询用于跟踪父活动取消子活动的请求。  跟踪参与者需要用此查询来订阅取消请求记录对象。|  
|[\<customTrackingQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/customtrackingqueries.md)|表示一个查询集合，这些查询用于跟踪您在代码活动中定义的事件。  跟踪参与者需要用此查询来订阅自定义跟踪记录。|  
|[\<faultPropagationQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/faultpropagationqueries.md)|表示一个查询集合，这些查询用于跟踪在某个活动中发生的错误的处理。 每次 FaultHandler 处理错误时，都会发生此事件。  应使用此类查询来跟踪对在活动中出现的错误进行的处理。  跟踪参与者需要用此查询来订阅错误传播记录。|  
|[\<workflowInstanceQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancequeries.md)|表示配置元素的集合，这些配置元素跟踪工作流实例生命周期的更改，例如已开始或已完成的事件。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<trackingProfile\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/trackingprofile.md)|表示一个配置节，用于创建对跟踪参与者中的工作流跟踪记录的订阅。  跟踪配置文件包含跟踪查询，这些查询允许跟踪参与者订阅当工作流实例的状态在运行时发生更改时发出的工作流事件。  跟踪配置文件节中定义的查询用于定义订阅返回的事件类型。|  
  
## 备注  
 跟踪配置文件包含跟踪查询，这些查询允许跟踪参与者订阅当特定工作流实例的状态在运行时发生更改时发出的工作流事件。  所跟踪的工作流实例由此配置元素来标识。  
  
 根据您的监视要求，可以编写一个非常粗陋的配置文件，用来订阅对工作流进行的一小组高级状态更改。  相反，也可以创建一个非常具体的配置文件，其生成的事件足够丰富，可在以后重新构造详细的执行流。  
  
 跟踪配置文件组织为跟踪记录的声明性订阅，利用这些订阅可以查询特定跟踪记录的工作流运行时。  查询类型有多种，可用于订阅跟踪记录的不同类。  有关查询在完整列表，请参见本主题的子元素列表以及[跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
 下面的示例演示配置文件中的跟踪配置文件，跟踪参与者可利用它订阅 `Started`和 `Completed`工作流事件。  
  
```  
  
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
   </profiles>  
  </tracking>  
</system.serviceModel>  
  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Activities.Tracking.Configuration.ProfileWorkflowElement>   
 <xref:System.Activities.Tracking.TrackingProfile>   
 [工作流跟踪](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)