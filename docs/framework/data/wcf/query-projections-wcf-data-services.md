---
title: "查询投影（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "投影 [WCF 数据服务]"
  - "查询投影 [WCF 数据服务]"
  - "WCF 数据服务, 投影"
  - "WCF 数据服务, 查询"
ms.assetid: a09f4985-9f0d-48c8-b183-83d67a3dfe5f
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 查询投影（WCF 数据服务）
投影在[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 中提供了一种机制，可通过指定仅在响应中返回实体的某些属性来减少查询返回的源中的数据量。  有关更多信息，请参见 [OData：Select 系统查询选项 \($select\)](http://go.microsoft.com/fwlink/?LinkId=186076)（可能为英文网页）。  
  
 本主题介绍如何定义查询投影、实体和非实体类型的要求、对投影的结果进行更新、创建投影的类型，还列出一些投影的注意事项。  
  
## 定义查询投影  
 可以通过在 URI 中使用 `$select` 查询选项或在 LINQ 查询中使用 [select](../Topic/select%20clause%20\(C%23%20Reference\).md) 子句（在 Visual Basic 中为 [Select](../Topic/Select%20Clause%20\(Visual%20Basic\).md)）来向查询添加投影子句。  可以将返回的实体数据投影到客户端上的实体类型或非实体类型。  本主题中的示例演示如何在 LINQ 查询中使用 `select` 子句。  
  
> [!IMPORTANT]
>  保存对投影的类型所进行的更新时，数据服务中可能会发生数据丢失。  有关更多信息，请参见[投影注意事项](#considerations)。  
  
## 实体类型和非实体类型的要求  
 实体类型必须拥有组成实体键的一个或多个标识属性。  在客户端上采用以下方式之一定义实体类型：  
  
-   将 <xref:System.Data.Services.Common.DataServiceKeyAttribute> 或 <xref:System.Data.Services.Common.DataServiceEntityAttribute> 应用于类型。  
  
-   当类型拥有一个名为 `ID` 的属性时。  
  
-   当类型拥有一个名为 *type*`ID` 的属性时，其中 *type* 是该类型的名称。  
  
 默认情况下，将查询结果投影到在客户端定义的类型时，投影中所请求的属性必须存在于客户端类型中。  但是，当为 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A> 属性指定值 `true` 时，投影中指定的属性不必出现在客户端类型中。  
  
### 对投影的结果进行更新  
 将查询结果投影到客户端上的实体类型时，<xref:System.Data.Services.Client.DataServiceContext> 可以跟踪会在调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时将更新发送回数据服务的那些对象。  但是，如果进行更新的数据投影到的是客户端上的非实体类型，则无法将更新发送回数据服务。  这是因为非实体类型没有键来标识实体实例，因此数据服务无法更新数据源中的正确实体。  非实体类型不会被附加到 <xref:System.Data.Services.Client.DataServiceContext>。  
  
 如果在数据服务中定义的某个实体类型的一个或多个属性没有出现在将该实体投影到的客户端类型中，插入新实体时将不包含这些缺少的属性。  在这种情况下，对现有实体的更新**也**不包括这些缺少的属性。  如果此类属性存在值，更新时会该属性重置为在数据源中所定义的默认值。  
  
### 创建投影的类型  
 下面的示例使用一个匿名 LINQ 查询，该查询将与地址相关的 `Customers` 类型的属性投影到新的 `CustomerAddress` 类型，该类型在客户端上定义并且属于实体类型：  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddressspecific)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddressspecific)]  
  
 在本示例中，使用对象初始值设定项模式而不是调用构造函数来创建 `CustmerAddress` 类型的新实例。  投影到实体类型时不支持构造函数，但是投影到非实体类型和匿名类型时可以使用构造函数。  由于 `CustomerAddress` 是实体类型，因此可以进行更改并将更改发送回数据服务。  
  
 此外，还将 `Customer` 类型的数据投影到 `CustomerAddress` 实体类型（而不是匿名类型）的实例。  支持投影到匿名类型，但数据将为只读数据，因为匿名类型被视为非实体类型。  
  
 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.MergeOption> 设置用于在查询投影期间标识解析。  这意味着，如果 `Customer` 类型的实例已存在于 <xref:System.Data.Services.Client.DataServiceContext> 中，则具有相同标识的 `CustomerAddress` 实例将遵循由 <xref:System.Data.Services.Client.MergeOption> 设置的标识解析规则  
  
 下表介绍将结果投影到实体类型和非实体类型时的行为：  
  
|操作|实体类型|非实体类型|  
|--------|----------|-----------|  
|使用初始值设定项创建新的投影实例，如以下示例所示：<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithInitializer](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithinitializer)]
 [!code-vb[Astoria Northwind Client#ProjectWithInitializer](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithinitializer)]|支持|支持|  
|使用构造函数创建新的投影实例，如以下示例所示：<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithConstructor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithconstructor)]
 [!code-vb[Astoria Northwind Client#ProjectWithConstructor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithconstructor)]|引发 <xref:System.NotSupportedException>。|支持|  
|使用投影来转换属性值，如下面的示例所示：<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithTransform](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithtransform)]
 [!code-vb[Astoria Northwind Client#ProjectWithTransform](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithtransform)]<br /><br /> 实体类型不支持此转换，因为这会导致混淆并且可能会覆盖数据源中属于另一个实体的数据。|引发 <xref:System.NotSupportedException>。|支持|  
  
<a name="considerations"></a>   
## 投影注意事项  
 定义查询投影时需要额外考虑下列注意事项。  
  
-   定义 Atom 格式的自定义源时，必须确保已定义自定义映射的所有实体属性都包含在投影中。  如果投影中不包含某个已映射的实体属性，则可能会丢失数据。  有关详细信息，请参阅[源自定义](../../../../docs/framework/data/wcf/feed-customization-wcf-data-services.md)。  
  
-   当对投影的类型进行插入时，如果对于数据服务的数据模型中的实体，该投影类型不包含其所有属性，则客户端上不包含在投影中的属性设置为其默认值。  
  
-   当对投影的类型进行更新时，如果对于数据服务的数据模型中的实体，该投影类型不包含其所有属性，则客户端上不包含在投影中的现有值将被未初始化的默认值覆盖。  
  
-   当投影包括复杂属性时，必须返回整个复杂对象。  
  
-   当投影包括导航属性时，会隐式加载相关对象，而无需调用 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 方法。  不支持在投影的查询中使用 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 方法。  
  
-   在客户端上进行查询的查询投影在请求 URI 中转换为使用 `$select` 查询选项。  针对不支持 `$select` 的以前版本的 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]执行带投影的查询时，会返回错误。将数据服务的 <xref:System.Data.Services.DataServiceBehavior> 的 <xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A> 设置为值 <xref:System.Data.Services.Common.DataServiceProtocolVersion> 时，也会返回错误。  有关详细信息，请参阅[数据服务版本管理](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md)。  
  
 有关详细信息，请参阅[如何：投影查询结果](../../../../docs/framework/data/wcf/how-to-project-query-results-wcf-data-services.md)。  
  
## 请参阅  
 [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)