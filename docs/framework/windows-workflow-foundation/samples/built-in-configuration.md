---
title: "内置配置 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34e85c9b-088d-4347-816c-0f77cb73ef2f
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 内置配置
此示例演示了 SQL 工作流实例存储的使用和配置。SQL 工作流实例存储是基于 SQL 的实例存储实现。它允许实例将状态保存到 SQL Server 或 SQL Server Express 数据库中以及从中加载状态。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果该目录不存在，请转到（下载页）以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Persistence\BuiltInConfiguration`  
  
## 示例详细信息  
 此示例由一个实现计数服务的工作流构成。在调用该服务的启动方法之后，该服务将从 0 计数到 59。计数器将每 2 秒递增一次。在每次计数之后，工作流将持久化。  
  
 计数工作流是通过工作流服务主机自承载的。程序的 `Main` 方法创建一个可承载计数工作流的工作流服务主机的实例。它定义计数工作流可以到达的终结点。之后，它定义一个 SQL 工作流实例存储行为，用于配置 SQL 工作流实例存储。接下来，程序创建一个客户端，调用计数工作流的启动方法。  
  
 在程序启动之后，计数器自动开始计数。请注意，加载该实例并配置 SQL 工作流实例存储可能需要花费几秒钟的时间。有关工作流实例存储的 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]，请参见 [SQL 工作流实例存储](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  
  
 此示例由两部分组成：  
  
1.  InstanceStore1 演示如何使用 C\# 代码配置 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>（请参见 Program.cs）。  
  
2.  InstanceStore2 演示如何使用 XML 代码配置 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>（请参见 App.config）。  
  
 以下设置可用于配置 SQL 工作流实例存储行为：  
  
-   设置 `HostLockRenewalPeriod`。此时间定义主机续订它运行的实例的所有权锁的间隔。锁信息存储在实例存储中。如果在两个 `HostLockRenewalPeriod` 中定义的间隔内没有续订所有权，则认为已放弃该实例。如果另一个 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 正在运行同一个工作流，并连接到同一个实例存储（在同一台计算机上或另一台计算机上），则它恢复该实例。（实例恢复不属于此示例的范围。）  
  
-   设置 `RunnableInstancesDetectionPeriod`。此期限定义主机轮询已经可以运行的实例的间隔。如果发生以下任何事件，则实例可能会变成可运行的：  
  
    -   持久计时器 \(<xref:System.Activities.Statements.Delay>\) 过期。  
  
    -   另一个主机错过其 `HostLockRenewal` 信号（例如，由于计算机崩溃）并恢复实例。  
  
-   设置 `InstanceCompletionAction`。此属性如果设置为 `DeleteNothing`，则在实例存储中保持完整的实例，如果设置为 `DeleteAll`，则在完成时从存储中删除所有实例。请注意  
  
    > [!NOTE]
    >  在计数完成之前通过按 Enter 终止主机并不会完成工作流实例。  
  
-   设置 `InstanceLockedExceptionAction`。此设置定义主机在需要加载另一个主机锁定的实例时应执行的操作。存在下列选项：  
  
    -   如果设置为 `NoRetry`：不再次尝试加载，并将 `InstanceLockedException` 返回到主机。  
  
    -   如果设置为 `BasicRetry`：一直重试加载该实例。按照一种简单的线性算法计划这些重试（例如，每 5 秒重试一次）。  
  
    -   如果设置为 `AggressiveRetry`：一直重试加载该实例。按照一种主动的指数补偿算法计划这些重试。  
  
-   设置编码选项。此设置定义实例状态在 SQL 工作流实例存储中的存储方式。存在下列选项：  
  
    -   使用 GZip 压缩算法对实例状态进行压缩。  
  
    -   不对实例状态进行压缩。  
  
#### 使用此示例  
  
1.  以管理员身份打开一个 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示（如果具有相应的权限）。  
  
2.  导航到示例目录 \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\\CS\)，然后运行 CreateInstanceStore.cmd。  
  
3.  如果管理员权限不可用，则创建 SQL Server 登录。转到`安全` \-\>**“登录”**。右击**“登录”**，创建一个新的登录。  
  
4.  向 SQL 角色添加您的 ACL 用户。依次打开**“数据库”**、**“InstanceStore”**和**“安全”**。右击**“用户”**，选择**“新建用户”**。将**“登录名”**设置为在上一步中创建的用户。将该用户添加到数据库角色成员 **System.Activities.DurableInstancing.InstanceStoreUsers**（以及其他成员）。请注意该用户可能已经存在（例如，用户 dbo）。  
  
5.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 InstanceStore.sln 文件，按 CTRL\+SHIFT\+B 生成解决方案。  
  
6.  在[!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)]中，导航到此示例相应的 bin\\debug 目录 \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\\cs\\InstanceStore\(1 或 2\)\\bin\\debug\)，右击 InstanceStore.exe 并选择**“以管理员身份运行”**。必须使用管理特权来运行此示例，因为它要打开一个通道侦听器。  
  
7.  如果已在数据库（而不是 SQL Server Express 的本地安装）中创建实例存储，则必须更新示例中的数据库连接字符串（InstanceStore1 项目的 Program.cs 中的 `const string ConnectionString` 和 InstanceStore2 项目的 App.config 中的 `connectionString` 特性），并重新编译示例。  
  
#### 验证示例是否正常运行  
  
1.  在此示例运行的过程中，启动 SQL Server Management Studio。  
  
2.  在**“对象资源管理器”**中，依次选择**“数据库”**、**“InstanceStore”**、**“表”**和**“System.Activities.DurableInstancing.InstanceTable”**。  
  
3.  右击**“InstanceTable”**，然后选择**“选择前 1000 行”**。  
  
4.  观察是否存在一个新项，而且**“锁有效期”\[Lock Expiration\]**是否每 5 秒钟更改一次（单击任务栏的**“执行”**按钮可刷新查询）。这是将**“主机锁续订期限”\[Host Lock Renewal Period\]**设置为 5 的结果。  
  
5.  计数完成后，观察实例表中的项是否已移除。这是将**“实例完成操作”\[Instance Completion Action\]**设置为**“DeleteAll”**的结果。  
  
6.  按 Enter 终止工作流宿主应用程序，并观察是否已删除**“LockOwnersTable”**。  
  
#### 卸载此示例  
  
1.  在示例目录 \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\) 中运行 RemoveInstanceStore.cmd。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Persistence\BuiltInConfiguration`  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)