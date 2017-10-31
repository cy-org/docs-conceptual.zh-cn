---
title: "持久性数据库架构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34f69f4c-df81-4da7-b281-a525a9397a5c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 持久性数据库架构
本主题介绍 SQL 工作流实例存储区支持的公共视图。  
  
## Instances 视图  
 **Instances** 视图包含有关数据库中所有工作流实例的常规信息。  
  
|列名|列类型|说明|  
|--------|---------|--------|  
|InstanceId|UniqueIdentifier|工作流实例的 ID。|  
|PendingTimer|DateTime|指示工作流在延迟活动上发生阻塞，并将在计时器过期后恢复。如果在等待计时器过期时工作流没有发生阻塞，则此值可以为 null。|  
|CreationTime|DateTime|指示创建工作流的时间。|  
|LastUpdatedTime|DateTime|指示将工作流持久化到数据库的最后时间。|  
|ServiceDeploymentId|BigInt|用作 \[ServiceDeployments\] 视图的外键。如果当前工作流实例为 Web 承载的服务的实例，则此列具有一个值，否则将其设置为 NULL。|  
|SuspensionExceptionName|Nvarchar\(450\)|指示异常的类型（例如InvalidOperationException），导致工作流暂停。|  
|SuspensionReason|Nvarchar\(max\)|指示将工作流实例挂起的原因。如果某个异常造成实例挂起，则此列包含与该异常关联的消息。<br /><br /> 如果该实例是手动挂起，则此列包含用户指定的挂起该实例的原因。|  
|ActiveBookmarks|Nvarchar\(max\)|如果工作流实例处于空闲状态，则此属性指示该实例是在哪个书签上发生阻塞的。如果该实例没有处于空闲状态，则此列为 NULL。|  
|CurrentMachine|Nvarchar\(128\)|指示当前已将工作流实例加载到内存中的计算机的名称。|  
|LastMachine|Nvarchar\(450\)|指示最后加载工作流实例的计算机。|  
|ExecutionStatus|Nvarchar\(450\)|指示工作流的当前执行状态。可能的状态包括 **Executing**、**Idle** 和 **Closed**。|  
|IsInitialized|Bit|指示工作流实例是否已初始化。已初始化的工作流实例是至少已持久化一次的工作流实例。|  
|IsSuspended|Bit|指示工作流实例是否已挂起。|  
|IsCompleted|Bit|指示工作流实例是否已执行完毕。 **Note:**  如果 **InstanceCompletionAction** 属性设置为 **DeleteAll**，则在完成后从视图中移除实例。|  
|EncodingOption|TinyInt|描述用于序列化数据属性的编码。<br /><br /> -   0 – 无编码<br />-   1 – GzipStream|  
|ReadWritePrimitiveDataProperties|Varbinary\(max\)|包含已序列化的实例数据属性，当加载实例时，这些属性将会重新提供给工作流运行时。<br /><br /> 每个基元属性都是本机 CLR 类型，这意味着，对 Blob 进行反序列化不需要特殊程序集。|  
|WriteOnlyPrimitiveDataProperties|Varbinary\(max\)|包含已序列化的实例数据属性，当加载实例时，这些属性不会重新提供给工作流运行时。<br /><br /> 每个基元属性都是本机 CLR 类型，这意味着，对 Blob 进行反序列化不需要特殊程序集。|  
|ReadWriteComplexDataProperties|Varbinary\(max\)|包含已序列化的实例数据属性，当加载实例时，这些属性将会重新提供给工作流运行时。<br /><br /> 反序列化程序需要知道此 Blob 中存储的所有对象类型。|  
|WriteOnlyComplexDataProperties|Varbinary\(max\)|包含已序列化的实例数据属性，当加载实例时，这些属性不会重新提供给工作流运行时。<br /><br /> 反序列化程序需要知道此 Blob 中存储的所有对象类型。|  
|IdentityName|Nvarchar\(max\)|工作流定义的名称|  
|标识包|Nvarchar\(max\)|创建工作流时提供的包信息（例如，程序集名称）。|  
|生成|BigInt|工作流版本的生成号。|  
|Major|BigInt|工作流的主版本号。|  
|Minor|BigInt|工作流的次版本号。|  
|修订|BigInt|工作流版本的修订号。|  
  
> [!CAUTION]
>  **Instances** 视图还包含一个“删除”触发器。具有适当权限的用户可以对此视图执行 Delete 语句，这将从数据库中强制移除工作流实例。由于从工作流运行时的下面删除实例可能会导致意外的结果，所以，建议不到万不得已，不要直接从视图删除，而应使用工作流实例管理终结点来使工作流运行时终止实例。如果需要从视图中删除大量实例，请确保没有可能正在对这些实例进行操作的活动的运行时。  
  
## ServiceDeployments 视图  
 **ServiceDeployments** 视图包含所有 Web \(IIS\/WAS\) 承载的工作流服务的部署信息。每个 Web 承载的工作流实例将包含一个 **ServiceDeploymentId**，引用此视图中的一行。  
  
|列名|列类型|说明|  
|--------|---------|--------|  
|ServiceDeploymentId|BigInt|此视图的主键。|  
|SiteName|Nvarchar\(max\)|代表包含工作流服务的站点的名称（例如**“默认网站”**）。|  
|RelativeServicePath|Nvarchar\(max\)|表示相对于指向工作流服务的站点的虚拟路径（例如**\/app1\/PurchaseOrderService.svc**）。|  
|RelativeApplicationPath|Nvarchar\(max\)|表示相对于指向包含工作流服务的应用程序的站点的虚拟路径（例如**\/app1**）。|  
|ServiceName|Nvarchar\(max\)|表示工作流服务的名称（例如**PurchaseOrderService**）。|  
|ServiceNamespace|Nvarchar\(max\)|表示工作流服务的命名空间（例如**MyCompany**）。|  
  
 ServiceDeployments 视图还包含一个“删除”触发器。具有适当权限的用户可以对此视图执行 Delete 语句，这将从数据库移除 ServiceDeployment 项。请注意：  
  
1.  从此视图中删除项的开销很大，因为在执行此操作之前必须锁定整个数据库。为了避免出现工作流实例可能引用一个不存在的 ServiceDeployment 项的情况，这是必需的。请仅在停机期间\/维护期间在此视图中进行删除操作。  
  
2.  任何删除由 **Instances** 视图中的项引用的 ServiceDeployment 行的尝试都将导致不执行任何操作。仅可以删除没有任何引用的 ServiceDeployment 行。  
  
## InstancePromotedProperties 视图  
 **InstancePromotedProperties** 视图包含由用户指定的所有促销属性的信息。促销属性用作一类属性，用户可以在查询中使用它来检索实例。例如，用户可以添加 PurchaseOrder 促销，它始终会在 **Value1** 列中存储订单的成本。这样用户可以查询所有成本超过某个值的购买订单。  
  
||||  
|-|-|-|  
|列名称|列类型|说明|  
|InstanceId|UniqueIdentifier|工作流实例的 ID|  
|EncodingOption|TinyInt|描述用于序列化促销二进制属性的编码。<br /><br /> -   0 – 无编码<br />-   1 – GZipStream|  
|PromotionName|Nvarchar\(400\)|与此实例关联的促销的名称。需要 PromotionName 来在此行的一般列中添加上下文。<br /><br /> 例如，PurchaseOrder 的 PromotionName 可能指示 Value1 包含订单成本，Value2 包含下订单的客户的名称，Value 3 包含客户地址，等等。|  
|Value\[1\-32\]|SqlVariant|Value\[1\-32\] 包含可以在 SqlVariant 列中存储的值。单次促销包含的 SqlVariant 不能超过 32 个。|  
|值\[33\-64\]|Varbinary\(max\)|值\[33\-64\] 包含可序列化的值。例如 Value33 可能包含购买项的一个 JPEG。单个促销包含的 SqlVariant 不能超过 32 个。|  
  
 InstancePromotedProperties 视图与架构绑定在一起，这意味着，用户可以在一个列或多个列上添加索引，以便针对此视图优化查询。  
  
> [!NOTE]
>  索引视图需要更大的存储空间，并增加额外的处理开销。有关更多信息，请参考[使用 SQL Server 2008 索引视图提高性能](http://go.microsoft.com/fwlink/?LinkId=179529)（可能为英文网站）。