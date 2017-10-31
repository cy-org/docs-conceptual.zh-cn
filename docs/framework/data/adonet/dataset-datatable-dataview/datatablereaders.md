---
title: "DataTableReader | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97546ae2-0e42-4d26-961d-e0b244d81ded
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTableReader
<xref:System.Data.DataTableReader> 以一个或多个只读、只进结果集的形式提供 <xref:System.Data.DataTable> 或的 <xref:System.Data.DataSet> 的内容。  
  
 在使用 **DataTable** 创建 **DataTableReader** 时，生成的 **DataTableReader** 对象包含一个结果集，其中的数据与创建该结果集的 **DataTable** 相同，所有已标记为已删除的行除外。  列出现的顺序与在原始 **DataTable** 中相同。  
  
 如果 **DataTableReader** 是通过调用 <xref:System.Data.DataSet.CreateDataReader%2A> 创建，可以包含多个结果集。  结果的顺序与 **DataSet** 对象的 <xref:System.Data.DataSet.Tables%2A> 集合中的 **DataTables** 相同。  
  
## 本节内容  
 [创建 DataReader](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datareader.md)  
 讨论如何创建 **DataTableReader** 对象。  
  
 [导航数据表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/navigating-datatables.md)  
 描述如何使用 **Read** 方法浏览 **DataTableReader** 的内容。  
  
## 请参阅  
 [在 ADO.NET 中检索和修改数据](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)