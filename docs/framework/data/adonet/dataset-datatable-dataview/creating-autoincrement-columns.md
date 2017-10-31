---
title: "创建 AutoIncrement 列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf09732a-ab54-4d98-89e2-4d0a1f28fbce
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 创建 AutoIncrement 列
要确保列值的唯一，可将列值设置为在表中添加新行时自动递增。  要创建自动递增的 <xref:System.Data.DataColumn>，可将列的 <xref:System.Data.DataColumn.AutoIncrement%2A> 属性设置为 **true**。  然后，<xref:System.Data.DataColumn> 将从 <xref:System.Data.DataColumn.AutoIncrementSeed%2A> 属性中定义的值开始，并且每添加一行，**AutoIncrement** 列的值将按列的 <xref:System.Data.DataColumn.AutoIncrementStep%2A> 属性中定义的值增加。  
  
 对于 **AutoIncrement** 列，我们建议将 **DataColumn** 的 <xref:System.Data.DataColumn.ReadOnly%2A> 属性设置为 **true**。  
  
 以下示例演示了如何创建从值 200 开始并以 3 为增量递增的列。  
  
```vb  
Dim workColumn As DataColumn = workTable.Columns.Add( _  
    "CustomerID", typeof(Int32))  
workColumn.AutoIncrement = true  
workColumn.AutoIncrementSeed = 200  
workColumn.AutoIncrementStep = 3  
  
```  
  
```csharp  
DataColumn workColumn = workTable.Columns.Add(  
    "CustomerID", typeof(Int32));  
workColumn.AutoIncrement = true;  
workColumn.AutoIncrementSeed = 200;  
workColumn.AutoIncrementStep = 3;  
```  
  
## 请参阅  
 <xref:System.Data.DataColumn>   
 [DataTable 架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)