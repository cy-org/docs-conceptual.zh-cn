---
title: "在 SQL Server 中为存储过程签名 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 在 SQL Server 中为存储过程签名
您可以使用证书或非对称密钥为存储过程签名。  此设计适用于无法通过所属权链继承权限或所属权链中断的方案，如动态 SQL。  然后您可以创建一个映射到该证书的用户，对存储过程需要访问的对象授予证书用户权限。  
  
 在执行存储过程时，SQL Server 会将证书用户的权限与调用方的权限组合在一起。  与 EXECUTE AS 子句不同，它不更改过程的执行上下文。  返回登录名和用户名的内置函数会返回调用方的名称，而不是证书用户的名称。  
  
 数字签名是用签名人的私钥加密的数据摘要。  该私钥可确保数字签名对于其持有者或所有者是唯一的。  您可以为存储过程、函数或触发器签名。  
  
> [!NOTE]
>  您可以在 master 数据库中创建证书以便授予服务器级权限。  
  
## 创建证书  
 当使用证书为存储过程签名时，会使用私钥创建由该存储过程代码的加密哈希组成的数据摘要。  在运行时，数据摘要将使用公钥解密并与存储过程的哈希值进行比较。  修改存储过程会使哈希值无效，使数字签名不再匹配。  这可防止无权访问私钥的人更改存储过程代码。  因此，每次修改过程时都必须重新为过程签名。  
  
 为模块签名涉及以下四个步骤：  
  
1.  使用 Transact\-SQL `CREATE CERTIFICATE [certificateName]` 语句创建一个证书。  此语句具有多个用于设置开始日期、结束日期和密码的选项。  默认的到期日期为一年  
  
2.  使用 Transact\-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]` 语句创建与该证书关联的数据库用户。  此用户仅存在于数据库中，不与登录名关联。  
  
3.  向证书用户授予访问数据库对象所需的权限。  
  
> [!NOTE]
>  证书不能向用户授予已经使用 DENY 语句撤消的权限。  DENY 始终优先于 GRANT，以防止调用方继承授予给证书用户的权限。  
  
1.  使用 Transact\-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` 语句通过证书为过程签名。  
  
## 外部资源  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|SQL Server 联机丛书中的[模块签名](http://go.microsoft.com/fwlink/?LinkId=98590)（可能为英文网页）|说明模块签名，提供示例方案和到相关 Transact\-SQL 主题的链接。|  
|SQL Server 联机丛书中的[使用证书为存储过程签名](http://msdn.microsoft.com/library/bb283630.aspx)（可能为英文网页）|提供有关使用证书为存储过程签名的教程。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [使用 SQL Server 中的存储过程管理权限](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)   
 [在 SQL Server 中编写安全动态 SQL](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)   
 [在 SQL Server 中使用模拟来自定义权限](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)   
 [使用存储过程修改数据](../../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)