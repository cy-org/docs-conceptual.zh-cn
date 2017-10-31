---
title: "存储扩展性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c3f4a46-4bac-4138-ae6a-a7c7ee0d28f5
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 存储扩展性
<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 允许用户提升自定义的特定于应用程序的属性，这些属性可用于查询持久性数据库中的实例。提升属性的操作将使属性值可用在数据库的特殊视图中。这些提升的属性（可用于用户查询的属性）可以是简单的类型，如 Int64、Guid、String 和 DateTime，也可以是序列化的二进制类型 \(byte\[\]\)。  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 类具有 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.Promote%2A> 方法，可以使用该方法将某个属性提升为可以在查询中使用的属性。以下示例是存储扩展性的一个端对端示例。  
  
1.  在此示例方案中，文档处理 \(DP\) 应用程序具有多个工作流，每个工作流都使用自定义的活动进行文档处理。这些工作流具有一组状态变量，最终用户需要看到这些变量。为了实现此目的，DP 应用程序提供了一个类型为 <xref:System.Activities.Persistence.PersistenceParticipant> 的实例扩展，活动使用该实例扩展来提供状态变量。  
  
    ```  
  
    class DocumentStatusExtension : PersistenceParticipant  
    {  
        public string DocumentId;  
        public string ApprovalStatus;  
        public string UserName;  
        public DateTime LastUpdateTime;  
    }  
  
    ```  
  
2.  然后，将新的扩展添加到主机。  
  
    ```  
    static Activity workflow = CreateWorkflow();  
    WorkflowApplication application = new WorkflowApplication(workflow);  
    DocumentStatusExtension documentStatusExtension = new DocumentStatusExtension ();  
    application.Extensions.Add(documentStatusExtension);  
  
    ```  
  
     有关添加自定义持久性参与者的更多详细信息，请参见[持久性参与者](../../../docs/framework/windows-workflow-foundation//persistence-participants.md)示例。  
  
3.  DP 应用程序中的自定义活动填充 **Execute** 方法中的各种状态字段。  
  
    ```  
  
    public override void Execute(CodeActivityContext context)  
    {  
        // ...  
        context.GetExtension<DocumentStatusExtension>().DocumentId = Guid.NewGuid();  
        context.GetExtension<DocumentStatusExtension>().UserName = "John Smith";  
        context.GetExtension<DocumentStatusExtension>().ApprovalStatus = “Approved”;  
        context.GetExtension<DocumentStatusExtension>().LastUpdateTime = DateTime.Now();  
        // ...  
    }  
  
    ```  
  
4.  当工作流实例达到某个持久点时，**DocumentStatusExtension** 持久性参与者的 **CollectValues** 方法会将这些属性保存到持久性数据集合中。  
  
    ```  
  
    class DocumentStatusExtension : PersistenceParticipant  
    {  
        const XNamespace xNS = XNamespace.Get("http://contoso.com/DocumentStatus");  
  
        protected override void CollectValues(out IDictionary<XName, object> readWriteValues, out IDictionary<XName, object> writeOnlyValues)  
        {  
            readWriteValues = new Dictionary<XName, object>();  
            readWriteValues.Add(xNS.GetName("UserName"), this.UserName);  
            readWriteValues.Add(xNS.GetName("ApprovalStatus"), this.ApprovalStatus);  
            readWriteValues.Add(xNS.GetName("DocumentId"), this.DocumentId);  
            readWriteValues.Add(xNS.GetName("LastModifiedTime"), this.LastUpdateTime);  
  
            writeOnlyValues = null;  
        }  
        // ...  
    }  
  
    ```  
  
    > [!NOTE]
    >  所有这些属性由持久性框架通过 **SaveWorkflowCommand.InstanceData** 集合传递给 **SqlWorkflowInstanceStore**。  
  
5.  DP 应用程序初始化 SQL 工作流实例存储并调用 **Promote** 方法来提升此数据。  
  
    ```  
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);  
  
    List<XName> variantProperties = new List<XName>()   
    {   
        xNS.GetName("UserName"),   
        xNS.GetName("ApprovalStatus"),   
        xNS.GetName("DocumentId"),   
        xNS.GetName("LastModifiedTime")   
    };  
  
    store.Promote("DocumentStatus", variantProperties, null);  
    ```  
  
     根据此提升信息，**SqlWorkflowInstanceStore** 将数据属性放置在 [[System.Activities.DurableInstancing.InstancePromotedProperties] 视图](../Topic/Store%20Extensibility.md#InstancePromotedProperties) 的各个列中。  
  
6.  为了从提升表中查询某个数据子集，DP 应用程序在提升视图之上添加一个自定义视图。  
  
    ```  
  
    create view [dbo].[DocumentStatus] with schemabinding  
    as  
        select  P.[InstanceId] as [InstanceId],  
            P.Value1 as [UserName],  
            P.Value2 as [ApprovalStatus],  
            P.Value3 as [DocumentId],  
            P.Value4 as [LastUpdatedTime]  
    from [System.Activities.DurableInstancing].[InstancePromotedProperties] as P  
    where P.PromotionName = N'DocumentStatus'  
    go  
  
    ```  
  
##  <a name="InstancePromotedProperties"></a> \[System.Activities.DurableInstancing.InstancePromotedProperties\] 视图  
  
|列名|列类型|说明|  
|--------|---------|--------|  
|InstanceId|GUID|此提升所属的工作流实例。|  
|PromotionName|nvarchar\(400\)|提升本身的名称。|  
|Value1、Value2、Value3、..、Value32|sql\_variant|已提升属性本身的值。除了长度超过 8000 个字节的二进制 Blob 和字符串之外，多数 SQL 基元数据类型都可适合 sql\_variant。|  
|Value33、Value34、Value35、…、Value64|varbinary\(max\)|显式声明为 varbinary\(max\) 的已提升属性的值。|