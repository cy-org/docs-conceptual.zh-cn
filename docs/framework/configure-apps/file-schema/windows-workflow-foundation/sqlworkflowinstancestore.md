---
title: "&lt;sqlWorkflowInstanceStore&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 8a4e4214-fc51-4f4d-b968-0427c37a9520
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;sqlWorkflowInstanceStore&gt;
一种服务行为，它允许您配置 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 功能，该功能支持将工作流服务实例的状态信息持久保存到 SQL Server 2005 或 SQL Server 2008 数据库中。  有关此功能的详细信息，请参阅 [SQL 工作流实例存储](../../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  
  
## 语法  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <sqlWorkflowInstanceStore   
          connectionStringName=”String”   
          honstLockRenewalPeriod=”TimeSpan”  
          instanceCompletionAction=”DeleteNothing/DeleteAll”  
          instanceEncodingAction=”None/GZip”  
          instanceLockedExceptionAction=”NoRetry/BasicRetry/AggressiveRetry”  
          runnableInstancesDetectionPeriod=”TimeSpan” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|connectionString|一个字符串，包含用于连接到基础持久性数据库的连接字符串。|  
|connectionStringName|一个字符串，包含指向数据库服务器的已命名连接字符串。  已命名连接字符串的一个示例为“DefaultConnectionString”。|  
|honstLockRenewalPeriod|一个 Timespan 值，指定宿主必须在其间续订对某个实例的锁定的时间段。  如果宿主没有在指定的时间段内续订锁定，则会解除锁定此实例，并且另一宿主可能会选取此实例。<br /><br /> 卸载一个工作流意味着该工作流已持久保存。  如果此特性设置为零，则在工作流进入空闲状态后会立即持久保存并卸载该工作流实例。  将此特性设置为 TimeSpan.MaxValue 可以有效地禁用卸载操作。  处于空闲状态的工作流实例永远不会被卸载。|  
|instanceCompletionAction|一个值，指定在工作流实例完成之后，该工作流实例数据是保留在持久性存储区中还是被删除。  此值的类型为 <xref:System.Activities.DurableInstancing.InstanceCompletionAction>。<br /><br /> 枚举的操作包括在实例完成其操作后删除持久性存储区中的实例数据或不删除持久性存储区中的实例数据。<br /><br /> 完成实例之后保留实例会导致持久性数据库快速增大，这会影响数据库的性能。  您应当配置数据库清除策略来定期删除这些记录，以确保数据库的性能水平能够满足性能要求。|  
|instanceEncodingOption|一个可选值，指定在将实例状态信息保存到持久性存储区之前，是否使用 GZip 算法压缩此信息。  此值的类型为 <xref:System.Activities.DurableInstancing.InstanceEncodingAction>。  此属性的可能值包括：“None”，指定无压缩；“GZip”，指定压缩实例数据并使用 gzip 算法。|  
|instanceLockedExceptionAction|一个值，指定为响应在宿主尝试锁定当前已由另一宿主锁定的实例时引发的异常而发生的操作。  此值的类型为 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>。<br /><br /> 此字段的可选选项有：“无”、“基本重试”和“积极重试”。  默认值为 None。  下面逐一说明上述三个选项：<br /><br /> -   无。  服务主机不会尝试锁定实例，并将 <xref:System.Runtime.Persistence.InstanceLockedException> 传递给调用方。<br />-   基本重试。  服务主机将使用线性重试间隔重新尝试锁定实例，并在序列结尾将异常传递给调用方。<br />-   积极重试。  服务主机将使用按指数增长的延迟时间重新尝试锁定实例，并在序列结尾将 <xref:System.Runtime.Persistence.InstanceLockedException> 传递给调用方。|  
|runnableInstancesDetectionPeriod||  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceBehaviors\> 的 \<behavior\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|指定行为元素。|  
  
## 请参阅  
 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.SqlWorkflowInstanceStoreElement>   
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>   
 [SQL 工作流实例存储](../../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)