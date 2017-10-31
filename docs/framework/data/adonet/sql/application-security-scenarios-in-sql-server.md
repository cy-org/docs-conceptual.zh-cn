---
title: "SQL Server 中的应用程序安全机制方案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server 中的应用程序安全机制方案
没有用于创建安全 SQL Server 客户端应用程序的一种通用的正确方法。  每个应用程序在其要求、部署环境和用户群方面都是不同的。  最初部署时相当安全的应用程序随着时间的推移可能会变得不太安全。  无法准确预测未来可能出现的威胁。  
  
 作为一种产品，SQL Server 已演变了多种版本，以合并有助于开发人员创建安全的数据库应用程序的最新安全功能。  但是，安全性并非一成不变；它需要不断监视和更新。  
  
## 常见威胁  
 开发人员需要了解安全威胁、针对安全威胁所提供的工具，以及如何避免自己造成的安全漏洞。  最好可将安全性视为一个链，其中任何一个环节中出现中断就会损害整个链的牢固性。  以下列表中包括了一些常见安全威胁，在本节的主题中对这些安全威胁进行了详细讨论。  
  
### SQL 注入  
 SQL 注入是恶意用户输入 Transact\-SQL 语句来取代有效输入的过程。  如果未经验证而将输入直接传递到服务器，且应用程序无意中执行了该注入的代码，则攻击可能就会损坏或破坏数据。  可以通过以下方式来阻止 SQL Server 注入攻击：使用存储过程和参数化的命令，避免动态 SQL，并限制所有用户的权限。  
  
### 特权提升  
 当用户能够具有某个可信帐户的特权（如所有者或管理员）时，就会发生特权提升攻击。  始终以最小特权的用户帐户运行，并仅分配所需的权限。  避免使用管理员帐户或所有者帐户来执行代码。  这样就会降低因攻击成功而导致的损坏程度。  当执行需要额外权限的任务时，仅在该任务的持续时间内使用过程签名或模拟。  可以使用证书为存储过程签名，或使用模拟来临时分配权限。  
  
### 探测和智能观测  
 探测攻击可使用由应用程序生成的错误消息来搜索安全漏洞。  在所有程序代码中实现错误处理可阻止 SQL Server 错误信息返回到最终用户。  
  
### 身份验证  
 如果在运行时构造了基于用户输入的连接字符串，则当使用 SQL Server 登录名时，就会发生连接字符串注入攻击。  如果未检查该连接字符串中是否存在有效的关键字对，则攻击者可插入额外字符，进而可能访问服务器上的敏感数据或其他资源。  尽量使用 Windows 身份验证。  如果必须使用 SQL Server 登录名，请在运行时使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 创建和验证连接字符串。  
  
### 密码  
 许多攻击成功的原因在于，入侵者能够获取或推测特权用户的密码。  密码是阻止入侵者的第一道防线，因此设置强密码对于保护您的系统安全非常重要。  为混合模式身份验证创建和实施密码策略。  
  
 始终为 `sa` 帐户分配强密码，即使在使用 Windows 身份验证时也是如此。  
  
## 本节内容  
 [使用 SQL Server 中的存储过程管理权限](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)  
 描述如何使用存储过程来管理权限和控制数据访问。  使用存储过程是应对许多安全威胁的一种有效方法。  
  
 [在 SQL Server 中编写安全动态 SQL](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)  
 描述用于使用存储过程编写安全的动态 SQL 的技术。  
  
 [在 SQL Server 中为存储过程签名](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)  
 描述如何使用证书为存储过程签名，以使用户可以使用其无直接访问权限的数据。  这就使存储过程可执行调用方无直接执行权限的操作。  
  
 [在 SQL Server 中使用模拟来自定义权限](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)  
 描述如何使用 EXECUTE AS 子句来模拟另一用户。  模拟将执行上下文从调用方切换到指定用户。  
  
 [在 SQL Server 中授予行级权限](../../../../../docs/framework/data/adonet/sql/granting-row-level-permissions-in-sql-server.md)  
 描述如何实现行级权限以限制数据访问。  
  
 [在 SQL Server 中创建应用程序角色](../../../../../docs/framework/data/adonet/sql/creating-application-roles-in-sql-server.md)  
 描述应用程序角色的功能。  
  
 [启用 SQL Server 中的跨数据库访问](../../../../../docs/framework/data/adonet/sql/enabling-cross-database-access-in-sql-server.md)  
 描述如何在不损害安全性的情况启用跨数据库访问。  
  
## 请参阅  
 [SQL Server 安全性](../../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)