---
title: "如何：使用 WorkflowServiceHost 配置永久性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：使用 WorkflowServiceHost 配置永久性
本主题介绍如何使用配置文件配置 SQL 工作流实例存储功能，以便对 <xref:System.ServiceHost.Activities.WorkflowServiceHost> 中承载的工作流启用永久性。  使用 SQL 工作流实例存储功能之前，必须创建用于保存工作流实例的 SQL 数据库。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：对工作流和工作流服务启用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  
  
### 在配置中配置 SQL 工作流实例存储  
  
1.  可以通过 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>（一个用于通过 XML 配置更改设置的服务行为）配置 SQL 工作流实例存储的属性。  下面的配置示例演示如何使用配置文件中的 \<`sqlWorkflowInstanceStore`\> 行为元素来配置 SQL 工作流实例存储。  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore   
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"   
                 runnableInstancesDetectionPeriod="00:00:05">  
            <sqlWorkflowInstanceStore/>  
        </behavior>  
    </serviceBehaviors>  
  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何配置 SQL 工作流实例存储的更多信息，请参见[如何：对工作流和工作流服务启用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] \<`sqlWorkflowInstanceStore`\> 行为元素的各种设置的更多信息，请参见 [SQL 工作流实例存储](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  Windows Server App Fabric 提供其自己的永久性存储。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Windows Server App Fabric 持久性](http://go.microsoft.com/fwlink/?LinkId=193121)（可能为英文网页）。  
  
    > [!NOTE]
    >  上面的配置示例使用的是简化配置。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [简化配置](../../../../docs/framework/wcf/simplified-configuration.md)  
  
### 在代码中配置 SQL 工作流实例存储  
  
1.  可以通过 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>（一个用于通过代码更改设置的服务行为）配置 SQL 工作流实例存储的属性。  下面的示例演示如何在代码中使用 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行为元素来配置 SQL 工作流实例存储。  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何配置 SQL 工作流实例存储的更多信息，请参见[如何：对工作流和工作流服务启用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行为元素的各种设置的更多信息，请参见 [SQL 工作流实例存储](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  Windows Server App Fabric 提供其自己的永久性存储。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Windows Server App Fabric 持久性](http://go.microsoft.com/fwlink/?LinkId=193121)（可能为英文网页）。  
  
    > [!NOTE]
    >  上面的配置示例使用的是简化配置。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [简化配置](../../../../docs/framework/wcf/simplified-configuration.md)  
  
     有关如何以编程方式配置持久性的示例，请参见[如何：对工作流和工作流服务启用持久性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-persistence-for-workflows-and-workflow-services.md)。  
  
## 请参阅  
 [工作流服务](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [工作流持久性](../../../../docs/framework/windows-workflow-foundation//workflow-persistence.md)   
 [Windows Server App Fabric 持久性 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=193121)