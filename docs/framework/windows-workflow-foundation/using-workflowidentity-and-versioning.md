---
title: "使用 WorkflowIdentity 和版本控制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8451735-8046-478f-912b-40870a6c0c3a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 使用 WorkflowIdentity 和版本控制
<xref:System.Activities.WorkflowIdentity> 为工作流应用程序开发人员提供了一种将名称和 <xref:System.Version> 与工作流定义关联的方法，这种方法还可用于将此信息与持久化工作流实例相关联。工作流应用程序开发人员可以使用这些标识信息，为一些情景（如并行执行一个工作流定义的多个版本）提供支持，并为其他功能（如动态更新）提供基础。此主题概述了如何将 <xref:System.Activities.WorkflowIdentity> 与 <xref:System.Activities.WorkflowApplication> 承载一起使用。有关在工作流服务中并行执行工作流定义的信息，请参见[WorkflowServiceHost 中的并行版本控制](../../../docs/framework/wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md)。有关动态更新的信息，请参见[动态更新](../../../docs/framework/windows-workflow-foundation//dynamic-update.md)。  
  
## 主题内容  
  
-   [使用 WorkflowIdentity](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UsingWorkflowIdentity)  
  
    -   [使用 WorkflowIdentity 并行执行](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#SxS)  
  
-   [升级 .NET Framework 4 持久性数据库以支持工作流版本控制](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)  
  
    -   [升级数据库架构](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#ToUpgrade)  
  
##  <a name="UsingWorkflowIdentity"></a> 使用 WorkflowIdentity  
 若要使用 <xref:System.Activities.WorkflowIdentity>，请创建并配置一个实例，并将它与一个 <xref:System.Activities.WorkflowApplication> 实例关联。一个 <xref:System.Activities.WorkflowIdentity> 实例包含三条标识信息。<xref:System.Activities.WorkflowIdentity.Name%2A> 和 <xref:System.Activities.WorkflowIdentity.Version%2A> 包含一个名称和一个 <xref:System.Version>，并且是必需的；而 <xref:System.Activities.WorkflowIdentity.Package%2A> 则是可选的，可用于指定包含如程序集名称或其他所需信息的附加字符串。如果 <xref:System.Activities.WorkflowIdentity> 的三个属性中有任一属性不同于其他 <xref:System.Activities.WorkflowIdentity>，则它是唯一的。  
  
> [!IMPORTANT]
>  <xref:System.Activities.WorkflowIdentity> 不应包含任何个人身份信息 \(PII\)。在几个不同活动生命周期点，运行时将向任何已配置的跟踪服务发出有关用于创建实例的 <xref:System.Activities.WorkflowIdentity> 的信息。WF 跟踪没有任何隐藏 PII（敏感用户信息）的机制。因此，<xref:System.Activities.WorkflowIdentity> 实例不应该包含任何 PII 数据，因为运行时将在跟踪记录中发出这些数据，任何有权查看跟踪记录的人都能够看到这些数据。  
  
 在以下示例中，创建了 <xref:System.Activities.WorkflowIdentity> 并将它与使用 `MortgageWorkflow` 工作流定义创建的工作流实例相关联。  
  
```csharp  
WorkflowIdentity identityV1 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v1",  
    Version = new Version(1, 0, 0, 0)  
};  
  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Run the workflow.  
wfApp.Run();  
```  
  
 重新加载和恢复工作流时，必须使用一个配置为与持久化工作流实例的 <xref:System.Activities.WorkflowIdentity> 匹配的 <xref:System.Activities.WorkflowIdentity>。  
  
```csharp  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Load the workflow.  
wfApp.Load(instanceId);  
  
// Resume the workflow...  
```  
  
 如果重新加载工作流实例时使用的 <xref:System.Activities.WorkflowIdentity> 与持久化 <xref:System.Activities.WorkflowIdentity> 不匹配，则将引发 <xref:System.Activities.VersionMismatchException>。在以下示例中，尝试加载在前一个示例中持久化的 `MortgageWorkflow` 实例。执行此加载尝试时，使用了一个为更新版本抵押工作流配置的 <xref:System.Activities.WorkflowIdentity>，该工作流与持久保存实例不匹配。  
  
```csharp  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow_v2(), identityV2);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Attempt to load the workflow instance.  
wfApp.Load(instanceId);  
  
// Resume the workflow...  
```  
  
 执行前一段代码时，引发了以下 <xref:System.Activities.VersionMismatchException>。  
  
 **所加载实例的 WorkflowIdentity \('MortgageWorkflow v1; Version\=1.0.0.0'\) 与提供的工作流定义的 WorkflowIdentity \('MortgageWorkflow v2; Version\=2.0.0.0'\) 不匹配。可以使用不同的定义加载此实例，或使用动态更新更新此实例。**   
###  <a name="SxS"></a> 使用 WorkflowIdentity 并行执行  
 可使用 <xref:System.Activities.WorkflowIdentity> 帮助并行执行一个工作流的多个版本。一种常见的情形是更改长期运行的工作流的业务需求。部署更新版本时，可能正在运行一个工作流的多个实例。可对主机应用程序进行配置，使之在启动新实例时使用更新过的工作流定义，并且该主机应用程序应负责在恢复实例时提供正确的工作流定义。<xref:System.Activities.WorkflowIdentity> 可用于在恢复工作流实例时确定和提供匹配的工作流定义。  
  
 为检索持久化工作流实例的 <xref:System.Activities.WorkflowIdentity>，将使用 <xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法。<xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法使用持久化工作流实例的 <xref:System.Activities.WorkflowApplication.Id%2A> 和包含该持久化实例的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>，并返回一个 <xref:System.Activities.WorkflowApplicationInstance>。<xref:System.Activities.WorkflowApplicationInstance> 包含有关持久化工作流实例的信息，包括其关联的 <xref:System.Activities.WorkflowIdentity>。主机可使用此关联 <xref:System.Activities.WorkflowIdentity> 在加载和恢复工作流实例时提供正确的工作流定义。  
  
> [!NOTE]
>  空 <xref:System.Activities.WorkflowIdentity> 是有效的，主机可以用它将没有关联 <xref:System.Activities.WorkflowIdentity> 的持久化实例映射到正确的工作流定义。如果最初编写工作流应用程序时没有采用工作流版本控制，或者应用程序从 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 升级而来，则可能发生这种情况。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [升级 .NET Framework 4 持久性数据库以支持工作流版本控制](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)。  
  
 在以下示例中，使用了一个 `Dictionary<WorkflowIdentity, Activity>` 将 <xref:System.Activities.WorkflowIdentity> 实例与其匹配的工作流定义相关联，并使用了与 `identityV1` <xref:System.Activities.WorkflowIdentity> 相关联的 `MortgageWorkflow` 工作流定义来启动一个工作流。  
  
```csharp  
WorkflowIdentity identityV1 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v1",  
    Version = new Version(1, 0, 0, 0)  
};  
  
WorkflowIdentity identityV2 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v2",  
    Version = new Version(2, 0, 0, 0)  
};  
  
Dictionary<WorkflowIdentity, Activity> WorkflowVersionMap = new Dictionary<WorkflowIdentity, Activity>();  
WorkflowVersionMap.Add(identityV1, new MortgageWorkflow());  
WorkflowVersionMap.Add(identityV2, new MortgageWorkflow_v2());  
  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Run the workflow.  
wfApp.Run();  
```  
  
 在以下示例中，通过调用 <xref:System.Activities.WorkflowApplication.GetInstance%2A> 来检索有关前一个示例中持久化工作流实例的信息，并使用了持久化 <xref:System.Activities.WorkflowIdentity> 信息来检索匹配的工作流定义。将使用这些信息来配置 <xref:System.Activities.WorkflowApplication>，然后将加载工作流。请注意，因为使用了 <xref:System.Activities.WorkflowApplication.Load%2A> 重载（它使用 <xref:System.Activities.WorkflowApplicationInstance>），<xref:System.Activities.WorkflowApplication> 将使用在 <xref:System.Activities.WorkflowApplicationInstance> 上配置的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>，因此无需配置其 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 属性。  
  
> [!NOTE]
>  如果设置 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 属性，则必须用 <xref:System.Activities.WorkflowApplicationInstance> 所使用的那一个 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 实例来设置，否则将引发 <xref:System.ArgumentException> 异常，并显示以下消息：`The instance is configured with a different InstanceStore than this WorkflowApplication.`。  
  
```csharp  
// Get the WorkflowApplicationInstance of the desired workflow from the specified  
// SqlWorkflowInstanceStore.  
WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(instanceId, store);  
  
// Use the persisted WorkflowIdentity to retrieve the correct workflow  
// definition from the dictionary.  
Activity definition = WorkflowVersionMap[instance.DefinitionIdentity];  
  
WorkflowApplication wfApp = new WorkflowApplication(definition, instance.DefinitionIdentity);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Load the persisted workflow instance.  
wfApp.Load(instance);  
  
// Resume the workflow...  
```  
  
##  <a name="UpdatingWF4PersistenceDatabases"></a> 升级 .NET Framework 4 持久性数据库以支持工作流版本控制  
 SqlWorkflowInstanceStoreSchemaUpgrade.sql 数据库脚本旨在用于升级使用 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 数据库脚本创建的持久性数据库。此脚本会更新这些数据库，使之支持 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中推出的全新版本控制功能。数据库中任何持久化工作流实例都将获得默认的版本控制值，然后就可以参与并行执行和动态更新。  
  
 如果某个 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 工作流应用程序尝试执行任何持久性操作，而此类操作对尚未使用提供的脚本升级的持久性数据库使用新的版本控制功能，则将引发 <xref:System.Runtime.DurableInstancing.InstancePersistenceCommandException>，并显示与以下消息内容类似的消息。  
  
 **SqlWorkflowInstanceStore 的数据库版本为“4.0.0.0”。InstancePersistenceCommand 'System.Activities.DurableInstancing.CreateWorkflowOwnerWithIdentityCommand' 无法针对此数据库版本运行。请将此数据库升级为“4.5.0.0”。**   
###  <a name="ToUpgrade"></a> 升级数据库架构  
  
1.  打开 SQL Server Management Studio 并连接到持久性数据库服务器，例如 **.\\SQLEXPRESS**。  
  
2.  从**文件”**菜单中依次选择**“打开”**和**“文件”**。浏览到以下文件夹：`C:\Windows\Microsoft.NET\Framework\4.0.30319\sql\en`  
  
3.  选择**“SqlWorkflowInstanceStoreSchemaUpgrade.sql”**，然后单击**“打开”**。  
  
4.  在**“可用数据库”**下拉列表中选择持久性数据库的名称。  
  
5.  从**“查询”**菜单中选择**“执行”**。  
  
 查询完成时，数据库架构将升级，您可以根据需要查看分配给持久化工作流实例的默认工作流标识。在**对象资源管理器**中的**“数据库”**节点中展开您的持久性数据库，然后展开**“视图”**节点。右键单击**“System.Activities.DurableInstancing.Instances”**，然后选择**“选择前 1000 行”**。滚动到列的末尾，可以看到视图中另外添加了六列，它们是：**“IdentityName”**、**“IdentityPackage”**、**“Build”**、**“Major”**、**“Minor”**以及**“Revision”**。任何持久化工作流的这些字段都将为 **NULL** 值，这表示空工作流标识。