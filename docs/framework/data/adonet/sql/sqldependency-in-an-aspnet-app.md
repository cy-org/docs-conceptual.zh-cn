---
title: "ASP.NET 应用程序中的 SqlDependency | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ASP.NET 应用程序中的 SqlDependency
本节中的示例演示如果通过利用 ASP.NET <xref:System.Web.Caching.SqlCacheDependency> 对象间接使用 <xref:System.Data.SqlClient.SqlDependency>。  <xref:System.Web.Caching.SqlCacheDependency> 对象使用 <xref:System.Data.SqlClient.SqlDependency> 来侦听通知和正确更新缓存。  
  
> [!NOTE]
>  示例代码假定已通过执行[启用查询通知](../../../../../docs/framework/data/adonet/sql/enabling-query-notifications.md)中的脚本启用了查询通知。  
  
## 关于示例应用程序  
 示例应用程序使用单个 ASP.NET 网页在 <xref:System.Web.UI.WebControls.GridView> 控件中显示 **AdventureWorks** SQL Server 数据库中的产品信息。  加载页面时，代码将当前时间写入 <xref:System.Web.UI.WebControls.Label> 控件。  然后，它定义一个 <xref:System.Web.Caching.SqlCacheDependency> 对象并设置 <xref:System.Web.Caching.Cache> 对象的属性，以存储最多三分钟的缓存数据。  然后，代码连接到数据库并检索数据。  加载页面后且应用程序运行时，ASP.NET 将从缓存中检索数据，这可以通过观察页面上的时间不改变来加以验证。  如果监视的数据发生更改，ASP.NET 将令缓存失效并用新数据重新填充 `GridView` 控件，更新 `Label` 控件中显示的时间。  
  
## 创建示例应用程序  
 请执行下面的步骤来创建并运行示例应用程序：  
  
1.  创建一个新的 ASP.NET 网站。  
  
2.  向 Default.aspx 页面添加一个 <xref:System.Web.UI.WebControls.Label> 和一个 <xref:System.Web.UI.WebControls.GridView> 控件。  
  
3.  打开该页面的类模块并添加下面的指令：  
  
    ```vb  
  
    Option Strict On  
    Option Explicit On  
  
    Imports System.Data.SqlClient  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4.  在该页面的 `Page_Load` 事件中添加下面的代码：  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#1)]
     [!code-vb[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#1)]  
  
5.  添加两个帮助器方法 `GetConnectionString` 和 `GetSQL`。  已定义的连接字符串使用集成安全性。  您将需要验证所使用的帐户是否具有必要的数据库权限，并且示例数据库 **AdventureWorks** 是否启用了通知。  有关详细信息，请参阅[Special Considerations When Using Query Notifications](http://msdn.microsoft.com/zh-cn/a83c8dc8-4fb9-4ffd-a2a5-c07cf4a203c7)。  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#2)]
     [!code-vb[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#2)]  
  
### 测试应用程序  
 如果没有活动，应用程序将会缓存 Web 窗体上显示的数据并每隔三分钟刷新一次。  如果对数据库发生了更改，则立即刷新缓存。  从 Visual Studio 中运行应用程序，将页面加载到浏览器中。  显示的缓存刷新时间指示最后刷新缓存的时间。  等待三分钟，然后刷新页面，使回发事件发生。  请注意，页面上显示的时间已发生改变。  如果您在三分钟之内刷新页面，页面上显示的时间将保持不变。  
  
 现在使用 Transact\-SQL UPDATE 命令更新数据库中的数据并刷新页面。  此时显示的时间指示已用数据库中的新数据刷新了缓存。  请注意，虽然已更新缓存，但页面上显示的时间在回发事件发生之前仍将保持不变。  
  
## 请参阅  
 [SQL Server 中的查询通知](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)