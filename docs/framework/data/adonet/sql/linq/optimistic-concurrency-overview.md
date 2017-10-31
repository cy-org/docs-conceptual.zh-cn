---
title: "开放式并发：概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2e38512-d0c8-4807-b30a-cb7e30338694
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 开放式并发：概述
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持开放式并发控制。  下表介绍 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 文档中涉及开放式并发的术语：  
  
|术语|描述|  
|--------|--------|  
|并发|两个或更多用户同时尝试更新同一数据库行的情形。|  
|并发冲突|两个或更多用户同时尝试向一行的一列或多列提交冲突值的情形。|  
|并发控制|用于解决并发冲突的技术。|  
|开放式并发控制|先调查其他事务是否已更改了行中的值，再允许提交更改的技术。<br /><br /> 相比之下，保守式并发控制则是通过锁定记录来避免发生并发冲突。<br /><br /> 之所以称作开放式控制，是因为它将一个事务干扰另一事务视为不太可能发生。|  
|冲突解决|通过重新查询数据库刷新出现冲突的项，然后协调差异的过程。<br /><br /> 刷新对象时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 更改跟踪器会保留以下数据：<br /><br /> -   最初从数据库获取并用于更新检查的值。<br />-   通过后续查询获得的新数据库值。<br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 随后会确定相应对象是否发生冲突（即它的一个或多个成员值是否已发生更改）。  如果此对象发生冲突，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 下一步会确定它的哪些成员发生冲突。<br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 发现的任何成员冲突都会添加到冲突列表中。|  
  
 在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 对象模型中，当以下两个条件都得到满足时，就会发生“开放式并发冲突”：  
  
-   客户端尝试向数据库提交更改。  
  
-   数据库中的一个或多个更新检查值自客户端上次读取它们以来已得到更新。  
  
 此冲突的解决过程包括查明对象的哪些成员发生冲突，然后决定您希望如何进行处理。  
  
> [!NOTE]
>  只有映射为 <xref:System.Data.Linq.Mapping.UpdateCheck> 或 <xref:System.Data.Linq.Mapping.UpdateCheck> 的成员才会参与开放式并发检查。  对于标记为 <xref:System.Data.Linq.Mapping.UpdateCheck> 的成员，不执行检查。  有关详细信息，请参阅<xref:System.Data.Linq.Mapping.UpdateCheck>。  
  
## 示例  
 例如，在下面的情况中，User1 通过查询数据库中的某一行开始准备更新。  User1 收到包含 Alfreds、Maria 和 Sales 值的一行。  
  
 User1 希望将 Manager 列的值更改为 Alfred，将 Department 列的值更改为 Marketing。  在 User2 将更改提交到数据库后，User1 才能提交这些更改。  所以，现在 Assistant 列的值已更改为 Mary，Department 列的值已更改为 Service。  
  
 当 User1 现在尝试提交更改时，提交失败并且引发 <xref:System.Data.Linq.ChangeConflictException> 异常。  出现这种结果是因为 Assistant 列和 Department 列的数据库值并不是他们所预期的那些值。  表示 Assistant 和 Department 列的成员发生了冲突。  下表对这种情形作了总结。  
  
||Manager|Assistant|Department|  
|------|-------------|---------------|----------------|  
|原始状态|Alfreds|Maria|销售额|  
|User1|Alfred||Marketing|  
|User2||Mary|服务|  
  
 您可以用多种不同的方式来解决此类冲突。  有关详细信息，请参阅[如何：管理更改冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)。  
  
## 冲突检测和解决检查表  
 您可以检测和解决任意详细等级的冲突。  一种极端情况是，您可以用三种方式之一（请参见 <xref:System.Data.Linq.RefreshMode>）来解决所有冲突，而不再作其他方面的考虑。  另一种极端情况是，您可以为发生冲突的每个成员上的每种冲突指定特定操作。  
  
-   在您的对象模型中指定或修改 <xref:System.Data.Linq.Mapping.UpdateCheck> 选项。  
  
     有关详细信息，请参阅[如何：指定测试哪些成员是否发生并发冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)。  
  
-   在对 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 的调用的 try\/catch 块中，指定您希望在哪个点引发异常。  
  
     有关详细信息，请参阅[如何：指定并发异常的引发时间](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-when-concurrency-exceptions-are-thrown.md)。  
  
-   决定您希望检索的冲突详细信息量，并在 try\/catch 块中包括相应的代码。  
  
     有关详细信息，请参阅[如何：检索实体冲突信息](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-entity-conflict-information.md)和[如何：检索成员冲突信息](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-member-conflict-information.md)。  
  
-   在 `try`\/`catch` 代码中包括您希望解决您发现的各种冲突的方式。  
  
     有关详细信息，请参阅[如何：通过保留数据库值解决冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-retaining-database-values.md)、[如何：通过覆盖数据库值解决冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-overwriting-database-values.md)和[如何：通过与数据库值合并解决并发冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-merging-with-database-values.md)。  
  
## 支持冲突发现和解决的 LINQ to SQL 类型  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中支持解决开放式并发冲突的类和功能包括：  
  
-   <xref:System.Data.Linq.ObjectChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.MemberChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictCollection?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictException?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.ChangeConflicts%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.Refresh%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.UpdateCheck?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.RefreshMode?displayProperty=fullName>  
  
## 请参阅  
 [如何：管理更改冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)