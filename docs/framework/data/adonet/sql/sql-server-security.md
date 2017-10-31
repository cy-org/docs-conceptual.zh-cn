---
title: "SQL Server 安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server 安全性
[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 具有许多支持创建安全数据库应用程序的功能。  
  
 无论您要使用哪个版本的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]，通用安全注意事项（如数据盗窃和蓄意破坏）都适用。  数据完整性也应视为安全问题。  如果数据不加保护，则在允许对数据执行临时操作并且数据被有意或无意修改（添加错误的值或完全删除）的情况下，数据可能会变得毫无价值。  此外，通常还有一些必须遵守的法定要求，如正确存储机密信息。  完全禁止存储某些类型的个人数据，具体取决于特定司法范围内适用的法律。  
  
 与每个版本的 Windows 一样，每个版本的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 都具有不同的安全功能，版本越高，功能越强。  必须了解的是，安全功能本身不能保证数据库应用程序的安全。  每个数据库应用程序都具有独特的要求、执行环境、部署模型、物理位置和用户人群。  范围限于本地的一些应用程序可能只需要最低的安全性，而其他本地应用程序或通过 Internet 部署的应用程序可能需要严格的安全措施和实时监控和评估。  
  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 数据库应用程序的安全要求应该在设计时就加以考虑，而不应事后再考虑。  在开发周期的初期评估危胁可以减轻检测到漏洞时造成的潜在损害。  
  
 即使应用程序的初始设计非常可靠，但随着系统的发展，仍可能会出现新的危胁。  通过在数据库周围构建多道防线，可以最大程度地减轻安全侵犯事件所造成的损害。  第一道防线是通过仅授予完全必要的权限而不授予更多权限来减小攻击面。  
  
 本节中的主题简要说明了 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中开发人员相关的安全功能，并提供了到 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书中的相关主题以及提供更详细说明的其他资源的链接。  
  
## 本节内容  
 [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)  
 说明了 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 的体系结构和安全功能。  
  
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)  
 包含对 ADO.NET 和 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 应用程序的各种应用程序安全方案进行讨论的主题。  
  
 [SQL Server Express 安全性](../../../../../docs/framework/data/adonet/sql/sql-server-express-security.md)  
 说明了 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] Express 的安全注意事项。  
  
## 相关章节  
 [安全性和保护（数据库引擎）](http://msdn2.microsoft.com/library/bb510589\(SQL.100\).aspx)。  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书安全性主题。  
  
 [SQL Server 的安全注意事项](http://go.microsoft.com/fwlink/?LinkId=98587)（可能为英文网页）  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书安全性主题。  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)