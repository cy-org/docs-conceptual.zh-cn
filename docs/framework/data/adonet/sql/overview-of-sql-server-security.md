---
title: "SQL Server 安全性概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae66dd75-5c16-4cc0-9e12-774dd26d3fb9
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server 安全性概述
具有重叠安全层的全面防御策略是抵御安全威胁的最佳方式。  SQL Server 提供的安全体系结构旨在允许数据库管理员和开发人员创建安全的数据库应用程序并抵御威胁。  通过引入新功能，SQL Server 的每个版本都在先前的 SQL Server 版本基础上得到改善。  但是，安全性并不是现成的。  每个应用程序都具有其独特的安全要求。  开发人员需要了解哪些功能组合最适合抵御已知的威胁，并需要预见未来可能出现的威胁。  
  
 SQL Server 实例包含以服务器为首的实体的分层集合。  每个服务器均包含多个数据库，而每个数据库均包含可保护对象的集合。  每个 SQL Server 可保护对象均具有可授予主体（个人、组或授予访问 SQL Server 权限的进程）的关联权限。  SQL Server 安全框架通过身份验证和授权来管理对可保护实体的访问。  
  
-   身份验证是指通过提交服务器评估的凭据以登录到主体请求访问的 SQL Server 的过程。  身份验证可以确定接受身份验证的用户或进程的标识。  
  
-   授权是指确定主体可以访问哪些可保护资源以及允许对这些资源执行哪些操作的过程。  
  
 本节中的主题介绍 SQL Server 安全基础知识，并提供到相关版本 SQL Server 联机丛书中完整文档的链接。  
  
## 本节内容  
 [SQL Server 中的身份验证](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)  
 说明 SQL Server 中的登录名和身份验证并提供到其他资源的链接。  
  
 [SQL Server 中的服务器和数据库角色](../../../../../docs/framework/data/adonet/sql/server-and-database-roles-in-sql-server.md)  
 说明固定服务器和数据库角色、自定义数据库角色和内置帐户，并提供到其他资源的链接。  
  
 [SQL Server 中的所有权和用户架构分离](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)  
 说明对象所属权和用户架构分离，并提供到其他资源的链接。  
  
 [SQL Server 中的授权和权限](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)  
 说明使用最低特权原则授予权限并提供到其他资源的链接。  
  
 [SQL Server 中的数据加密](../../../../../docs/framework/data/adonet/sql/data-encryption-in-sql-server.md)  
 说明 SQL Server 中的数据加密选项并提供到其他资源的链接。  
  
 [SQL Server 中的 CLR 集成安全性](../../../../../docs/framework/data/adonet/sql/clr-integration-security-in-sql-server.md)  
 提供到 CLR 集成安全资源的链接。  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 安全性](../../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)