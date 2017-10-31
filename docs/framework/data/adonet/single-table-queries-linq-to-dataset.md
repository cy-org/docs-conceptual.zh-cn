---
title: "单表查询 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b74bcf8-3f87-449f-bff7-6bcb0d69d212
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 单表查询 (LINQ to DataSet)
[!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 查询适用于实现 <xref:System.Collections.Generic.IEnumerable%601> 接口或 <xref:System.Query.IQueryable%601> 接口的数据源。  <xref:System.Data.DataTable> 类不实现任何一个接口，所以如果要使用 <xref:System.Data.DataTable> 作为[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询的 `From` 子句中的源，则必须调用 <xref:System.Data.DataTableExtensions.AsEnumerable%2A> 方法。  
  
 下面的示例获取 SalesOrderHeader 表中的所有联机订单并将订单 ID、订单日期和订单编号输出到控制台。  
  
 [!code-csharp[dp linq to dataset examples#Where1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where1)]
 [!code-vb[dp linq to dataset examples#Where1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where1)]  
  
 本地变量查询使用查询表达式进行初始化，该表达式通过应用标准查询运算符中的一个或多个查询运算符，或者在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 的情况下应用特定于 <xref:System.Data.DataSet> 类的一个或多个运算符对一个或多个信息源进行运算。  前面示例中的查询表达式使用两个标准查询运算符：`Where` 和 `Select`。  
  
 `Where` 子句基于条件筛选序列，在本例中，`OnlineOrderFlag` 设置为 `true`。  `Select` 运算符分配并返回一个可枚举对象，该对象可捕获传递给运算符的参数。  在上面的示例中，创建了一个具有三个属性的匿名类型：`SalesOrderID`、`OrderDate` 和 `SalesOrderNumber`。  这三个属性的值设置为 `SalesOrderHeader` 表中的 `SalesOrderID`、`OrderDate` 和 `SalesOrderNumber` 列值。  
  
 然后，`foreach` 循环枚举由 `Select` 返回的可枚举对象，并生成查询结果。  由于查询是一种可以实现 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Linq.Enumerable> 类型，因此，查询的计算将推迟到使用 `foreach` 循环来循环访问查询变量之后进行。  推迟查询计算可使查询保持为可进行多次计算的值，每次计算都可能生成不同的结果。  
  
 <xref:System.Data.DataRowExtensions.Field%2A> 方法提供对 <xref:System.Data.DataRow> 列值的访问，而 <xref:System.Data.DataRowExtensions.SetField%2A>（前面的示例未演示）设置 <xref:System.Data.DataRow> 中的列值。  <xref:System.Data.DataRowExtensions.Field%2A> 方法和 <xref:System.Data.DataRowExtensions.SetField%2A> 方法都可以处理可以为 null 的类型，因此不必显式检查 null 值。  这两种方法也都是泛型方法，这意味着您不必强制转换返回类型。  您可以使用 <xref:System.Data.DataRow> 中预先存在的列访问器（例如 `o["OrderDate"]`），但是这样做要求您将返回对象强制转换为相应的类型。  如果列可以为 null，则必须使用 <xref:System.Data.DataRow.IsNull%2A> 方法检查值是否为 null。  有关详细信息，请参阅[泛型 Field 和 SetField 方法](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md)。  
  
 请注意，<xref:System.Data.DataRowExtensions.Field%2A> 方法和 <xref:System.Data.DataRowExtensions.SetField%2A> 方法的泛型参数 `T` 中指定的数据类型必须与基础值的类型相匹配，否则将引发 <xref:System.InvalidCastException>。  指定的列名称也必须与 <xref:System.Data.DataSet> 中的列名称相匹配，否则将引发 <xref:System.ArgumentException>。  在这两种情况下，异常都是在执行查询期间的运行时数据枚举时引发的。  
  
## 请参阅  
 [交叉表查询](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)   
 [查询类型化数据集](../../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [泛型 Field 和 SetField 方法](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md)