---
title: "查询类型化数据集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad712fa1-2baf-462a-b163-574cce6d376a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 查询类型化数据集
如果在应用程序设计时已知 <xref:System.Data.DataSet> 的架构，则建议在使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 时使用类型化 <xref:System.Data.DataSet>。  类型化 <xref:System.Data.DataSet> 是从 <xref:System.Data.DataSet> 中派生的类。  因此，它继承 <xref:System.Data.DataSet> 的所有方法、事件和属性。  此外，类型化 <xref:System.Data.DataSet> 还提供强类型方法、事件和属性。  这意味着可以按名称而不使用基于集合的方法来访问表和列。  这可使查询更简单、更具可读性。  有关详细信息，请参阅[类型化数据集](../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)。  
  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 还支持对类型化 <xref:System.Data.DataSet> 进行查询。  对于类型化 <xref:System.Data.DataSet>，您不必使用泛型 <xref:System.Data.DataRowExtensions.Field%2A> 方法或 <xref:System.Data.DataRowExtensions.SetField%2A> 方法即可访问列数据。  由于 <xref:System.Data.DataSet> 中包括类型信息，因此属性名称在编译时可用。[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 提供对正确类型的列值的访问，以便可以在编译代码时而不是在运行时捕获类型不匹配错误。  
  
 在可以开始查询类型化 <xref:System.Data.DataSet> 之前，必须先通过使用 [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] 中的数据集设计器生成该类。  有关详细信息，请参阅[如何：创建类型化数据集](../Topic/Create%20and%20configure%20datasets%20in%20Visual%20Studio.md)。  
  
## 示例  
 下面的示例演示对类型化 <xref:System.Data.DataSet> 进行查询：  
  
```csharp  
var query = from o in orders  
            where o.OnlineOrderFlag == true  
            select new { o.SalesOrderID,  
                         o.OrderDate,  
                         o.SalesOrderNumber };  
  
foreach(var order in query)   
{  
    Console.WriteLine("{0}\t{1:d}\t{2}",   
order.SalesOrderID,   
order.OrderDate,   
order.SalesOrderNumber);  
}  
```  
  
```vb  
Dim orders = ds.Tables("SalesOrderHeader")  
  
Dim query = _  
       From o In orders _  
       Where o.OnlineOrderFlag = True _  
       Select New {SalesOrderID := o.SalesOrderID, _  
                   OrderDate := o.OrderDate, _  
                   SalesOrderNumber := o.SalesOrderNumber}  
  
For Each Dim onlineOrder In query  
 Console.WriteLine("{0}\t{1:d}\t{2}", _  
 onlineOrder.SalesOrderID, _  
 onlineOrder.OrderDate, _  
 onlineOrder.SalesOrderNumber)  
Next  
```  
  
## 请参阅  
 [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [交叉表查询](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)   
 [单表查询](../../../../docs/framework/data/adonet/single-table-queries-linq-to-dataset.md)