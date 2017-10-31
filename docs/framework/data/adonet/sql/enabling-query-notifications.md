---
title: "启用查询通知 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 启用查询通知
使用查询通知的应用程序有一组通用的要求。  必须正确配置数据源才能支持 SQL 查询通知，并且用户必须具有正确的客户端和服务器端权限。  
  
 要使用查询通知，必须符合下列条件：  
  
-   对数据库启用查询通知。  
  
-   确保用于连接数据库的用户 ID 具有必要的权限。  
  
-   使用 <xref:System.Data.SqlClient.SqlCommand> 对象执行有效的 SELECT 语句，包含关联的通知对象 — <xref:System.Data.SqlClient.SqlDependency> 或 <xref:System.Data.Sql.SqlNotificationRequest>。  
  
-   提供所监视的数据更改时用于处理通知的代码。  
  
## 查询通知要求  
 仅对满足一系列特定要求的 SELECT 语句支持查询通知。  下表提供指向“SQL Server 联机丛书”中的 Service Broker 和“查询通知”文档的链接。  
  
 **SQL Server 联机丛书**  
  
-   [为通知创建查询](http://msdn.microsoft.com/library/ms181122.aspx)（可能为英文网页）  
  
-   [Service Broker 的安全注意事项](http://msdn.microsoft.com/library/ms166059.aspx)（可能为英文网页）  
  
-   [安全性和保护 \(Service Broker\)](http://msdn.microsoft.com/library/bb522911.aspx)（可能为英文网页）  
  
-   [Notification Services 的安全注意事项](http://msdn.microsoft.com/library/ms172604.aspx)（可能为英文网页）  
  
-   [查询通知权限](http://msdn.microsoft.com/library/ms188311.aspx)（可能为英文网页）  
  
-   [Service Broker 的国际化注意事项](http://msdn.microsoft.com/library/ms166028.aspx)（可能为英文网页）  
  
-   [解决方案设计注意事项 \(Service Broker\)](http://msdn.microsoft.com/library/bb522899.aspx)（可能为英文网页）  
  
-   [Service Broker 开发人员信息中心](http://msdn.microsoft.com/library/ms166100.aspx)（可能为英文网页）  
  
-   [开发人员指南 \(Service Broker\)](http://msdn.microsoft.com/library/bb522908.aspx)（可能为英文网页）  
  
## 启用查询通知运行示例代码  
 若要通过使用 SQL Server Management Studio 在 **AdventureWorks** 数据库上启用 Service Broker，请执行下面的 Transact\-SQL 语句：  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 若要此查询通知示例正确运行，必须在数据库服务器上执行下面的 Transact\-SQL 语句。  
  
```  
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## 查询通知权限  
 执行请求通知的命令的用户必须在服务器上具有 SUBSCRIBE QUERY NOTIFICATIONS 数据库权限。  
  
 在部分信任情况下运行的客户端代码要求 <xref:System.Data.SqlClient.SqlClientPermission>。  
  
 下面的代码创建一个 <xref:System.Data.SqlClient.SqlClientPermission> 对象，将 <xref:System.Security.Permissions.PermissionState> 设置为 <xref:System.Security.Permissions.PermissionState>。  如果尚未为调用堆栈中的所有高级调用方授予该权限，则 <xref:System.Security.CodeAccessPermission.Demand%2A> 将在运行时强制引发 <xref:System.Security.SecurityException>。  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## 选择通知对象  
 查询通知 API 提供两个用于处理通知的对象：<xref:System.Data.SqlClient.SqlDependency> 和 <xref:System.Data.Sql.SqlNotificationRequest>。  通常情况下，大多数非 ASP.NET 应用程序应使用 <xref:System.Data.SqlClient.SqlDependency> 对象。  ASP.NET 应用程序应使用更高级别的 <xref:System.Web.Caching.SqlCacheDependency>，以便包装 <xref:System.Data.SqlClient.SqlDependency> 并为管理通知和缓存对象提供框架。  
  
### 使用 SqlDependency  
 要使用 <xref:System.Data.SqlClient.SqlDependency>，必须对所使用的 SQL Server 数据库启用 Service Broker，并且用户必须具有接收通知的权限。  Service Broker 对象（例如通知队列）已预定义。  
  
 此外，<xref:System.Data.SqlClient.SqlDependency> 会自动启动一个辅助线程以在通知发布到队列中时处理这些通知；它还会分析 Service Broker 消息，将此信息作为事件参数数据公开。  必须通过调用 `Start` 方法初始化 <xref:System.Data.SqlClient.SqlDependency>，以建立与数据库的相关性。  此方法是静态方法，在为每个所需的数据库连接初始化应用程序期间只需调用一次。  必须在应用程序终止时为执行的每个相关连接调用 `Stop` 方法。  
  
### 使用 SqlNotificationRequest  
 相对而言，<xref:System.Data.Sql.SqlNotificationRequest> 要求您自己实现整个侦听基础结构。  此外，必须定义队列所支持的所有支持 Service Broker 对象（例如队列、服务和消息类型）。  如果应用程序要求特殊的通知消息或通知行为，或应用程序是更大的服务中介应用程序的一部分，此手动方法非常有用。  
  
## 请参阅  
 [SQL Server 中的查询通知](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)