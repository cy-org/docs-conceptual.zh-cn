---
title: "数据表约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27c9f2fd-f64d-4b4e-bbf6-1d24f47067cb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 数据表约束
为了维护数据的完整性，可以使用约束来对 <xref:System.Data.DataTable> 中的数据施加限制。  约束是应用于某列或相关各列的自动规则，它决定了某行的值以某种方式更改时的操作过程。  当 <xref:System.Data.DataSet> 的  `System.Data.DataSet.EnforceConstraints` 属性为 **true** 时，就可强制使用约束。  有关显示如何设置 `EnforceConstraints` 属性的代码示例，请参见 <xref:System.Data.DataSet.EnforceConstraints%2A> 参考主题。  
  
 ADO.NET 中有两种约束：<xref:System.Data.ForeignKeyConstraint> 和 <xref:System.Data.UniqueConstraint>。  默认情况下，通过将 <xref:System.Data.DataRelation> 添加到 **DataSet** 来创建两个或多个表之间的关系时，两种约束都会自动创建。  但是，也可以在创建关系时，通过指定 **createConstraints** \= **false** 禁用这一行为。  
  
## ForeignKeyConstraint  
 **ForeignKeyConstraint** 强制使用有关如何对相关表所做更新和删除进行传播的规则。  例如，如果更新或删除了一个表的某行中的值，并且一个或多个相关的表中也使用了同样的值，**ForeignKeyConstraint** 会决定相关表中发生的操作。  
  
 **ForeignKeyConstraint** 的 <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> 和 <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> 属性定义在用户试图删除或更新相关表中某行时采取的操作。  下表描述可用于 **ForeignKeyConstraint** 的 **DeleteRule** 和 **UpdateRule** 属性的不同设置。  
  
|规则设置|描述|  
|----------|--------|  
|**Cascade**|删除或更新相关的行。|  
|**SetNull**|将相关行中的值设置为 **DBNull**。|  
|**SetDefault**|将相关行中的值设置为默认值。|  
|**无**|对相关行不执行任何操作。  这是默认设置。|  
  
 **ForeignKeyConstraint** 可以限制并传播对相关列的更改。  根据为列的 **ForeignKeyConstraint** 设置的属性，并且如果 **DataSet** 的 **EnforceConstraints** 属性是 **true**，对父行执行某些特定操作将会导致异常。  例如，如果 **ForeignKeyConstraint** 的 **DeleteRule** 属性是 **None**，那么在父行有子行的情况下，则无法删除父行。  
  
 可以通过使用 **ForeignKeyConstraint** 构造函数创建单列间或一组列间的外键约束。  将生成的 **ForeignKeyConstraint** 对象传递给该表的 **Constraints** 属性的 **Add** 方法，该属性是一个 **ConstraintCollection**。  还可以将构造函数参数传递给 **ConstraintCollection** 的 **Add** 方法的几个重载，以创建 **ForeignKeyConstraint**。  
  
 在创建 **ForeignKeyConstraint** 时，可以将 **DeleteRule** 和 **UpdateRule** 值作为参数传递给构造函数，也可以作为属性进行设置，如以下示例所示（其中 **DeleteRule** 值设置为 **None**）。  
  
```vb  
Dim custOrderFK As ForeignKeyConstraint = New ForeignKeyConstraint("CustOrderFK", _  
  custDS.Tables("CustTable").Columns("CustomerID"), _  
  custDS.Tables("OrdersTable").Columns("CustomerID"))  
custOrderFK.DeleteRule = Rule.None    
' Cannot delete a customer value that has associated existing orders.  
custDS.Tables("OrdersTable").Constraints.Add(custOrderFK)  
  
```  
  
```csharp  
ForeignKeyConstraint custOrderFK = new ForeignKeyConstraint("CustOrderFK",  
  custDS.Tables["CustTable"].Columns["CustomerID"],   
  custDS.Tables["OrdersTable"].Columns["CustomerID"]);  
custOrderFK.DeleteRule = Rule.None;    
// Cannot delete a customer value that has associated existing orders.  
custDS.Tables["OrdersTable"].Constraints.Add(custOrderFK);  
```  
  
### AcceptRejectRule  
 可使用 **AcceptChanges** 方法接受对行的更改，或者使用 **DataSet**、**DataTable** 或 **DataRow** 的 **RejectChanges** 方法取消对行的更改。  **DataSet** 包含 **ForeignKeyConstraints** 时，调用 **AcceptChanges** 或 **RejectChanges** 方法会强制使用 **AcceptRejectRule**。  **ForeignKeyConstraint** 的 **AcceptRejectRule** 属性决定了对父行调用 **AcceptChanges** 或 **RejectChanges** 时要对子行执行的操作。  
  
 下表列出了 **AcceptRejectRule** 的可用设置。  
  
|规则设置|描述|  
|----------|--------|  
|**Cascade**|接受或拒绝对子行的更改。|  
|**无**|对子行不执行任何操作。  这是默认设置。|  
  
### 示例  
 下面的示例创建一个 <xref:System.Data.ForeignKeyConstraint>，设置它的一些属性（包括 <xref:System.Data.ForeignKeyConstraint.AcceptRejectRule%2A>），并将它添加到 <xref:System.Data.DataTable> 对象的 <xref:System.Data.ConstraintCollection>。  
  
 [!code-csharp[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/CS/source.cs#1)]
 [!code-vb[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/VB/source.vb#1)]  
  
## UniqueConstraint  
 **UniqueConstraint** 对象（可分配给 **DataTable** 中的单独一列或一组列）确保指定的某列或多个列中的所有数据对于每行都是唯一的。  通过使用 **UniqueConstraint** 构造函数，可以为一列或一组列创建唯一的约束。  将生成的 **UniqueConstraint** 对象传递给该表的 **Constraints** 属性的 **Add** 方法，该属性是一个 **ConstraintCollection**。  还可以将构造函数参数传递给 **ConstraintCollection** 的 **Add** 方法的几个重载，以创建 **UniqueConstraint**。  为一列或多列创建 **UniqueConstraint** 时，可以选择指定此列或这些列是不是主键。  
  
 还可以通过将列的 **Unique** 属性设置为 **true**，为某列创建唯一约束。  或者，通过将单列的 **Unique** 属性设置为 **false**，可移除可能存在的任何唯一约束。  如果将一列或多列定义为表的主键，会自动为一个或多个指定的列创建唯一的约束。  如果从 **DataTable** 的 **PrimaryKey** 属性中移除一列，则 **UniqueConstraint** 也被移除。  
  
 以下示例为 **DataTable** 的两列创建 **UniqueConstraint**。  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custUnique As UniqueConstraint = _  
    New UniqueConstraint(New DataColumn()   {custTable.Columns("CustomerID"), _  
    custTable.Columns("CompanyName")})  
custDS.Tables("Customers").Constraints.Add(custUnique)  
  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
UniqueConstraint custUnique = new UniqueConstraint(new DataColumn[]   
    {custTable.Columns["CustomerID"],   
    custTable.Columns["CompanyName"]});  
custDS.Tables["Customers"].Constraints.Add(custUnique);  
```  
  
## 请参阅  
 <xref:System.Data.DataRelation>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.ForeignKeyConstraint>   
 <xref:System.Data.UniqueConstraint>   
 [DataTable 架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)