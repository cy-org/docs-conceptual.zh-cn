---
title: "SQL Server 中的 CLR 集成安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 489fe096-fd1d-42de-8438-bf7aed46aea2
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server 中的 CLR 集成安全性
Microsoft SQL Server 提供 .NET Framework 的公共语言运行时 \(CLR\) 组件集成。  通过 CLR 集成，您可以使用任何 .NET Framework 语言（如 Microsoft Visual Basic .NET 或 Microsoft Visual C\#）编写存储过程、触发器、用户定义的类型、用户定义的函数、用户定义的聚合以及流式表值函数。  
  
 CLR 支持一种用于托管代码的安全模型，称为代码访问安全性 \(CAS\)。  在此模型中，将根据元数据中代码提供的证据向程序集授予权限。  SQL Server 将 SQL Server 的基于用户的安全模型与 CLR 的基于代码启用的安全模型相集成。  
  
## 外部资源  
 有关 CLR 与 SQL Server 集成的更多信息，请参见下列资源。  
  
|资源|描述|  
|--------|--------|  
|[Code Access Security](http://msdn.microsoft.com/zh-cn/23a20143-241d-4fe5-9d9f-3933fd594c03)|包含描述 .NET Framework 中 CAS 的主题。|  
|[CLR 集成安全性](http://go.microsoft.com/fwlink/?LinkId=59998)（可能为英文网页）|讨论在 SQL Server 内部执行的托管代码的安全模型。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [SQL Server 公共语言运行库集成](../../../../../docs/framework/data/adonet/sql/sql-server-common-language-runtime-integration.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)