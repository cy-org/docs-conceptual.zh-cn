---
title: "类型化数据集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 033d2548-cf24-4c05-8179-67d8b009c048
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 类型化数据集
在允许通过弱类型化变量对值进行后期绑定访问的同时，<xref:System.Data.DataSet> 还允许通过强类型化比喻对数据进行访问。  使用用户友好名称和强类型化变量，可以访问作为 **DataSet** 一部分的表和列。  
  
 类型化的 **DataSet** 是从 **DataSet** 派生的类。  同样，它继承 **DataSet** 的所有方法、事件和属性。  此外，类型化的 **DataSet** 提供强类型化的方法、事件和属性。  这意味着可以按名称（而不是使用基于集合的方法）访问表和列。  除了提高代码的可读性之外，类型化的 **DataSet** 还允许 Visual Studio .NET 代码编辑器自动填写您键入的行。  
  
 此外，强类型化的 **DataSet** 还允许在编译时以正确的类型访问值。  通过强类型化的 **DataSet**，将在编译代码时（而不是在运行时）捕获类型不匹配错误。  
  
## 本节内容  
 [生成强类型数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-strongly-typed-datasets.md)  
 描述如何创建和使用强类型化的 **DataSet**。  
  
 [批注类型化数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/annotating-typed-datasets.md)  
 描述如何批注 XML 架构定义语言 \(XSD\) 架构（该架构用于生成强类型化的 **DataSet**），以便在不更改基础架构的情况下提供 **DataSet** 元素友好的名称。  
  
## 请参阅  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)