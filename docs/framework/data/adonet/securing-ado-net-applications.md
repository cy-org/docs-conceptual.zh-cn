---
title: "保证 ADO.NET 应用程序的安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 005a1d43-6ee5-471e-ad98-1d30a44d49d5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 保证 ADO.NET 应用程序的安全
编写安全 ADO.NET 应用程序不仅仅是避免常见的编码缺陷（如不验证用户输入）。  访问数据的应用程序具有许多潜在的故障点，攻击者可以利用这些故障点来检索、操作或损坏敏感数据。  因此，了解安全性的各个方面（从应用程序设计阶段期间的威胁建模过程到应用程序的最终部署和不断的维护）非常重要。  
  
 .NET Framework 提供了很多有用的类、服务和工具，以用于保证数据库应用程序的安全和对其进行管理。  公共语言运行库 \(CLR\) 提供了供代码在其中运行的类型安全环境，以及用于进一步限制托管代码权限的代码访问安全性 \(CAS\)。  遵循安全数据访问编码惯例可降低由潜在攻击者造成的损坏。  
  
 编写安全代码不会阻止在使用非托管资源（如数据库）时自己造成的安全漏洞。  多数服务器数据库（如 SQL Server）拥有其各自的安全系统，正确实现这些安全系统可增强安全性。  但是，即使是具有可靠安全系统的数据源，如果未适当配置，也可能受到攻击。  
  
## 本节内容  
 [安全性概述](../../../../docs/framework/data/adonet/security-overview.md)  
 提供对设计安全 ADO.NET 应用程序的建议。  
  
 [安全数据访问](../../../../docs/framework/data/adonet/secure-data-access.md)  
 描述如何使用受保护数据源中的数据。  
  
 [安全客户端应用程序](../../../../docs/framework/data/adonet/secure-client-applications.md)  
 描述客户端应用程序的安全注意事项。  
  
 [代码访问安全性和 ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)  
 描述 CAS 如何帮助保护 ADO.NET 代码，  还讨论如何使用部分信任。  
  
 [隐私和数据安全](../../../../docs/framework/data/adonet/privacy-and-data-security.md)  
 描述 ADO.NET 应用程序的加密选项。  
  
## 相关章节  
 [SQL Server 安全性](../../../../docs/framework/data/adonet/sql/sql-server-security.md)  
 描述从开发人员角度来讲的 SQL Server 安全功能。  
  
 [安全注意事项](../../../../docs/framework/data/adonet/ef/security-considerations.md)  
 描述实体框架应用程序的安全性。  
  
 [安全性](../../../../docs/standard/security/index.md)  
 包含描述 .NET Framework 中各个安全方面的主题的链接。  
  
 [Security Tools](http://msdn.microsoft.com/zh-cn/2a3eb98a-2de6-4fba-b41c-01a74d354c11)  
 用于保证安全策略的安全和对其进行管理的 .NET Framework 工具。  
  
 [Resources for Creating Secure Applications](http://msdn.microsoft.com/zh-cn/0ebf5f69-76f2-498a-a2df-83cf3443e132)  
 提供用于创建安全应用程序的主题的链接。  
  
 [安全参考书目](../Topic/Security%20Bibliography.md)  
 提供联机和印刷资料中提供的外部资源的链接。  
  
## 请参阅  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)