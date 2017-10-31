---
title: "SQL Server 中的数据加密 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83b992f7-b351-4678-b4b9-f4ffd58134cc
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 中的数据加密
SQL Server 提供了使用证书、非对称密钥或对称密钥对数据进行加密和解密的功能。  它在一个内部证书存储中管理所有这些证书或密钥。  该存储使用加密层次结构，可在层次结构中的上一层级别保护证书和密钥。  SQL Server 的此功能区域称为“机密存储”。  
  
 加密功能支持的最快加密模式是对称密钥加密。  此模式适用于处理大量数据。  可以通过证书、密码或其他对称密钥加密对称密钥。  
  
## 密钥和算法  
 SQL Server 支持多种对称密钥加密算法，包括 DES、Triple DES、RC2、RC4、128 位 RC4、DESX、128 位 AES、192 位 AES 和 256 位 AES。  这些算法使用 Windows 加密 API 实现。  
  
 在数据库连接范围内，SQL Server 可以保留多个开放式对称密钥。  开放式密钥从存储中进行检索，并可用于解密数据。  解密一段数据时，不需要指定要使用的对称密钥。  每个加密的值均包含用于加密该值的密钥的密钥标识符（密钥 GUID）。  如果已解密正确的密钥并且该密钥已开放，则引擎会将加密的字节流匹配到开放式对称密钥。  然后使用此密钥执行解密并返回数据。  如果正确的密钥未开放，则返回 NULL。  
  
 有关显示如何处理数据库中的加密数据的示例，请参见 SQL Server 联机丛书中的[如何：加密数据列](http://go.microsoft.com/fwlink/?LinkID=128559)（可能为英文网页）。  
  
## 外部资源  
 有关数据加密的更多信息，请参见以下资源。  
  
|||  
|-|-|  
|SQL Server 联机丛书中的 [SQL Server 加密](http://msdn.microsoft.com/library/bb510663.aspx)（可能为英文网页）|概述了 SQL Server 中的加密。  此主题包括到其他主题和帮助主题的链接。|  
|SQL Server 联机丛书中的[加密层次结构](http://msdn.microsoft.com/library/ms189586.aspx)（可能为英文网页）和[加密帮助主题](http://msdn.microsoft.com/library/aa337557.aspx)（可能为英文网页）|概述了 SQL Server 中的加密。  此主题提供到其他主题和帮助主题的链接。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [SQL Server 中的身份验证](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)   
 [SQL Server 中的服务器和数据库角色](../../../../../docs/framework/data/adonet/sql/server-and-database-roles-in-sql-server.md)   
 [SQL Server 中的所有权和用户架构分离](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)   
 [SQL Server 中的授权和权限](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)