---
title: "SQL Server Compact 与 LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59022359-a5a2-4c42-9a6a-5c0259c3ad17
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server Compact 与 LINQ to SQL
SQL Server Compact 是与 Visual Studio 一起安装的默认数据库。有关更多信息，请参见[PAVE OVER Using SQL Server Compact \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/13320dd1-94e5-4077-bf76-8df253695ccc)。  
  
 本主题概括了在用法、配置、功能集和 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持范围上的主要差异。  
  
## SQL Server Compact 相对于 LINQ to SQL 的特性  
 默认情况下，所有 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 版本均安装了 SQL Server Compact，因此在开发计算机上它可以与 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 一起使用。  但是部署使用 SQL Server Compact 和 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的应用程序与部署 [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] 应用程序的方式不同。  SQL Server Compact 不是 .NET Framework 的一部分，因此必须与应用程序一起打包或单独从 Microsoft 网站下载。  
  
 请注意下列特性：  
  
-   SQL Server Compact 打包为可直接对数据库文件（扩展名为 .sdf）使用的 DLL。  
  
-   SQL Server Compact 与客户端应用程序在同一进程中运行。  因此与 SQL Server Compact 通信的效率要大大高于与 [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] 通信的效率。  另一方面，SQL Server Compact 确实需要托管代码和非托管代码之间的互操作性，而这也会带来开销。  
  
-   SQL Server Compact DLL 很小。  这一特征减小了应用程序的总大小。  
  
-   [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 运行时和 SQLMetal 命令行工具支持 SQL Server Compact。  
  
-   [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 不支持 SQL Server Compact。  
  
## 功能集  
 SQL Server Compact 功能集与 [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] 的功能集相比要简单得多，具体体现在可影响 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序的以下方面：  
  
-   SQL Server Compact 不支持存储过程或视图。  
  
-   SQL Server Compact 仅支持部分数据类型和 SQL 函数。  
  
-   SQL Server Compact 仅支持部分 SQL 构造。  
  
-   SQL Server Compact 仅提供具有最基本功能的优化器。  有些查询可能会超时。  
  
-   SQL Server Compact 不支持部分信任。  
  
## 请参阅  
 [参考](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)