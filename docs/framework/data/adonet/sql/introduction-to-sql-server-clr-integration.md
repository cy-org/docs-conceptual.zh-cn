---
title: "SQL Server CLR 集成简介 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 551d2290-ed80-49be-b377-44b32444da1c
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server CLR 集成简介
公共语言运行库 \(CLR\) 是 Microsoft .NET Framework 的核心，为所有 .NET Framework 代码提供执行环境。  在 CLR 中运行的代码称为托管代码。  CLR 提供执行程序所需的各种函数和服务，包括实时 \(JIT\) 编译、分配和管理内存、强制类型安全性、异常处理、线程管理和安全性。  
  
 通过在 Microsoft SQL Server 中托管 CLR（称为 CLR 集成），可以在托管代码中编写存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合函数。  因为托管代码在执行之前会编译为本机代码，所以，在有些方案中可以大大提高性能。  
  
 托管代码使用代码访问安全性 \(CAS\)、代码链接和应用程序域来阻止程序集执行某些操作。  SQL Server 使用 CAS 来帮助保证托管代码的安全，并避免操作系统或数据库服务器受到威胁。  
  
 本节只是为了提供足够的信息，以便开始使用 SQL Server CLR 集成编程，而并非为了提供完整的信息。  有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
-   [公共语言运行时 \(CLR\) 集成概述](http://go.microsoft.com/fwlink/?LinkId=115242)（可能为英文网页）  
  
## 启用 CLR 集成  
 默认情况下，Microsoft SQL Server 中禁用公共语言运行库 \(CLR\) 集成功能，必须启用才能使用通过 CLR 集成实现的对象。  要使用 Transact\-SQL 启用 CLR 集成，请使用如下所示的 `sp_configure` 存储过程的 `clr enabled` 选项：  
  
```  
sp_configure 'clr enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
 可以通过将 `clr enabled` 选项设置为 0 来禁用 CLR 集成。  在禁用 CLR 集成时，SQL Server 停止执行所有 CLR 例程并卸载所有应用程序域。  
  
 有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
-   [启用 CLR 集成](http://go.microsoft.com/fwlink/?LinkId=115230)（可能为英文网页）  
  
## 部署 CLR 程序集  
 在测试服务器上测试和验证 CLR 方法后，可以使用部署脚本将其分发到生产服务器。  部署脚本可以通过手动或使用 SQL Server Management Studio 生成。  有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
1.  [部署 CLR 数据库对象](http://go.microsoft.com/fwlink/?LinkId=115232)（可能为英文网页）  
  
## CLR 集成安全性  
 Microsoft SQL Server 与 Microsoft .NET Framework 公共语言运行库 \(CLR\) 相集成，这种安全模型可管理和保护 SQL Server 中运行的不同类型 CLR 和非 CLR 对象之间的访问。  这些对象可以通过 Transact\-SQL 语句或服务器中运行的其他 CLR 对象进行调用。  
  
 有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
-   [CLR 集成安全性](http://go.microsoft.com/fwlink/?LinkId=115234)（可能为英文网页）  
  
## 调试 CLR 程序集  
 Microsoft SQL Server 支持调试数据库中的 Transact\-SQL 和公共语言运行库 \(CLR\) 对象。  跨语言调试工作：用户可以从 Transact\-SQL 无缝地进入并单步执行 CLR 对象，反之亦然。  
  
 有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
-   [调试 CLR 数据库对象](http://go.microsoft.com/fwlink/?LinkId=115236)（可能为英文网页）  
  
## 请参阅  
 [Creating SQL Server 2005 Objects In Managed Code](http://msdn.microsoft.com/zh-cn/5358a825-e19b-49aa-8214-674ce5fed1da)   
 [代码访问安全性和 ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)