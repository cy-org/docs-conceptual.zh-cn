---
title: "如何：对工作流和工作流服务启用 SQL 持久性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ca7bf77f-3e5d-4b23-b17a-d0b60f46411d
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# 如何：对工作流和工作流服务启用 SQL 持久性
本主题介绍如何通过编程方式以及使用配置文件来配置 SQL 工作流实例存储功能，以便为工作流和工作流服务启用持久性。  
  
 Windows Server App Fabric 大大简化了配置持久性的进程。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][App Fabric 持久性配置](http://go.microsoft.com/fwlink/?LinkId=201204)  
  
 使用 SQL 工作流实例存储功能之前，创建一个数据库以供该功能用来持久保存工作流实例。[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 安装程序将与 SQL 工作流实例存储功能相关联的 SQL 脚本文件复制到 %WINDIR%\\Microsoft.NET\\Framework\\v4.xxx\\SQL\\EN 文件夹。针对您希望 SQL 工作流实例存储用于持久保存工作流实例的 SQL Server 2005 或 SQL Server 2008 数据库，运行这些脚本文件。首先运行 SqlWorkflowInstanceStoreSchema.sql 文件，然后运行 SqlWorkflowInstanceStoreLogic.sql 文件。  
  
> [!NOTE]
>  若要清除此持久性数据库以获得一个全新的数据库，请按下列顺序运行 %WINDIR%\\Microsoft.NET\\Framework\\v4.xxx\\SQL\\EN 中的脚本。  
>   
>  1.  SqlWorkflowInstanceStoreSchema.sql  
> 2.  SqlWorkflowInstanceStoreLogic.sql  
  
> [!IMPORTANT]
>  如果不创建持久性数据库，则当宿主尝试持久保存工作流时，SQL 工作流实例存储功能将引发与以下异常类似的异常。  
>   
>  System.Data.SqlClient.SqlException: 找不到存储过程“System.Activities.DurableInstancing.CreateLockOwner”  
  
 下面介绍如何使用 SQL 工作流实例存储来为工作流与工作流服务启用持久性。SQL 工作流实例存储的 [!INCLUDE[crabout](../../../includes/crabout-md.md)] 属性，请参见 [SQL 工作流实例存储的属性](../../../docs/framework/windows-workflow-foundation//properties-of-sql-workflow-instance-store.md)。  
  
## 为使用 WorkflowApplication 的自承载工作流启用持久性  
 可通过使用 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 对象模型为以编程方式使用 <xref:System.Activities.WorkflowApplication> 的自承载工作流启用持久性。以下过程包含了执行上述操作的步骤。  
  
#### 为自承载工作流启用持久性  
  
1.  添加对 System.Activites.DurableInstancing.dll 的引用。  
  
2.  将以下语句添加到源文件顶部的现有“using”语句后面。  
  
    ```csharp  
    using System.Activities.DurableInstancing;  
    ```  
  
3.  如下面的代码示例中所示，构造一个 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>，并将其分配给 <xref:System.Activities.WorkflowApplication> 的 <xref:System.Activities.WorkflowApplication.InstanceStore%2A>。  
  
    ```csharp  
  
    SqlWorkflowInstanceStore store =   
        new SqlWorkflowInstanceStore("Server=.\\SQLEXPRESS;Initial Catalog=Persistence;Integrated Security=SSPI");  
  
    WorkflowApplication wfApp =  
        new WorkflowApplication(new Workflow1());  
  
    wfApp.InstanceStore = store;  
  
    ```  
  
    > [!NOTE]
    >  根据您的 SQL Server 版本，该连接字符串服务器的名称可能有所不同。  
  
4.  对 <xref:System.Activities.WorkflowApplication> 对象调用 <xref:System.Activities.WorkflowApplication.Persist%2A> 方法以持久保存工作流，或者调用 <xref:System.Activities.WorkflowApplication.Unload%2A> 方法以持久保存并卸载工作流。还可以处理由 <xref:System.Activities.WorkflowApplication> 对象引发的 <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> 事件，并返回 <xref:System.Activities.PersistableIdleAction> 的适当的（<xref:System.Activities.PersistableIdleAction> 或 <xref:System.Activities.PersistableIdleAction>）成员。  
  
    ```csharp  
    wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)  
    {  
        return PersistableIdleAction.Persist;  
    };  
    ```  
  
> [!NOTE]
>  有关使用 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 为工作流启用持久性的示例，请参见[持久性](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)中的[持久保存工作流应用程序](../../../docs/framework/windows-workflow-foundation/samples/persisting-a-workflow-application.md)示例。有关分步说明，请参见[入门教程](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)中的[如何：创建和运行长时间运行的工作流](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md)步骤。  
  
## 为使用 WorkflowServiceHost 的自承载工作流服务启用持久性  
 可通过使用 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 类或者 <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A> 类为以编程方式使用 <xref:System.ServiceModel.WorkflowServiceHost> 的自承载工作流服务启用持久性。  
  
### 使用 SqlWorkflowInstanceStoreBehavior 类  
 以下过程包含使用 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 类来为自承载工作流服务启用持久性的步骤。  
  
##### 使用 SqlWorkflowInstanceStoreBehavior 启用持久性  
  
1.  添加对 System.ServiceModel.dll 的引用。  
  
2.  将以下语句添加到源文件顶部的现有“using”语句后面。  
  
    ```csharp  
    using System.ServiceModel.Activities.Description;  
    ```  
  
3.  创建一个 `WorkflowServiceHost` 实例，并为该工作流服务添加终结点。  
  
    ```  
  
    WorkflowServiceHost host = new WorkflowServiceHost(new CountingWorkflow(), new Uri(hostBaseAddress));  
    host.AddServiceEndpoint("ICountingWorkflow", new BasicHttpBinding(), "");  
  
    ```  
  
4.  构造一个 `SqlWorkflowInstanceStoreBehavior` 对象，并设置该行为对象的属性。  
  
    ```csharp  
  
    SqlWorkflowInstanceStoreBehavior instanceStoreBehavior = new SqlWorkflowInstanceStoreBehavior(connectionString);  
    instanceStoreBehavior.HostLockRenewalPeriod = new TimeSpan(0, 0, 5);  
    instanceStoreBehavior.InstanceCompletionAction = InstanceCompletionAction.DeleteAll;  
    instanceStoreBehavior.InstanceLockedExceptionAction = InstanceLockedExceptionAction.AggressiveRetry;  
    instanceStoreBehavior.InstanceEncodingOption = InstanceEncodingOption.GZip;  
    instanceStoreBehavior.RunnableInstancesDetectionPeriod = new TimeSpan("00:00:02");  
    host.Description.Behaviors.Add(instanceStoreBehavior);  
  
    ```  
  
5.  打开工作流服务宿主。  
  
    ```vb  
  
    host.Open();  
  
    ```  
  
> [!IMPORTANT]
>  有关使用 `SqlWorkflowInstanceStoreBehavior` 类为工作流服务启用持久性的示例，请参见[持久性](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)中的[内置配置](../../../docs/framework/windows-workflow-foundation/samples/built-in-configuration.md)示例。  
  
### 使用 DurableInstancingOptions 属性  
 应用 `SqlWorkflowInstanceStoreBehavior` 时，`WorkflowServiceHost` 上的 `DurableInstancingOptions.InstanceStore` 设置为使用配置值创建的 `SqlWorkflowInstanceStore` 对象。如下面的代码示例中所示，您可以通过编程方式设置 `WorkflowServiceHost` 的 <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A> 属性（而不使用 `SqlWorkflowInstanceStoreBehavior` 类）来达到相同目的。  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
## 使用配置文件为使用 WorkflowServiceHost 的 WAS 承载工作流服务启用持久性  
 可使用配置文件为自承载或 Windows 进程激活服务 \(WAS\) 承载的工作流服务启用持久性。WAS 承载的工作流服务与自承载工作流服务一样，都使用 WorkflowServiceHost。  
  
 `SqlWorkflowInstanceStoreBehavior` 是一个服务行为，可用于通过 XML 配置方便地更改 [SQL 工作流实例存储](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)属性。对于 WAS 承载的工作流服务，请使用 Web.config 文件。下面的配置示例演示如何使用配置文件中的 `sqlWorkflowInstanceStore` 行为元素来配置 SQL 工作流实例存储。  
  
```  
  
<serviceBehaviors>  
    <behavior name="">  
        <sqlWorkflowInstanceStore   
                    connectionString="Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                    instanceEncodingOption="GZip | None"  
                    instanceCompletionAction="DeleteAll | DeleteNothing"  
                    instanceLockedExceptionAction="NoRetry | BasicRetry |AggressiveRetry"  
                    hostLockRenewalPeriod="00:00:30"   
                    runnableInstancesDetectionPeriod="00:00:05">  
  
        <sqlWorkflowInstanceStore/>  
    </behavior>  
</serviceBehaviors>  
  
```  
  
 如果没有设置 `connectionString` 或 `connectionStringName` 属性的值，则 SQL 工作流实例存储将使用默认命名连接字符串 `DefaultSqlWorkflowInstanceStoreConnectionString`。  
  
 应用 `SqlWorkflowInstanceStoreBehavior` 时，`WorkflowServiceHost` 上的 `DurableInstancingOptions.InstanceStore` 设置为使用配置值创建的 `SqlWorkflowInstanceStore` 对象。可以通过编程方式将 `SqlWorkflowInstanceStore` 与 `WorkflowServiceHost` 一起使用，而不使用服务行为元素来达到相同目的。  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
> [!IMPORTANT]
>  建议不要在 Web.config 文件中存储敏感信息，如用户名和密码。如果在 Web.config 文件中存储了敏感信息，应使用文件系统访问控制列表 \(ACL\) 来确保安全访问 Web.config 文件。此外，还可以保护配置文件中的配置值的安全，如[使用受保护的配置加密配置信息](http://go.microsoft.com/fwlink/?LinkId=178419)（可能为英文网页）中所述。  
  
### 与 SQL 工作流实例存储功能相关的 Machine.config 元素  
 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 安装将以下与 SQL 工作流实例存储功能相关的元素添加到 Machine.config 文件中：  
  
-   将以下行为扩展元素添加到 Machine.config 文件中，以便可以使用配置文件中的 \<`sqlWorkflowInstanceStore`\> 服务行为元素来为服务配置持久性。  
  
    ```  
  
    <configuration>  
        <system.serviceModel>  
            <extensions>  
                <behaviorExtensions>  
                    <add name="sqlWorkflowInstanceStore" type="System.Activities.DurableInstancing.SqlWorkflowInstanceStoreElement, System.Activities.DurableInstancing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />  
                </behaviorExtensions>  
            </extensions>  
        <system.serviceModel>  
    <configuration>  
  
    ```