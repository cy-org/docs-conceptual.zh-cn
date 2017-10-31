---
title: "使用 LINQ to SQL 的 N 层应用程序和远程应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 854a1cdd-53cb-45f5-83ca-63962a9b3598
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 使用 LINQ to SQL 的 N 层应用程序和远程应用程序
可以创建使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的 n 层或多层应用程序。  通常，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 数据上下文、实体类和查询构造逻辑作为数据访问层 \(DAL\) 位于中间层上。  业务逻辑和任何非持久性数据都可以在实体的分部类和分部方法中以及数据上下文中完整实现，也可以在单独的类中实现。  
  
 客户端或表示层调用中间层的远程接口上的方法，而该层上的 DAL 会执行映射到 <xref:System.Data.Linq.DataContext> 方法的查询或存储过程。  中间层通常以实体或代理对象的 XML 表示形式向客户端返回数据。  
  
 在中间层上，实体由数据上下文创建，数据上下文会跟踪实体的状态，并管理从数据库延迟加载实体以及将更改提交给数据库的过程。  这些实体被“附加”到 `DataContext`。  但是，在实体通过序列化发送到其他层后，这些实体会分离出来，这意味着 `DataContext` 不再跟踪它们的状态。  必须在将客户端发送回来进行更新的实体重新附加到数据上下文之后，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 才能将更改提交给数据库。  如果原始值和\/或时间戳是开放式并发检查所必需的，则客户端负责将它们返回给中间层。  
  
 在 ASP.NET 应用程序中，<xref:System.Web.UI.WebControls.LinqDataSource> 管理这一复杂过程的大部分工作。  有关详细信息，请参阅 [NIB: LinqDataSource Web Server Control Overview](http://msdn.microsoft.com/zh-cn/104cfc3f-7385-47d3-8a51-830dfa791136)。  
  
## 其他资源  
 有关如何实现使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的 n 层应用程序的更多信息，请参见以下主题：  
  
-   [具有 ASP.NET 的 LINQ to SQL N 层](../../../../../../docs/framework/data/adonet/sql/linq/linq-to-sql-n-tier-with-aspnet.md)  
  
-   [使用 Web 服务的 LINQ to SQL N 层](../../../../../../docs/framework/data/adonet/sql/linq/linq-to-sql-n-tier-with-web-services.md)  
  
-   [用于紧密耦合的客户端\-服务器应用程序的 LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/linq-to-sql-with-tightly-coupled-client-server-applications.md)  
  
-   [实现 N 层业务逻辑](../../../../../../docs/framework/data/adonet/sql/linq/implementing-business-logic-linq-to-sql.md)  
  
-   [N 层应用程序中的数据检索和 CUD 操作 \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md)  
  
 有关使用 ADO.NET 数据集的 n 层应用程序的详细信息，请参阅 [在 N 层应用程序中使用数据集](../Topic/Work%20with%20datasets%20in%20n-tier%20applications.md)。  
  
## 请参阅  
 [背景信息](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)