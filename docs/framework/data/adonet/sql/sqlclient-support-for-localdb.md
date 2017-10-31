---
title: "SqlClient 对 LocalDB 的支持 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# SqlClient 对 LocalDB 的支持
从 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]（代号 Denali）开始，提供轻量版本 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]（称为 LocalDB）。 本主题讨论如何连接到 LocalDB 数据库。  
  
## 备注  
 有关 LocalDB 的更多信息（包括如何安装 LocalDB 和配置 LocalDB 实例），请参见 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书。  
  
 以下汇总了使用 LocalDB 可以执行的操作：  
  
-   使用 sqllocaldb.exe 或 app.config 文件创建和启动 LocalDB 实例。  
  
-   使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如 `sqlcmd -S (localdb)\myinst`。  
  
-   使用 `AttachDBFilename` 连接字符串关键字将数据库添加到 LocalDB 实例。 使用 `AttachDBFilename` 时，如果不使用 `Database` 连接字符串关键字指定数据库的名称，则在应用程序关闭时，将从 LocalDB 实例中删除数据库。  
  
-   在连接字符串中指定 LocalDB 实例。 例如，如果实例名称是 `myInstance`，连接字符串将包括：  
  
    ```  
    server=(localdb)\\myInstance  
    ```  
  
 连接到 LocalDB 数据库时，不允许 `User Instance=True`。  
  
 可以从 [Microsoft SQL Server 2012 功能包](http://www.microsoft.com/download/en/details.aspx?id=29065)下载 LocalDB。 如果将使用 sqlcmd.exe 来修改 LocalDB 实例中的数据，将需要 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 中的 sqlcmd，也可以从 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 功能包中获得它。  
  
## 以编程方式创建命名实例  
 应用程序可以创建命名实例并指定数据库，如下所示：  
  
-   在 app.config 文件中指定要创建的 LocalDB 实例，如下所示。  实例版本号应与 LocalDB 安装的版本号相同。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?> <configuration> <configSections> <section name="system.data.localdb" type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/> </configSections> <system.data.localdb> <localdbinstances> <add name="myInstance" version="11.0" /> </localdbinstances> </system.data.localdb> </configuration>  
    ```  
  
-   使用 `server` 连接字符串关键字指定实例名称。`server` 连接字符串关键字中指定的实例名称必须与 app.config 文件中指定的名称匹配。  
  
-   使用 `AttachDBFilename` 连接字符串关键字来指定 .MDF 文件。  
  
## 请参阅  
 [SQL Server 功能和 ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-features-and-adonet.md)   
 [ADO.NET 托管提供程序和 DataSet 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)