---
title: "泛型 Field 和 SetField 方法 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1883365f-9d6c-4ccb-9187-df309f47706d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 泛型 Field 和 SetField 方法 (LINQ to DataSet)
[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 为 <xref:System.Data.DataRow> 类提供用于访问列值的扩展方法：<xref:System.Data.DataRowExtensions.Field%2A> 方法和 <xref:System.Data.DataRowExtensions.SetField%2A> 方法。这些方法使开发人员能够更轻松地访问列值，特别是 null 值。<xref:System.Data.DataSet> 使用 <xref:System.DBNull.Value> 来表示 null 值，而 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 使用 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 中引入的可以为 null 的类型支持。  使用 <xref:System.Data.DataRow> 中预先存在的列访问器需要将返回对象强制转换成相应的类型。  如果 <xref:System.Data.DataRow> 中的特定字段可以为 null，则必须显示检查 Null 值，因为返回 <xref:System.DBNull.Value> 并隐式地将其强制转换为另一种类型会引发 <xref:System.InvalidCastException>。  在下面的示例中，如果不使用 <xref:System.Data.DataRow.IsNull%2A> 方法检查 Null 值，则在索引器返回 <xref:System.DBNull.Value> 并试图将其强制转换为 <xref:System.String> 的情况下会引发异常。  
  
 [!code-csharp[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#whereisnull)]
 [!code-vb[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#whereisnull)]  
  
 <xref:System.Data.DataRowExtensions.Field%2A> 方法提供对 <xref:System.Data.DataRow> 列值的访问，而 <xref:System.Data.DataRowExtensions.SetField%2A> 设置 <xref:System.Data.DataRow>中的列值。  <xref:System.Data.DataRowExtensions.Field%2A> 方法和 <xref:System.Data.DataRowExtensions.SetField%2A> 方法都可以处理可以为 null 的类型，因此不必像前面的示例那样检查 Null 值。  这两种方法也都是泛型方法，因此不必强制转换返回类型。  
  
 下面的示例使用 <xref:System.Data.DataRowExtensions.Field%2A> 方法。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where3)]
 [!code-vb[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where3)]  
  
 请注意，<xref:System.Data.DataRowExtensions.Field%2A> 方法和 <xref:System.Data.DataRowExtensions.SetField%2A> 方法的泛型参数 `T` 中指定的数据类型必须与基础值的类型相匹配。  否则，将引发 <xref:System.InvalidCastException> 异常。  指定的列名称也必须与 <xref:System.Data.DataSet> 中的列名称相匹配，否则将引发 <xref:System.ArgumentException>。  在这两种情况下，异常都是在执行查询期间的运行时数据枚举时引发的。  
  
 <xref:System.Data.DataRowExtensions.SetField%2A> 方法本身不执行任何类型转换。  但这并不意味着不会发生类型转换。  <xref:System.Data.DataRowExtensions.SetField%2A> 方法公开 <xref:System.Data.DataRow> 类的 [!INCLUDE[ado_whidbey_long](../../../../includes/ado-whidbey-long-md.md)] 行为。  类型转换可以由 <xref:System.Data.DataRow> 对象执行，转换的值随后将保存到 <xref:System.Data.DataRow> 对象。  
  
## 请参阅  
 <xref:System.Data.DataRowExtensions>