---
title: "使用命令修改数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 使用命令修改数据
使用 .NET Framework 数据提供程序，您可以执行存储过程或数据定义语言语句（如 CREATE TABLE 和 ALTER COLUMN）来对数据库或编录执行架构处理。  这些命令不会像查询一样返回行，因此 **Command** 对象提供了 **ExecuteNonQuery** 来处理这些命令。  
  
 除了使用 **ExecuteNonQuery** 来修改架构之外，还可以使用此方法处理那些修改数据但不返回行的 SQL 语句，如 INSERT、UPDATE 和 DELETE。  
  
 虽然行不是由 **ExecuteNonQuery** 方法返回的，但可以通过 **Command** 对象的 **Parameters** 集合来传递和返回输入和输出参数以及返回值。  
  
## 本节内容  
 [更新数据源中的数据](../../../../docs/framework/data/adonet/updating-data-in-a-data-source.md)  
 描述如何执行对数据库中的数据进行修改的命令或存储过程。  
  
 [执行编录操作](../../../../docs/framework/data/adonet/performing-catalog-operations.md)  
 描述如何执行对数据库架构进行修改的命令。  
  
## 请参阅  
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)