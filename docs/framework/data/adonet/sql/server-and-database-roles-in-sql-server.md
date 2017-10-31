---
title: "SQL Server 中的服务器和数据库角色 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5482dfdb-e498-4614-8652-b174829eed13
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# SQL Server 中的服务器和数据库角色
所有版本的 SQL Server 均使用基于角色的安全，它允许您为角色、用户组而不是各个用户分配权限。  固定服务器和固定数据库角色具有分配给它们的一组固定的权限。  
  
## 固定服务器角色  
 固定服务器角色具有一组固定的权限，并且适用于整个服务器范围。  它们专门用于管理 SQL Server，且不能更改分配给它们的权限。  可以在数据库中不存在用户帐户的情况下向固定服务器角色分配登录。  
  
> [!IMPORTANT]
>  `sysadmin` 固定服务器角色包含所有其他角色并且具有无限范围。  请不要将这些主体添加到此角色，除非它们是高度信任的。  `sysadmin` 角色成员对所有服务器数据库和资源有不可撤消的管理特权。  
  
 将用户添加到固定服务器角色时，请仔细选择。  例如，`bulkadmin` 角色允许用户将任意本地文件的内容插入表中，这样可能会损坏数据的完整性。  有关固定服务器角色和权限的完整列表，请参见 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书。  
  
## 固定数据库角色  
 固定数据库角色具有一组预定义的权限，这些权限旨在允许您轻松管理权限组。  `db_owner` 角色的成员可对数据库执行所有配置和维护活动。  
  
 有关 SQL Server 预定义角色的更多信息，请参阅以下资源。  
  
|资源|描述|  
|--------|--------|  
|[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书中的[服务器级角色](http://msdn.microsoft.com/library/ms188659.aspx)（可能为英文网页）和[固定服务器角色的权限](http://msdn.microsoft.com/library/ms175892.aspx)（可能为英文网页）|描述 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中的固定服务器角色以及与其关联的权限。|  
|[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书中的[数据库级角色](http://msdn.microsoft.com/library/ms189121.aspx)（可能为英文网页）和[固定数据库角色的权限](http://msdn.microsoft.com/library/ms189612.aspx)（可能为英文网页）|描述固定数据库角色及与其关联的权限|  
  
## 数据库角色和用户  
 要使用数据库对象，必须将登录映射到数据库用户帐户。  这样就可以将数据库用户添加到数据库角色，从而继承与这些角色关联的任何权限集。  可以授予所有权限。  
  
 当为应用程序设计安全性时，还必须考虑 `public` 角色、`dbo` 用户帐户和 `guest` 帐户。  
  
### 公共角色  
 `public` 角色包含在每个数据库中，包括系统数据库。  无法删除该角色，也无法向其中添加用户或从中删除用户。  授予 `public` 角色的权限由所有其他用户和角色继承，因为默认情况下，它们属于 `public` 角色。  仅为 `public` 角色授予您希望所有用户都具有的权限。  
  
### dbo 用户帐户  
 `dbo` 或数据库所有者是具有在数据库中执行所有活动的默示权限的用户帐户。  `sysadmin` 固定服务器角色的成员会自动映射到 `dbo`。  
  
> [!NOTE]
>  `dbo` 也是架构名称，如 [SQL Server 中的所有权和用户架构分离](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)中所述。  
  
 `dbo` 用户帐户经常与 `db_owner` 固定数据库角色相混淆。  `db_owner` 的作用域是一个数据库；`sysadmin` 的作用域是整个服务器。  `db_owner` 角色中的成员无法授予 `dbo` 用户特权。  
  
### guest 用户帐户  
 用户经过身份验证并允许登录 SQL Server 的实例后，用户需要访问的每个数据库中必须存在一个单独的用户帐户。  要求每个数据库中具有用户帐户会阻止用户连接到 SQL Server 的实例，并且会阻止用户访问服务器上的所有数据库。  通过允许没有数据库用户帐户的登录访问数据库，可在数据库中包含 `guest` 用户帐户时避开此要求。  
  
 在所有版本的 SQL Server 中，`guest` 帐户均为内置帐户。  默认情况下，它在新的数据库中是禁用的。  如果启用此帐户，则可以通过撤消其 CONNECT 权限（方法是执行 Transact\-SQL REVOKE CONNECT FROM GUEST 语句）来禁用此帐户。  
  
> [!IMPORTANT]
>  避免使用 `guest` 帐户；没有其自己的数据库权限的所有登录都会获取授予此帐户的数据库权限。  如果必须使用 `guest` 帐户，请为其授予最小权限。  
  
 有关 SQL Server 登录名、用户和角色的更多信息，请参阅以下资源。  
  
|资源|描述|  
|--------|--------|  
|SQL Server 联机丛书中的[标识和访问控制](http://msdn.microsoft.com/library/bb510418.aspx)（可能为英文网页）|包含指向描述主体、角色、凭据、安全对象和权限的主题的链接。|  
|[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书中的[主体](http://msdn.microsoft.com/library/ms181127.aspx)（可能为英文网页）|描述主体并包含指向描述服务器和数据库角色的主题的链接。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [SQL Server 中的身份验证](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)   
 [SQL Server 中的所有权和用户架构分离](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)   
 [SQL Server 中的授权和权限](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)