---
title: "SQL 工作流实例存储 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8cd2f8a5-4bf8-46ea-8909-c7fdb314fabc
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# SQL 工作流实例存储
[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 附带的 SQL 工作流实例存储允许工作流在 SQL Server 2005 或 SQL Server 2008 数据库中持久保存有关工作流实例的状态信息。此功能主要以 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 类的形式实现，该类是从持久性框架的抽象 <xref:System.Runtime.Persistence.InstanceStore> 类派生的。SQL 工作流实例存储功能包含一个 SQL 持久性提供程序，该提供程序是持久性 API 的具体实现，宿主将使用此持久性 API 向存储发送持久性命令。  
  
 SQL 工作流实例存储支持自承载工作流或使用 <xref:System.Activities.WorkflowApplication> 或 <xref:System.ServiceModel.WorkflowServiceHost> 的工作流服务以及 WAS 中承载的使用 <xref:System.ServiceModel.WorkflowServiceHost> 的服务。可以使用 SQL 工作流实例存储功能公开的对象模型以编程方式为自承载服务配置该功能。可以使用对象模型，也可以使用 XML 配置文件以编程方式为由 <xref:System.ServiceModel.WorkflowServiceHost> 承载的服务配置此功能。  
  
 SQL 工作流实例存储功能（**SqlWorkflowInstanceStore** 类）并不实现 <xref:System.ServiceModel.Persistence.PersistenceProviderFactory>，因此不提供对永久性非工作流 WCF 服务的持久性支持。它也不实现 <xref:System.Workflow.Runtime.Hosting.WorkflowPersistenceService>，因此不提供对 3.x 工作流的持久性支持。该功能仅对 WF 4.0（及更高版本）工作流和工作流服务提供持久性支持。该功能也不支持除了 SQL Server 2005 和 SQL Server 2008 之外的任何数据库。  
  
 本节中的主题介绍 SQL 工作流实例存储的属性和功能，并且提供有关配置该存储的详细信息。  
  
 Windows Server 应用程序 Fabric 提供其自己的实例存储和简化配置和使用实例存储的工具。有关 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)]，请参阅 [Windows Server 应用 Fabric 实例商店](http://go.microsoft.com/fwlink/?LinkId=201201)。有关 [!INCLUDE[crabout](../../../includes/crabout-md.md)] 应用 Fabric SQL Server 持久性数据库，请参见 [应用程序 Fabric SQL Server 持久性数据库](http://go.microsoft.com/fwlink/?LinkId=201202)  
  
## 本节内容  
  
-   [SQL 工作流实例存储的属性](../../../docs/framework/windows-workflow-foundation//properties-of-sql-workflow-instance-store.md)  
  
-   [如何：对工作流和工作流服务启用 SQL 持久性](../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)  
  
-   [实例激活](../../../docs/framework/windows-workflow-foundation//instance-activation.md)  
  
-   [查询支持](../../../docs/framework/windows-workflow-foundation//support-for-queries.md)  
  
-   [存储扩展性](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)  
  
-   [安全性](../../../docs/framework/windows-workflow-foundation//security.md)  
  
-   [SQL Server 持久性数据库](../../../docs/framework/windows-workflow-foundation//sql-server-persistence-database.md)  
  
## 请参阅  
 [Persistence Samples（持久性示例）](http://go.microsoft.com/fwlink/?LinkID=177735)