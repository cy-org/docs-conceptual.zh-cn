---
title: "跟踪配置文件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22682566-1cd9-4672-9791-fb3523638e18
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 跟踪配置文件
跟踪配置文件包含跟踪查询，这些查询允许跟踪参与者订阅当工作流实例的状态在运行时发生更改时发出的工作流事件。  
  
## 跟踪配置文件  
 跟踪配置文件用来指定为工作流实例发出的跟踪的信息。 如果未指定配置文件，则发出所有跟踪事件。如果指定了配置文件，则将发出在配置文件中指定的跟踪事件。根据您的监视要求，可以编写一个非常一般的配置文件，用来订阅对工作流进行的一小组高级状态更改。相反，也可以创建一个非常详细的配置文件，其生成的事件足够丰富，可在以后重新构造详细的执行流。  
  
 跟踪配置文件将其自身列为标准 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 配置文件中的 XML 元素或在代码中指定的 XML 元素。下面的示例摘自配置文件中的 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]跟踪配置文件，跟踪参与者可利用它订阅 `Started` 和 `Completed` 工作流事件。  
  
```  
<system.serviceModel>  
    ...  
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
    ...  
</system.serviceModel>  
  
```  
  
 下面的示例演示如何使用代码显示创建的等效跟踪配置文件。  
  
```csharp  
TrackingProfile profile = new TrackingProfile()  
{  
    Name = "CustomTrackingProfile",  
    Queries =   
    {  
        new WorkflowInstanceQuery()  
        {  
            // Limit workflow instance tracking records for started and  
            // completed workflow states.  
            States = { WorkflowInstanceStates.Started, WorkflowInstanceStates.Completed },  
        }  
    }  
};  
  
```  
  
 利用 <xref:System.Activities.Tracking.ImplementationVisibility> 特性，可以通过跟踪配置文件中的可见性模式筛选跟踪记录。复合活动是顶级活动，包含构成其实现的其他活动。可见性模式指定工作流活动中的复合活动发出的跟踪记录，这些跟踪记录用于指定是否跟踪构成实现的活动。可见性模式在跟踪配置文件级别应用。对工作流中单个活动的跟踪记录的筛选由跟踪配置文件中的查询控制。有关更多信息，请参见本文档中的**跟踪配置文件查询类型**部分。  
  
 跟踪配置文件中的 `implementationVisibility` 特性指定的两种可见性模式包括 `RootScope` 和 `All`。如果复合活动不是工作流的根，则使用 `RootScope` 模式会禁止构成活动实现的活动的跟踪记录。这意味着，如果将使用其他活动实现的某一活动添加到工作流中，并将 `implementationVisibility` 设置为 RootScope，则仅跟踪该复合活动中的顶级活动。如果活动是工作流的根，该活动的实现即为工作流自身，因此将发出构成实现的活动的跟踪记录。使用 All 模式允许发出根活动及其所有复合活动的所有跟踪记录。  
  
 例如，假定 *MyActivity* 是一个复合活动，其实现包含 *Activity1* 和 *Activity2* 两个活动。如果将此活动添加到工作流，并使用跟踪配置文件（已将 `implementationVisibility` 设置为 `RootScope`）启用跟踪，则仅发出 *MyActivity* 的跟踪记录，而不会发出 *Activity1* 和 *Activity2* 活动的记录。  
  
 但是，如果将跟踪配置文件的 `implementationVisisbility` 特性设置为 `All`，则不仅会发出 *MyActivity* 的跟踪记录，还会发出 *Activity1* 和 *Activity2* 活动的跟踪记录。  
  
 `implementationVisibility` 标志适用于以下跟踪记录类型：  
  
-   ActivityStateRecord  
  
-   FaultPropagationRecord  
  
-   CancelRequestedRecord  
  
-   ActivityScheduledRecord  
  
> [!NOTE]
>  implementationVisibility 设置无法筛选出活动实现发出的 CustomTrackingRecord。  
  
 在代码中，按如下方式在跟踪配置文件中指定为 <xref:System.Activities.Tracking.ImplementationVisibility> 的 `implementationVisibility` 功能：  
  
```  
TrackingProfile sampleTrackingProfile = new TrackingProfile()  
{  
    Name = "Sample Tracking Profile",  
    ImplementationVisibility = ImplementationVisibility.RootScope  
};  
  
```  
  
 可按如下方式在跟踪配置文件中指定为 <xref:System.Activities.Tracking.ImplementationVisibility> 的 `implementationVisibility` 功能：  
  
```  
<tracking>  
      <profiles>  
        <trackingProfile name="Shipping Monitoring" implementationVisibility="All">  
          <workflow activityDefinitionId="*">  
...  
         </workflow>  
        </trackingProfile>  
      </profiles>  
</tracking>  
  
```  
  
 跟踪配置文件中的 `ImplementationVisibility` 设置是可选的。默认情况下，其值设置为 `RootScope`。此外，该特性的值还区分大小写。  
  
### 跟踪配置文件查询类型  
 跟踪配置文件组织为跟踪记录的声明性订阅，利用这些订阅可以查询特定跟踪记录的工作流运行时。查询类型有多种，可用于订阅 <xref:System.Activities.Tracking.TrackingRecord> 对象的不同类。可以通过配置或代码指定跟踪配置文件。以下是最常见的查询类型：  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceQuery> \- 用于跟踪工作流实例生命周期更改，例如，上面演示的 `Started` 和 `Completed`。<xref:System.Activities.Tracking.WorkflowInstanceQuery> 用于订阅下列 <xref:System.Activities.Tracking.TrackingRecord> 对象：  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceAbortedRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceTerminatedRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceSuspendedRecord>  
  
     在 <xref:System.Activities.Tracking.WorkflowInstanceStates> 类中指定了可订阅的状态。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.WorkflowInstanceQuery> 订阅 `Started` 实例状态的工作流实例级跟踪记录所使用的配置或代码。  
  
    ```  
    <workflowInstanceQueries>  
        <workflowInstanceQuery>  
          <states>  
            <state name="Started"/>  
          </states>  
        </workflowInstanceQuery>  
    </workflowInstanceQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new WorkflowInstanceQuery()  
            {  
                States = { WorkflowInstanceStates.Started}                                                                     
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.ActivityStateQuery> \- 用于跟踪组成工作流实例的活动的生命周期更改。例如，您可能希望对工作流实例中的“发送电子邮件”活动的每次完成进行跟踪。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.ActivityStateRecord> 对象。在 <xref:System.Activities.Tracking.ActivityStates> 中指定了要订阅的可用状态。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.ActivityStateQuery> 订阅 `SendEmailActivity` 活动的活动状态跟踪记录所使用的配置和代码。  
  
    ```  
    <activityStateQueries>  
      <activityStateQuery activityName="SendEmailActivity">  
        <states>  
          <state name="Closed"/>  
        </states>  
      </activityStateQuery>  
    </activityStateQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =  
        {  
            new ActivityStateQuery()  
            {                              
                ActivityName = "SendEmailActivity",  
                States = { ActivityStates.Closed }  
            }  
        }  
    };  
  
    ```  
  
    > [!NOTE]
    >  如果多个 activityStateQuery 元素具有相同的名称，只有最后一个元素中的状态用于跟踪配置文件。  
  
-   <xref:System.Activities.Tracking.ActivityScheduledQuery> \- 该查询用于跟踪安排给父活动来执行的活动。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.ActivityScheduledRecord> 对象。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.ActivityScheduledQuery> 订阅与安排执行的 `SendEmailActivity` 子活动相关的记录所使用的配置和代码。  
  
    ```  
    <activityScheduledQueries>  
      <activityScheduledQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />  
     </activityScheduledQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new ActivityScheduledQuery()  
            {  
                ActivityName = "ProcessNotificationsActivity",  
                ChildActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.FaultPropagationQuery> \- 用于跟踪对在活动中出现的错误进行的处理。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.FaultPropagationRecord> 对象。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.FaultPropagationQuery> 订阅与错误传播相关的记录所使用的配置和代码。  
  
    ```  
    <faultPropagationQueries>  
      <faultPropagationQuery faultSourceActivityName="SendEmailActivity" faultHandlerActivityName="NotificationsFaultHandler" />  
    </faultPropagationQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =  
        {  
            new FaultPropagationQuery()  
            {  
                FaultSourceActivityName = "SendEmailActivity",  
                FaultHandlerActivityName = "NotificationsFaultHandler"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.CancelRequestedQuery> \- 用于跟踪父活动取消子活动的请求。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.CancelRequestedRecord> 对象。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.CancelRequestedQuery> 订阅与活动取消相关的记录所使用的配置和代码。  
  
    ```  
    <cancelRequestedQueries>  
      <cancelRequestedQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />  
    </cancelRequestedQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new CancelRequestedQuery()  
            {  
                ActivityName = "ProcessNotificationsActivity",  
                ChildActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.CustomTrackingQuery> \- 用于跟踪您在代码活动中定义的事件。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.CustomTrackingRecord> 对象。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.CustomTrackingQuery> 订阅与自定义跟踪记录相关的记录所使用的配置和代码。  
  
    ```  
    <customTrackingQueries>  
      <customTrackingQuery name="EmailAddress" activityName="SendEmailActivity" />  
    </customTrackingQueries>  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new CustomTrackingQuery()   
            {  
                Name = "EmailAddress",  
                ActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.BookmarkResumptionQuery> \- 用于跟踪工作流实例中的书签恢复。<xref:System.Activities.Tracking.TrackingParticipant> 需要用该查询来订阅 <xref:System.Activities.Tracking.BookmarkResumptionRecord> 对象。  
  
     下面的示例演示使用 <xref:System.Activities.Tracking.BookmarkResumptionQuery> 订阅与书签恢复相关的记录所使用的配置和代码。  
  
    ```  
    <bookmarkResumptionQueries>  
      <bookmarkResumptionQuery name="SentEmailBookmark" />  
    </bookmarkResumptionQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new BookmarkResumptionQuery()  
            {  
                Name = "sentEmailBookmark"  
            }  
        }  
    };  
  
    ```  
  
### 批注  
 通过批注，可以使用可在生成时后配置的某个值任意标记跟踪记录。例如，可能希望使用“Mail Server”\=\=“Mail Server1”来标记跨多个工作流的多个跟踪记录。这样便于在以后查询跟踪记录时查找带有此标记的所有记录。  
  
 为此，可以在跟踪查询中添加一个批注，如下面的示例所示。  
  
```  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <annotations>  
    <annotation name="MailServer" value="Mail Server1"/>  
  </annotations>  
</activityStateQuery>  
  
```  
  
### 如何创建跟踪配置文件  
 跟踪查询元素用于通过使用 XML 配置文件或 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 代码创建跟踪配置文件。以下是使用配置文件创建跟踪配置文件的示例。  
  
```  
<system.serviceModel>  
  <tracking>  
    <profiles>  
      <trackingProfile name="Sample Tracking Profile ">  
        <workflow activityDefinitionId="*">  
          <!--Specify the tracking profile query elements to subscribe for tracking records-->  
        </workflow>  
      </trackingProfile>  
    </profiles>  
  </tracking>  
</system.serviceModel>  
  
```  
  
> [!WARNING]
>  对于使用工作流服务主机的 WF，跟踪配置文件通常是使用配置文件创建的。也可以通过代码使用跟踪配置文件和跟踪查询 API 来创建跟踪配置文件。  
  
 配置为 XML 配置文件的配置文件适用于使用行为扩展的跟踪参与者。该配置文件添加到 WorkflowServiceHost 中，如下一节[为工作流配置跟踪](../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md)中所述。  
  
 主机发出的跟踪记录的详细信息由跟踪配置文件中的配置设置确定。跟踪参与者通过向跟踪配置文件添加查询来订阅跟踪记录。若要订阅所有跟踪记录，跟踪配置文件需要在每个查询的名称字段中使用 "\*" 指定所有跟踪查询。  
  
 下面是跟踪配置文件的一些常见示例。  
  
-   用于获取工作流实例记录和错误的跟踪配置文件。  
  
```  
<trackingProfile name="Instance and Fault Records">  
  <workflow activityDefinitionId="*">  
    <workflowInstanceQueries>  
      <workflowInstanceQuery>  
        <states>  
          <state name="*" />  
        </states>  
      </workflowInstanceQuery>  
    </workflowInstanceQueries>  
    <activityStateQueries>  
      <activityStateQuery activityName="*">  
        <states>  
          <state name="Faulted"/>  
        </states>  
      </activityStateQuery>  
    </activityStateQueries>  
  </workflow>  
</trackingProfile>  
  
```  
  
1.  用于获取所有自定义跟踪记录的跟踪配置文件。  
  
```  
<trackingProfile name="Instance_And_Custom_Records">  
  <workflow activityDefinitionId="*">  
    <customTrackingQueries>  
      <customTrackingQuery name="*" activityName="*" />  
    </customTrackingQueries>  
  </workflow>  
</trackingProfile>  
  
```  
  
## 请参阅  
 [SQL 跟踪](../../../docs/framework/windows-workflow-foundation/samples/sql-tracking.md)   
 [Windows Server App Fabric 监控](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [使用 App Fabric 监控应用程序](http://go.microsoft.com/fwlink/?LinkId=201275)