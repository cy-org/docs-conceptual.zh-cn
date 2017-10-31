---
title: "SQL Server 中的所有权和用户架构分离 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 242830c1-31b5-4427-828c-cc22ff339f30
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 中的所有权和用户架构分离
SQL Server 安全性的核心概念是对象的所有者具有管理这些对象的不可撤消的权限。  您不能取消对象所有者的特权，并且如果用户在数据库中拥有对象，您也不能将用户从数据库中删除。  
  
## 用户架构分离  
 通过用户架构分离，可实现管理数据库对象权限的更大灵活性。  “架构”是一个命名的数据库对象容器，它允许您将对象分组为单独的命名空间。  例如，AdventureWorks 示例数据库包含 Production、Sales 和 HumanResources 的架构。  
  
 用于引用对象的由四部分组成的命名语法指定架构名称。  
  
```  
Server.Database.DatabaseSchema.DatabaseObject  
```  
  
### 架构所有者和权限  
 任何数据库主体都可以拥有架构，并且一个主体可拥有多个架构。  您可以对架构应用安全规则，安全规则将由架构中的所有对象继承。  如果设置了对架构的访问权限，则当新对象添加到架构时，新对象会自动应用这些权限。  可以为用户分配一个默认的架构，且多个数据库用户可以共享同一架构。  
  
 默认情况下，当开发人员在架构中创建对象时，该对象由拥有架构的安全主体而不是开发人员拥有。  可以使用 ALTER AUTHORIZATION Transact\-SQL 语句转移对象所有权。  虽因架构会增大管理权限的复杂度而不建议使用，但架构仍然可以包含由不同用户拥有的对象并可具有比分配给架构的权限更加细化的权限。  对象可以在架构之间移动，架构所有权也可以在主体之间转移。  可以在不影响架构的情况下删除数据库用户。  
  
### 内置架构  
 SQL Server 随附了十个预定义的架构，它们与内置数据库用户和角色具有相同的名称。  这些架构主要用于向后兼容性。  如果您不需要与固定数据库角色具有相同名称的架构，则可以删除它们。  您不能删除下列架构：  
  
-   `dbo`  
  
-   `guest`  
  
-   `sys`  
  
-   `INFORMATION_SCHEMA`  
  
 如果从模型数据库中删除这些架构，它们将不会显示在新数据库中。  
  
> [!NOTE]
>  `sys` 和 `INFORMATION_SCHEMA` 架构是为系统对象而保留的。  您不能在这些架构中创建对象，而且不能删除它们。  
  
#### dbo 架构  
 `dbo` 是新创建的数据库的默认架构。  `dbo` 架构由 `dbo` 用户帐户拥有。  默认情况下，使用 CREATE USER Transact\-SQL 命令创建的用户的默认架构为 `dbo`。  
  
 分配了 `dbo` 架构的用户不继承 `dbo` 用户帐户的权限。  用户不从架构继承权限；架构权限由架构中包含的数据库对象继承。  
  
> [!NOTE]
>  当使用部分名称来引用数据库对象时，SQL Server 首先在用户的默认架构中查找。  如果在此处未找到该对象，则 SQL Server 其次将在 `dbo` 架构中查找。  如果对象不在 `dbo` 架构中，则会返回一个错误。  
  
## 外部资源  
 有关对象所有权和架构的更多信息，请参见下列资源。  
  
|资源|描述|  
|--------|--------|  
|SQL Server 联机丛书中的[用户架构分离](http://msdn.microsoft.com/library/ms190387.aspx)（可能为英文网页）|描述用户架构分离引发的变化，  包括新行为及其对所有权、目录视图和权限的影响。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [SQL Server 中的身份验证](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)   
 [SQL Server 中的服务器和数据库角色](../../../../../docs/framework/data/adonet/sql/server-and-database-roles-in-sql-server.md)   
 [SQL Server 中的授权和权限](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)