---
title: "处理 DataTable 事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62f404a5-13ea-4b93-a29f-55b74a16c9d3
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 处理 DataTable 事件
<xref:System.Data.DataTable> 对象提供一系列可以由应用程序处理的事件。  下表描述了 `DataTable` 事件。  
  
|Event|描述|  
|-----------|--------|  
|<xref:System.Data.DataTable.Initialized>|在调用 `DataTable` 的 <xref:System.Data.DataTable.EndInit%2A> 方法后发生。  此事件主要用于支持设计时方案。|  
|<xref:System.Data.DataTable.ColumnChanged>|在成功更改 <xref:System.Data.DataColumn> 中的值后发生。|  
|<xref:System.Data.DataTable.ColumnChanging>|提交 `DataColumn` 的值后发生。|  
|<xref:System.Data.DataTable.RowChanged>|在成功更改 `DataColumn` 值或 `DataTable` 中 <xref:System.Data.DataRow> 的 <xref:System.Data.DataRow.RowState%2A> 后发生。|  
|<xref:System.Data.DataTable.RowChanging>|在提交对 `DataColumn` 值或 `DataTable` 中 `DataRow` 的 `RowState` 的更改后发生。|  
|<xref:System.Data.DataTable.RowDeleted>|在 `DataTable` 中的 `DataRow` 已标记为 `Deleted` 后发生。|  
|<xref:System.Data.DataTable.RowDeleting>|在 `DataTable` 中的 `DataRow` 标记为 `Deleted` 前发生。|  
|<xref:System.Data.DataTable.TableCleared>|在对 `DataTable` 的 <xref:System.Data.DataTable.Clear%2A> 方法的调用已成功清除每个 `DataRow` 后发生。|  
|<xref:System.Data.DataTable.TableClearing>|在调用 `Clear` 方法后，开始执行 `Clear` 操作前发生。|  
|<xref:System.Data.DataTable.TableNewRow>|在对 `DataTable` 的 `NewRow` 方法的调用创建了新 `DataRow` 后发生。|  
|<xref:System.ComponentModel.MarshalByValueComponent.Disposed>|在 `DataTable` 被 `Disposed` 时发生。  从 <xref:System.ComponentModel.MarshalByValueComponent> 继承。|  
  
> [!NOTE]
>  添加或删除行的大多数操作不会引发 `ColumnChanged` 和 `ColumnChanging` 事件。  但是，当要读取的 XML 文档为 `DiffGram` 时，除非将 `XmlReadMode` 设置为 `DiffGram` 或 `Auto`，否则 `ReadXml` 方法会引发 `ColumnChanged` 和 `ColumnChanging` 事件。  
  
> [!WARNING]
>  如果在从中引发 `RowChanged` 事件的 `DataSet` 中修改数据，则会发生数据损坏。  出现这类数据损坏并不会引发任何异常。  
  
## 其他相关事件  
 <xref:System.Data.DataTable.Constraints%2A> 属性包含 <xref:System.Data.ConstraintCollection> 实例。  <xref:System.Data.ConstraintCollection> 类会公开 <xref:System.Data.ConstraintCollection.CollectionChanged> 事件。  在 `ConstraintCollection` 中添加、修改约束，或从中删除约束时，会激发此事件。  
  
 <xref:System.Data.DataTable.Columns%2A> 属性包含 <xref:System.Data.DataColumnCollection> 实例。  `DataColumnCollection` 类会公开 <xref:System.Data.DataColumnCollection.CollectionChanged> 事件。  在 `DataColumnCollection` 中添加、修改或从中删除 `DataColumn` 时，会激发此事件。  导致激发此事件的修改包括更改列的名称、类型、表达式或序号位置。  
  
 <xref:System.Data.DataSet> 的 <xref:System.Data.DataSet.Tables%2A> 属性包含 <xref:System.Data.DataTableCollection> 实例。  `DataTableCollection` 类会公开 `CollectionChanged` 和 `CollectionChanging` 事件。  向 `DataSet` 中添加或从中删除 `DataTable` 时，会激发这两个事件。  
  
 更改 `DataRows` 还会触发已关联 <xref:System.Data.DataView> 的事件。  `DataView` 类会公开 <xref:System.Data.DataView.ListChanged> 事件，当 `DataColumn` 值发生更改或视图的撰写或排序顺序发生更改时会激发此事件。  <xref:System.Data.DataRowView> 类会公开 <xref:System.Data.DataRowView.PropertyChanged> 事件，当关联的 `DataColumn` 值发生更改时会激发此事件。  
  
## 操作顺序  
 下面是添加、修改或删除 `DataRow` 时所执行操作的顺序：  
  
1.  创建建议的记录并应用任何更改。  
  
2.  检查非表达式列的约束。  
  
3.  如适用，引发 `RowChanging` 或 `RowDeleting` 事件。  
  
4.  将建议的记录设置为当前记录。  
  
5.  更新任何关联的索引。  
  
6.  为关联的 `DataView` 对象引发 `ListChanged` 事件；为关联的 `DataRowView` 对象引发 `PropertyChanged` 事件。  
  
7.  计算所有表达式列，但延迟检查对这些列的任何约束。  
  
8.  为关联的 `DataView` 对象引发 `ListChanged` 事件；为受表达式列计算影响的 `DataRowView` 对象引发 `PropertyChanged` 事件。  
  
9. 如适用，引发 `RowChanged` 或 `RowDeleted` 事件。  
  
10. 检查对表达式列的约束。  
  
> [!NOTE]
>  更改表达式列绝不会引发 `DataTable` 事件。  更改表达式列只会引发 `DataView` 和 `DataRowView` 事件。  表达式列可与多个其他列存在相关性，并且在单个 `DataRow` 操作期间可计算多次。  每个表达式计算都可引发事件，并且当表达式列受影响时，单个 `DataRow` 操作可引发多个 `ListChanged` 和 `PropertyChanged` 事件，其中可能包括同一表达式列的多个事件。  
  
> [!WARNING]
>  请勿在 `RowChanged` 事件处理程序中引发 <xref:System.NullReferenceException>。  如果在 `DataTable` 的 `RowChanged` 事件中引发了 <xref:System.NullReferenceException>，`DataTable` 将被损坏。  
  
### 示例  
 下面的示例演示如何为 `RowChanged`、`RowChanging`、`RowDeleted`、`RowDeleting`、`ColumnChanged`、`ColumnChanging`、`TableNewRow`、`TableCleared` 和 `TableClearing` 事件创建事件处理程序。  在激发每个事件处理程序时，都会在控制台窗口中显示相关输出。  
  
 [!code-csharp[DataWorks DataTable.Events#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.Events/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.Events#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.Events/VB/source.vb#1)]  
  
## 请参阅  
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [处理 DataAdapter 事件](../../../../../docs/framework/data/adonet/handling-dataadapter-events.md)   
 [处理数据集事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataset-events.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)