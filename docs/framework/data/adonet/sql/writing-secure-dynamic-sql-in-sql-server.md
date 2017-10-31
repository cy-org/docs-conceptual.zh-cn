---
title: "在 SQL Server 中编写安全动态 SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 在 SQL Server 中编写安全动态 SQL
SQL 注入是恶意用户输入 Transact\-SQL 语句来取代有效输入的过程。  如果输入的语句没有经过验证直接传递到服务器，并且应用程序不慎执行了注入的代码，这种攻击有可能损坏或毁坏数据。  
  
 任何构造 SQL 语句的过程都应该针对注入漏洞进行审核，因为 SQL Server 将执行它扪收到的所有语法上有效的查询。  技术熟练的蓄意攻击者甚至可以操作参数化数据。  如果您使用动态 SQL，请确保将命令参数化，绝不要在查询字符串中直接包括参数值。  
  
## SQL 注入攻击剖析  
 注入过程的工作原理是过早终止某一文本字符串并追加一个新命令。  因为插入的命令可能在执行之前已追加了其他字符串，攻击者可以使用注释标记“\-\-”终止注入的字符串。  执行时会忽略后续的文本。  通过使用分号 \(;\) 分隔符可以插入多个命令。  
  
 只要注入的 SQL 代码在语法上正确，就无法通过编程方式检测到这种篡改。  因此，您必须验证所有用户输入并仔细检查将在您使用的服务器上执行构造的 SQL 命令的代码。  切勿连接未经验证的用户输入。  字符串连接是脚本注入的主要入口点。  
  
 下面是几条有帮助的准则：  
  
-   切勿直接从用户输入生成 Transact\-SQL 语句，应使用存储过程来验证用户输入。  
  
-   通过测试类型、长度、格式和范围来验证用户输入。  使用 Transact\-SQL QUOTENAME\(\) 函数转义系统名称，或使用 REPLACE\(\) 函数转义字符串中的任何字符。  
  
-   在您的应用程序的每个层中实现多层验证。  
  
-   测试输入内容的大小和数据类型并实施适当的限制。  这有助于防止故意的缓冲区溢出。  
  
-   测试字符串变量的内容，并只接受预期值。  拒绝包含二进制数据、转义序列和注释字符的输入。  
  
-   如果使用 XML 文档，则在输入时对照其架构验证所有数据。  
  
-   在多层环境中，在允许数据进入受信任区域之前所有数据都应该进行验证。  
  
-   在可能据以构造文件名的字段中，不接受下列字符串：AUX、CLOCK$、COM1 到 COM8、CON、CONFIG$、LPT1 到 LPT8、NUL 以及 PRN。  
  
-   使用带有存储过程和命令的 <xref:System.Data.SqlClient.SqlParameter> 对象以提供类型检查和长度验证。  
  
-   在客户端代码中使用 <xref:System.Text.RegularExpressions.Regex> 表达式以筛选无效字符。  
  
## 动态 SQL 策略  
 在过程代码中动态执行已创建的 SQL 语句会中断所属权链，使 SQL Server 按照由动态 SQL 访问的对象检查调用方的权限。  
  
 SQL Server 提供了使用存储过程和可执行动态 SQL 的用户定义函数来授予用户对数据的访问权限的方法。  
  
-   使用带有 Transact\-SQL EXECUTE AS 子句的模拟，如[在 SQL Server 中使用模拟来自定义权限](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md) 中所述。  
  
-   使用证书对存储过程签名，如[在 SQL Server 中为存储过程签名](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)中所述。  
  
### EXECUTE AS  
 EXECUTE AS 子句用 EXECUTE AS 子句中指定的用户的权限替换调用方的权限。  嵌套的存储过程或触发器在代理用户的安全上下文下执行。  这可能会中断依赖于行级安全性或要求审核的应用程序。  某些可返回用户标识的函数会返回 EXECUTE AS 子句中指定的用户的标识，而不是原始调用方的标识。  只有在执行该过程或发出 REVERT 语句后，执行上下文才会恢复到原始调用方。  
  
### 证书签名  
 在执行使用证书进行签名的存储过程时，授予给证书用户的权限会与调用方的权限合并。  执行上下文保持不变，证书用户不模拟调用方。  为存储过程签名需要执行多个步骤才能实现。  每次修改过程时，都必须重新签名。  
  
### 跨数据库访问  
 在执行动态创建的 SQL 语句时，跨数据库的所属权链接不起作用。  在 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中，您可以通过创建一个可访问另一个数据库中数据的存储过程并使用两个数据库中都存在的证书为此过程签名来解决此问题。  这可为用户提供访问该过程所使用的数据库资源的权限，而不必向他们授予数据库访问权或权限。  
  
## 外部资源  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|SQL Server 联机丛书中的[存储过程](http://go.microsoft.com/fwlink/?LinkId=98233)（可能为英文网页）和 [SQL 注入](http://go.microsoft.com/fwlink/?LinkId=98234)（可能为英文网页）|说明如何创建存储过程和 SQL 注入工作原理的主题。|  
|MSDN 杂志中的[新的 SQL 截断攻击以及如何避免这些攻击](http://msdn.microsoft.com/msdnmag/issues/06/11/SQLSecurity/)（可能为英文网页）。|说明截断攻击如何分隔字符和字符串、SQL 注入和所进行的修改。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [使用 SQL Server 中的存储过程管理权限](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)   
 [在 SQL Server 中为存储过程签名](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)   
 [在 SQL Server 中使用模拟来自定义权限](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)