---
title: "在 ADO.NET 中的连接字符串 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 在 ADO.NET 中的连接字符串
.NET Framework 2.0 引入了用于处理连接字符串的新功能（包括将新的关键字引入到连接字符串生成器类），这将有助于在运行时创建有效的连接字符串。  
  
 连接字符串包含作为参数从数据提供程序传递到数据源的初始化信息。  其语法取决于数据提供程序，并且会在试图打开连接的过程中对连接字符串进行分析。  语法错误会生成运行时异常，但其他错误只有在数据源收到连接信息后才会发生。  经过验证后，数据源将应用连接字符串中指定的选项并打开连接。  
  
 连接字符串的格式是使用分号分隔的键\/值参数对列表：  
  
 `keyword1=value; keyword2=value;`  
  
 关键字不区分大小写，并将忽略键\/值对之间的空格。  不过，根据数据源的不同，值可能是区分大小写的。  任何包含分号、单引号或双引号的值必须用双引号引起来。  
  
 有效的连接字符串语法因提供程序而异，从早期的 API（如 ODBC）开始，已经过了多年的发展演变。  适用于 SQL Server 的 .NET Framework 数据提供程序 \(SqlClient\) 并入了早期语法中的许多元素，并且在使用通常的连接字符串语法时更具灵活性。  连接字符串语法元素经常会出现一些同等有效的同义词，但有些语法和拼写错误可能会导致出现问题。  例如，“`Integrated Security=true`”是有效的，而“`IntegratedSecurity=true`”则会导致出错。  另外，在运行时从未验证的用户输入构造的连接字符串可能导致字符串注入式攻击，从而危害数据源的安全。  
  
 为了解决这些问题，ADO.NET 2.0 为每个 .NET Framework 数据提供程序引入了新的连接字符串生成器。  关键字作为属性公开，以便在将连接字符串提交到数据源之前，能够对连接字符串语法进行验证。  
  
## 本节内容  
 [连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)  
 演示如何使用 `ConnectionStringBuilder` 类在运行时构造有效的连接字符串。  
  
 [连接字符串和配置文件](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)  
 演示如何在配置文件中存储和检索连接字符串。  
  
 [连接字符串语法](../../../../docs/framework/data/adonet/connection-string-syntax.md)  
 描述如何为 `SqlClient`、`OracleClient`、`OleDb` 和 `Odbc` 配置提供程序专用的连接字符串。  
  
 [保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)  
 演示保护用于连接到数据源的信息的各项技术。  
  
## 请参阅  
 [连接到数据源](../../../../ocs/framework/data/adonet/connecting-to-a-data-source.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)