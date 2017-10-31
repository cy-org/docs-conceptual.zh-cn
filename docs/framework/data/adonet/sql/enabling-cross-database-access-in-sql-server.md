---
title: "启用 SQL Server 中的跨数据库访问 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10663fb6-434c-4c81-8178-ec894b9cf895
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 启用 SQL Server 中的跨数据库访问
当某个数据库中的某一过程依赖另一个数据库中的对象时，会发生跨数据库所有权链接。  跨数据库所有权链与单个数据库中的所有权链接的工作方式相同，不同之处在于完整的所有权链要求将所有对象拥有者映射为同一登录帐户。  如果同一登录帐户拥有源数据库中的源对象和目标数据库中的目标对象，则 SQL Server 不会检查对目标对象的权限。  
  
## 默认情况下为关  
 默认情况下，跨数据库的所有权链接已关闭。  Microsoft 建议禁用跨数据库所有权链接，因为它会使您面临以下安全风险：  
  
-   数据库所有者和 `db_ddladmin` 成员或 `db_owners` 数据库角色可创建其他用户所拥有的对象。  这些对象的目标可能是其他数据库中的对象。  这表示如果启用跨数据库所有权链接，您必须完全信任在所有数据库中具有数据的这些用户。  
  
-   具有 CREATE DATABASE 权限的用户可创建新数据库以及附加现有数据库。  如果启用了跨数据库所有权链接，则这些用户可以从新创建的或他们创建的附加数据库中访问他们在其中没有权限的其他数据库中的对象。  
  
## 启用跨数据库所有权链接  
 只能在完全信任高级权限用户的环境中启用跨数据库所有权链接。  可以在设置过程中针对所有数据库来配置所有权链接，或者使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 命令 `sp_configure` 和 `ALTER DATABASE`，有选择地针对特定数据库配置所有权链接。  
  
 若要有选择地配置跨数据库所有权链接，请使用 `sp_configure` 将服务器的所有权链接关闭。  然后，使用包含 SET DB\_CHAINING ON 的 ALTER DATABASE 命令仅为需要跨数据库所有权链接的数据库配置跨数据库所有权链接。  
  
 下面的示例针对所有数据库启用跨数据库所有权链接：  
  
```  
EXECUTE sp_configure 'show advanced', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'cross db ownership chaining', 1;  
RECONFIGURE;  
```  
  
 下面的示例针对特定数据库启用跨数据库所有权链接：  
  
```  
ALTER DATABASE Database1 SET DB_CHAINING ON;  
ALTER DATABASE Database2 SET DB_CHAINING ON;  
  
```  
  
### 动态 SQL  
 在执行了动态创建的 SQL 语句的情况下跨数据库所有权链接将不起作用，除非同一用户同时存在于两个数据库中。  在 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中，您可以通过创建一个可访问另一个数据库中数据的存储过程并使用两个数据库中都存在的证书为此过程签名来解决此问题。  这可为用户提供访问该过程所使用的数据库资源的权限，而不必向他们授予数据库访问权或权限。  
  
## 外部资源  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[通过使用 EXECUTE AS 来扩展数据库模拟](http://msdn.microsoft.com/library/ms188304\(SQL.105\).aspx)和[跨数据库所有权链接选项](http://msdn.microsoft.com/library/ms188694.aspx)[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]联机丛书。|这些主题描述了如何为 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 的实例配置跨数据库所有权链接。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [使用 SQL Server 中的存储过程管理权限](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)   
 [在 SQL Server 中编写安全动态 SQL](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)   
 [在 SQL Server 中为存储过程签名](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)