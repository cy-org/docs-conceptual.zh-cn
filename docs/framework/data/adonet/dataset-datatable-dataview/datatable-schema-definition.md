---
title: "DataTable 架构定义 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTable 架构定义
表的架构（即结构）由列和约束表示。  使用 <xref:System.Data.DataColumn> 对象以及 <xref:System.Data.ForeignKeyConstraint> 和 <xref:System.Data.UniqueConstraint> 对象定义 <xref:System.Data.DataTable> 的架构。  表中的列可以映射到数据源中的列、包含从表达式计算所得的值、自动递增它们的值，或包含主键值。  
  
 按名称引用表中的列、关系和约束是区分大小写的。  因此，一个表中可以存在两个或两个以上名称相同（但大小写不同）的列、关系或约束。  例如，您可以有 **Col1** 和 **col1**。  在这种情况下，按名称引用某一列就必须完全符合该列名的大小写，否则会引发异常。  例如，如果表 **myTable** 包含列 **Col1** 和列 **col1**，就要以 **myTable.Columns\["Col1"\]** 的形式来按名称引用 **Col1**，而以 **myTable.Columns\["col1"\]** 的形式按名称引用 **col1**。  尝试以 **myTable.Columns\["COL1"\]** 的形式来引用其中某列就会产生异常。  
  
 如果某个特定名称只存在一个列、关系或约束，则不应用区分大小写规则。  也就是说，如果表中没有其他的列、关系或约束对象与该特定列、关系或约束对象的名称匹配，您就可以使用任意的大小写来按名称引用该对象，并且不会引发异常。  例如，如果表中只有 **Col1**，您就可以使用 **my.Columns\["COL1"\]** 来引用。  
  
> [!NOTE]
>  **DataTable** 的 <xref:System.Data.DataTable.CaseSensitive%2A> 属性不影响此行为。  **CaseSensitive** 属性应用于表中的数据，并会影响排序、搜索、筛选、执行约束，等等，但是不应用于对列、关系和约束的引用。  
  
## 本节内容  
 [向数据表中添加列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-columns-to-a-datatable.md)  
 说明如何使用 **DataColumn** 对象来定义表中的列。  
  
 [创建表达式列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-expression-columns.md)  
 说明如何使用列的 **Expression** 属性来计算值（根据行中其他列中的值）。  
  
 [创建 AutoIncrement 列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)  
 说明如何将列设置为自动递增数值，以确保每行都有唯一的列值。  
  
 [定义主键](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)  
 说明如何从一个或多个 **DataColumn** 对象中指定表的主键。  
  
 [数据表约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)  
 说明如何为表中的列定义外键和唯一约束。  
  
## 请参阅  
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)