---
title: "LINQ to Entities 查询中的标准查询运算符 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 7fa55a9b-6219-473d-b1e5-2884a32dcdff
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# LINQ to Entities 查询中的标准查询运算符
在查询中，您可以指定要从数据源检索哪些信息。  查询也可以指定返回信息之前信息的排序、分组和表现方式。  LINQ 提供了一组可在查询中使用的标准查询方法。  这些方法中的大多数都在序列上进行运算；在此上下文中，序列指其类型实现 <xref:System.Collections.Generic.IEnumerable%601> 接口或 <xref:System.Linq.IQueryable%601> 接口的对象。  标准查询运算符查询功能包括筛选、投影、聚合、排序、分组和分页等。  一些更为频繁使用的标准查询运算符包含专用关键字语法，以便可通过查询表达式语法调用。  查询表达式是另一种比基于方法的等式更具可读性的查询表达方法。  查询表达式子句在编译时被转换为对查询方法的调用。  有关包含等效查询表达式子句的标准查询运算符的列表，请参见[Standard Query Operators Overview](../../../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询并不支持所有标准查询运算符。  有关更多信息，请参见[支持和不支持的 LINQ 方法 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)。本主题提供有关特定于 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 的标准查询运算符的信息。  有关 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询中的已知问题的更多信息，请参见 [LINQ to Entities 的已知问题和注意事项](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)。  
  
## 投影和筛选方法  
 “投影”是指将结果集的元素转换到所需的形式。  例如，可以从结果集中的每个对象投影所需的属性子集，可以投影一个属性并对其执行数学计算，也可以从结果集投影整个对象。  投影方法有 `Select` 和 `SelectMany`。  
  
 “筛选”是指将结果集限制为仅包含满足指定条件的元素的操作。  筛选方法为 `Where`。  
  
 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 中支持大多数投影和筛选方法的重载，除了那些接受位置参数的方法。  
  
## 联接方法  
 在面向相互之间没有可导航关系的数据源的查询中，联接是一项重要的操作。  联接两个数据源就是将一个数据源中的对象与另一个数据源中具有相同属性的对象相关联。  联接方法有 `Join` 和 `GroupJoin`。  
  
 大多数联接方法的重载都受支持，除了使用 <xref:System.Collections.Generic.IEqualityComparer%601> 的方法。  这是因为比较器不能转换为数据源。  
  
## 集方法  
 LINQ 中的集运算是根据包含或不包含本集合或其他集合（或集）中的等价元素，对其结果集执行查询运算。  集方法有 `All`、`Any`、`Concat`、`Contains`、`DefaultIfEmpty`、`Distinct`、`EqualAll`、`Except`、`Intersect` 和 `Union`。  
  
 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 中支持大多数集方法的重载，只是与 LINQ to Objects 在行为上有所不同。  但是，并不支持使用 <xref:System.Collections.Generic.IEqualityComparer%601> 的集方法，原因是比较器不能转换为数据源。  
  
## 排序方法  
 排序是指基于一个或多个属性对结果集中的元素排序。  指定多个排序条件可在组中消除并列。  
  
 大多数排序方法的重载都受支持，除了使用 <xref:System.Collections.Generic.IComparer%601> 的方法。  这是因为比较器不能转换为数据源。  排序方法有 `OrderBy`、`OrderByDescending`、`ThenBy`、`ThenByDescending` 和 `Reverse`。  
  
 由于查询在数据源上执行，因此排序行为与在 CLR 中执行的查询可能有所不同。  这是因为可以在数据源中设置诸如区分大小写排序、日本文字排序和 null 值排序等排序选项。  根据数据源的不同，这些排序选项可能会产生与 CLR 中不同的结果。  
  
 如果在多个排序操作中指定相同的关键字选择器，则会产生重复排序。  此举无效并将引发异常。  
  
## 分组方法  
 分组是指将数据分到不同的组，使每组中的元素拥有公共的属性。  分组方法为 `GroupBy`。  
  
 大多数分组方法的重载都受支持，除了使用 <xref:System.Collections.Generic.IEqualityComparer%601> 的方法。  这是因为比较器不能转换为数据源。  
  
 分组方法使用对关键字选择器的不同子查询映射到数据源。  关键字选择器比较子查询使用数据源的语义执行，其中包括与比较 `null` 值相关的问题。  
  
## 聚合方法  
 聚合运算从值的集合中计算出单个值。  例如，从一个月累计的每日温度值计算出日温度平均值就是一个聚合运算。  聚合方法有 `Aggregate`、`Average`、`Count`、`LongCount`、`Max`、`Min` 和 `Sum`。  
  
 大多数聚合方法的重载都受支持。  对于与 null 值有关的行为，聚合方法使用数据源语义。  根据使用的后端数据源的不同，聚合方法在涉及 null 值时的行为也可能会有所不同。  使用数据源语义的聚合方法行为与 CLR 方法的预期行为也可能有所不同。  例如，SQL Server 上的 `Sum` 方法的默认行为是忽略所有 null 值，而不是引发异常。  
  
 聚合导致的任何异常（如 `Sum` 函数的溢出）都会在查询结果具体化的过程中作为数据源异常或实体框架异常引发。  
  
 对于涉及序列计算的方法，如 `Sum` 和 `Average`，真正的计算将在服务器上执行。  因此，服务器上可能发生类型转换和精度损失，其结果与使用 CLR 语义预期得出的结果可能有所不同。  
  
 下表显示了聚合方法对 null 值和非 null 值的默认行为：  
  
|方法|无数据|全部 null 值|部分 null 值|无 null 值|  
|--------|---------|---------------|---------------|--------------|  
|`Average`|返回 Null。|返回 Null。|返回序列中非 null 值的平均值。|计算数值序列的平均值。|  
|`Count`|返回 0|返回序列中 null 值的个数。|返回序列中的 null 值和非 null 值个数。|返回序列中的元素数。|  
|`Max`|返回 Null。|返回 Null。|返回序列中非 null 值的最大值。|返回序列中的最大值。|  
|`Min`|返回 Null。|返回 Null。|返回序列中非 null 值的最小值。|返回序列中的最小值。|  
|`Sum`|返回 Null。|返回 Null。|返回序列中非 null 值的和。|计算数值序列的和。|  
  
## 类型方法  
 在 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 上下文中支持处理类型转换和测试的两个 LINQ 方法。  这就意味着仅支持映射到相应 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 类型的类型。  有关这些类型的列表，请参见[Conceptual Model Types \(CSDL\)](http://msdn.microsoft.com/zh-cn/987b995f-e429-4569-9559-b4146744def4)。  类型方法有 `Convert` 和 `OfType`。  
  
 对于实体类型支持 `OfType`。  对概念模型基元类型支持 `Convert`。  还支持 C\# 的 `is` 和 `as` 方法。  
  
## 分页方法  
 分页操作从序列中返回唯一、特定的元素。  这些元素方法有 `ElementAt`、`First`、`FirstOrDefault`、`Last`、`LastOrDefault`、`Single`、`Skip`、`Take` 和 `TakeWhile`。  
  
 有些分页方法不受支持，原因可能是无法将函数映射到数据源，或是数据源上缺少集的隐式排序。  返回默认值的方法仅限于默认值为 null 的概念模型基元类型和引用类型。  对空序列执行的分页方法将返回 null。  
  
## 请参阅  
 [支持和不支持的 LINQ 方法 \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)   
 [Standard Query Operators Overview](../../../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)