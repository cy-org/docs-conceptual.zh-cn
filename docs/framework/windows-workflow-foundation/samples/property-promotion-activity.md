---
title: "属性提升活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 802196b7-1159-4c05-b41b-d3bfdfcc88d9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 属性提升活动
本示例提供了将 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 提升功能直接集成到工作流创作体验的端到端解决方案。提供了一组用于简化对提升功能的使用的配置元素、工作流活动和工作流扩展。此外，该示例包含一个演示如何使用此集合的简单工作流。  
  
> [!NOTE]
>  提供的示例仅供教学使用。这些示例不是针对生产环境设计的，也没有在生产环境中进行测试。对于这些示例，Microsoft 不提供相关的技术支持。  
  
## 必备条件  
  
-   已初始化的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 数据库  
  
-   [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]  
  
## 示例项目  
  
-   **PropertyPromotionActivity** 项目包含与特定于提升的配置元素、工作流活动和工作流扩展相关的文件。  
  
-   **CounterServiceApplication** 项目包含一个使用 **SqlWorkflowInstanceStorePromotion** 项目的示例工作流。  
  
-   一个必须对 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 数据库运行的 SQL 脚本 \(PropertyPromotionActivitySQLSample.sql\)。  
  
-   一个链接两个 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 项目的解决方案文件 \(`PropertyPromotionActivity.sln`\)  
  
## 设置和运行示例  
  
1.  初始化工作流持久性数据库。  
  
    1.  导航到示例目录 \(\\WF\\Basic\\Persistence\\PropertyPromotionActivity\)，然后运行 CreateInstanceStore.cmd。  
  
    2.  如果管理员权限不可用，则创建 SQL Server 登录。在 SQL Server Management Studio 中，转到**“安全性”**和**“登录”**。右击**“登录”**，创建一个新的登录。通过依次打开**“数据库”**、**“InstanceStore”**和**“安全性”**，将 ACL 用户添加到 SQL 角色。右击**“用户”**，然后选择**“新建用户”**。将**“登录名”**设置为在上面创建的用户。将该用户添加到数据库角色成员 System.Activities.DurableInstancing.InstanceStoreUsers（以及其他成员）。请注意，该用户可能已经存在（例如，用户 dbo）。  
  
2.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开解决方案文件 PropertyPromotionActivity.sln。  
  
3.  如果已在 SQL Server Express 本地安装之外的数据库中创建实例存储区，则必须更新数据库连接字符串。通过设置 `sqlWorkflowInstanceStorePromotion` 节点上的 `connectionString` 属性的值，使其指向步骤 1 中初始化的持久性数据库来更改 **CounterServiceApplication** 下的 App.config 文件。  
  
4.  生成并运行解决方案。这将启动计数器 WF 服务并自动启动一个工作流实例。  
  
5.  快速选择持久性数据库中的 \[dbo\].\[CounterService\] 视图中的所有行（步骤 1 中通过运行 CreateInstanceStore.cmd 添加了此视图）。您将看到与下面的内容类似的结果集：  
  
    |InstanceId|CounterValue|CounterValueLastUpdated|  
    |----------------|------------------|-----------------------------|  
    |2FA2C302\-929E\-4C0D\-8C25\-768A3DA20CE5|12|2010\-02\-18 22:48:01.740|  
  
     在连续刷新视图时，您会发现，CounterValue 和 CounterValueLastUpdated 将每两秒更改一次。这是计数器自行更新的时间间隔。CounterValue 和 CounterValueLastUpdated 表示此工作流的已提升属性。  
  
## 移除示例  
  
-   在示例目录 \(\\WF\\Basic\\Persistence\\PropertyPromotionActivity\) 中运行 RemoveInstanceStore.cmd。  
  
## 了解此示例  
 此示例包含两个项目和一个 SQL 文件：  
  
-   **CounterServiceApplication** 是一个承载简单计数器 WF 服务的控制台应用程序。在通过 `Start` 终结点接收单向消息后，工作流将从 0 计数到 29，并每两秒递增一个计数器变量。在每个计数器递增后，工作流将保留，并将在 \[dbo\].\[CounterService\] 视图中更新已提升的属性。在运行控制台应用程序时，它会承载 WF 服务并向 `Start` 终结点发送一条消息，由此创建计数器 WF 实例。  
  
-   **PropertyPromotionActivity** 是一个包含 **CounterServiceApplication** 使用的配置元素、工作流活动和工作流扩展的类库。  
  
-   **PropertyPromotionActivitySQLSample.sql** 会创建视图 \[dbo\].\[CounterService\] 并将该视图添加到数据库。  
  
### CounterServiceApplication  
  
#### 使用 SqlWorkflowInstanceStorePromotion 配置元素  
 `SqlWorkflowInstanceStorePromotion` 配置元素继承自 `SqlWorkflowInstanceStore` 配置元素，但添加了一个称作 `promotionSets` 的附加配置元素。使用 `promotionSets` 元素，用户可通过配置指定提升的属性。这是由此示例使用的配置文件：  
  
```xml  
<sqlWorkflowInstanceStorePromotion connectionString ="Data Source=.;Initial Catalog=SqlWorkflowInstanceStoreTest;Integrated Security=True;">  
  <promotionSets>  
    <promotionSet name="CounterService">  
      <promotedValue propertyName="Count"/>  
      <promotedValue propertyName="LastIncrementedAt"/>  
    </promotionSet>  
  </promotionSets>  
</sqlWorkflowInstanceStorePromotion>  
```  
  
 检查 \[dbo\].\[CounterService\] 视图的定义。  
  
```sql  
create view [dbo].[CounterService] as  
      select [InstanceId],  
 [Value1] as [CounterValue],  
 [Value2] as [CounterValueLastUpdated]  
      from [System.Activities.DurableInstancing].[InstancePromotedProperties]  
      where [PromotionName] = 'CounterService'  
go  
  
```  
  
 当工作流实例保留时，将在配置中定义的每个 `PromotionSet` 的 `InstancePromotedProperties` 视图中插入一行。此行包含 `PromotionSet` 的所有已提升的属性（一个列对应一个已提升的属性）。此 `PromotionSet` 由元组 `InstanceId, PromotionName` 进行键控。此示例中具有一个配置中定义的 `PromotionSet`，其 name 属性为 `CounterService`。请注意，`PromotionName` 列值与 `PromotionSet` 元素的 name 属性的相等程度。  
  
 `promotedValue` 元素的顺序与已提升的属性在 `InstancePromotedProperties` 视图中的位置有关。`Count` 是第一个 `promotedValue` 元素。因此，它将映射到 `InstancePromotedProperties` 视图中的 `Value1` 列。`LastIncrementedAt` 是第二个 `promotedValue` 元素。因此，它将映射到 `InstancePromotedProperties` 视图中的 `Value2` 列。  
  
#### 使用 PromoteValue 活动  
 检查 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 设计器中的 CounterService.xamlx 文件。请注意，WF 定义中包含两个特殊活动：`PromoteValue<DateTime>` 和 `PromoteValue<Int32>`。  
  
 `PromoteValue<Int32>` 活动的 `Name` 成员已定义为 `Count`。这与配置中的第一个 `promotedValue` 元素匹配，并且其 `Value` 已定义为 `Counter` 工作流变量。当工作流保留时，`Counter` 工作流变量将作为已提升的属性保留到 `InstancePromotedProperties` 视图的 `Value1` 列中。  
  
 `PromoteValue<DateTime>` 活动的 `Name` 成员已定义为 `LastIncrementedAt`。这与配置中的第二个 `promotedValue` 元素匹配，并且其 `Value` 已定义为 `TimeLastIncremented` 工作流变量。这意味着，当工作流保留时，`TimeLastIncremented` 工作流变量的值将作为已提升的属性保留到 `InstancePromotedProperties` 视图的 `Value2` 列中。  
  
 请注意，`PromotedValue` 活动还具有一个称作 `ClearExistingPromotedData` 的 Boolean 成员。在将此成员设置为 `true` 时，将清除工作流中该点之前的所有已提升的属性值。例如，如果将 Sequence 活动定义为如下内容：  
  
1.  PromoteValue { Name \= “Count”, Value \= 3}  
  
2.  PromoteValue {Name \= “LastIncrementedAt”, Value \= 1\-1\-2000 }  
  
3.  持久  
  
4.  PromoteValue {Name \= “Count”, Value \= 4, ClearExistingPromotedData \= true}  
  
5.  持久  
  
 在第二次保留时，`Count` 的已提升的值将为 4。但 `LastIncrementedAt` 的已提升的值将为 `NULL`。如果步骤 4 中未将 `ClearExistingPromotedData` 设置为 `true`，则在第二次保留之后，Count 的已提升的值将为 4。因此，`LastIncrementedAt` 的已提升的值仍将为 1\-1\-2000。  
  
### PropertyPromotionActivity  
 此类库包含以下用于简化对 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 提升功能的使用的公共类。  
  
#### PromoteValue 类  
 此类可提升一个属性。已提升的属性的名称应与配置中的 `promotedValue` 元素的 name 属性匹配。可在工作流设计器中使用此活动。有关示例用法，请参见 CounterServiceApplication。  
  
```csharp  
public class PromoteValue<T> : CodeActivity  
{  
    public PromoteValue()  
    {  
    }  
  
    public bool ClearExistingPromotedData { get; set; }  
    public string Name { get; set; }  
    public InArgument<T> Value { get; set; }  
}  
  
```  
  
 ClearExistingPromotedData \(Bool\)  
 清除在此活动之前已提升的所有值。  
  
 Name \(string\)  
 表示此属性的名称。此名称应与配置中的 \<promotedValue\> 元素的 name 属性匹配。  
  
 Value \(InArgument\<T\>\)  
 要存储在列中的变量\/值。  
  
#### PromoteValues 类  
 提升多个属性。已提升的属性的名称应与配置中的 `promotedValue` 元素中的所有 name 属性匹配。用法与 `PromoteValue` 活动相似，只不过可同时提升多个属性。无法在工作流设计器中使用此活动。  
  
```  
public class PromoteValues : CodeActivity  
{  
    public PromoteValues()  
    {  
        this.ValuesToPromote = new Dictionary<string, InArgument>();  
    }  
  
    public bool ClearExistingPromotedData { get; set; }  
    public IDictionary<string, InArgument> ValuesToPromote { get; set; }  
}  
```  
  
#### SqlWorkflowInstanceStorePromotionBehavior  
 派生自 `SqlWorkflowInstanceStoreBehavior`。此派生类会将自定义持久性参与者（也是此库的一部分）添加为工作流扩展。前两个工作流活动的实现依赖于此自定义持久性参与者。  
  
```  
public class SqlWorkflowInstanceStorePromotionBehavior :  
             SqlWorkflowInstanceStoreBehavior, IServiceBehavior  
{  
        public void Promote(string name, IEnumerable<string> promoteAsSqlVariant,  
                            IEnumerable<string> promoteAsBinary)  
  
}  
  
```  
  
 此类库还包含 `SqlWorkflowInstanceStorePromotionElement` 的 `ConfigurationElement` 实现和前面的提升活动所使用的自定义持久性参与者。  
  
### PropertyPromotionActivitySQLSample  
 此 SQL 文件会创建 `[dbo].[CounterService]` 视图以及用于查询具有 CounterService 提升集的所有实例的 `[InstancePromotedProperties]` 视图。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Persistence\PropertyPromotionActivity`  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)