---
title: "工厂模型概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 工厂模型概述
ADO.NET 2.0 在 <xref:System.Data.Common> 命名空间中引入了新基类。  基类为抽象类，这意味着它们不能直接实例化。  这些基类包括 <xref:System.Data.Common.DbConnection>、<xref:System.Data.Common.DbCommand> 和 <xref:System.Data.Common.DbDataAdapter>，它们由 .NET Framework 数据提供程序（如 <xref:System.Data.SqlClient> 和 <xref:System.Data.OleDb>）共享。  添加基类简化了向 .NET Framework 数据提供程序添加功能的过程，不再需要创建新接口。  
  
 ADO.NET 2.0 中还引入了一些抽象基类，使开发人员能够编写不依赖于特定数据提供程序的一般数据访问代码。  
  
## 工厂设计模式  
 编写独立于提供程序的代码的编程模型基于“工厂”设计模式的使用，此模式使用单个 API 跨多个提供程序访问数据库。  此模式的命名非常恰当，因为它需单独使用专用的对象来创建其他对象，与实际的工厂非常类似。  有关工厂设计模式的详细说明，请参阅 MSDN 上的“[在 ASP.NET 2.0 和 ADO.NET 2.0 中编写泛型数据访问代码](http://go.microsoft.com/fwlink/?LinkId=55915)”（可能为英文网页）和“使用 ADO.NET 2.0 基类和工厂的泛型编码”[http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/dnvs05\/html\/vsgenerics.asp](http://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/vsgenerics.asp)（可能为英文网页）。  
  
 从 ADO.NET 2.0 开始，<xref:System.Data.Common.DbProviderFactories> 类提供 `static`（或 Visual Basic 中的 `Shared`）方法以用于创建 <xref:System.Data.Common.DbProviderFactory> 实例。  该实例随后会基于提供程序信息和运行时提供的连接字符串返回正确的强类型对象。  
  
## 请参阅  
 [获取 DbProviderFactory](../../../../docs/framework/data/adonet/obtaining-a-dbproviderfactory.md)   
 [DbConnection、DbCommand 和 DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)   
 [使用 DbDataAdapter 修改数据](../../../../docs/framework/data/adonet/modifying-data-with-a-dbdataadapter.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)