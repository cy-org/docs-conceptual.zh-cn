---
title: "CLR 用户定义的类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# CLR 用户定义的类型
Microsoft SQL Server 提供了对使用 Microsoft .NET Framework 公共语言运行时 \(CLR\) 实现的用户定义类型 \(UDT\) 的支持。  CLR 集成在 SQL Server 中，通过此机制，您可以扩展数据库的类型系统。  UDT 使用户可以扩展 SQL Server 的数据类型系统，还可以定义复杂的结构化类型。  
  
 从应用程序结构的角度来说，UDT 具有两个重要的优点：  
  
-   在内部状态和外部行为之间强大的包装（无论在客户端中还是在服务器中）。  
  
-   与其他相关服务器功能的深度集成。  定义了自己的 UDT 后，可以在所有可使用 SQL Server 中的系统类型（包括列定义）的上下文中使用，并且可以作为变量、参数、函数结果、游标、触发器和复制使用。  
  
 有关更多详细信息，请参见您正在使用的 SQL Server 版本的“SQL Server 联机丛书”版本。  
  
 **SQL Server 联机丛书**  
  
1.  [CLR 用户定义类型](http://go.microsoft.com/fwlink/?LinkId=98366)（可能为英文网页）  
  
## 请参阅  
 [Creating SQL Server 2005 Objects In Managed Code](http://msdn.microsoft.com/zh-cn/5358a825-e19b-49aa-8214-674ce5fed1da)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)