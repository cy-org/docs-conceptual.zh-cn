---
title: "使用 SqlDependency 检测更改 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用 SqlDependency 检测更改
<xref:System.Data.SqlClient.SqlDependency> 对象可以与 <xref:System.Data.SqlClient.SqlCommand> 关联，以便检测查询结果何时与最初检索的结果不同。  也可以向 `OnChange` 事件分配一个委托，当关联命令的结果更改时，将会触发该委托。  在执行命令前，必须将 <xref:System.Data.SqlClient.SqlDependency> 与该命令关联。  也可以使用 <xref:System.Data.SqlClient.SqlDependency> 的 `HasChanges` 属性来确定自从首次检索数据以来查询结果是否已经更改。  
  
## 安全注意事项  
 依赖项基础结构依赖于 <xref:System.Data.SqlClient.SqlConnection>，它会在调用 <xref:System.Data.SqlClient.SqlDependency.Start%2A> 时打开，以便接收有关给定命令的基础数据已经更改的通知。  客户端启动对 `SqlDependency.Start` 的调用的能力是通过使用 <xref:System.Data.SqlClient.SqlClientPermission> 和代码访问安全性属性来控制的。  有关详细信息，请参阅[启用查询通知](../../../../../docs/framework/data/adonet/sql/enabling-query-notifications.md)和[代码访问安全性和 ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md)。  
  
### 示例  
 下面的步骤演示如何声明依赖项、执行命令和在结果集更改时接收通知：  
  
1.  启动到服务器的 `SqlDependency` 连接。  
  
2.  创建 <xref:System.Data.SqlClient.SqlConnection> 和 <xref:System.Data.SqlClient.SqlCommand> 对象以连接到服务器并定义 Transact\-SQL 语句。  
  
3.  创建一个新的 `SqlDependency` 对象，或使用现有的对象，并将其绑定到 `SqlCommand` 对象。  这会在内部创建一个 <xref:System.Data.Sql.SqlNotificationRequest> 对象并根据需要将其绑定到命令对象。  此通知请求包含一个内部标识符，可唯一地标识此 `SqlDependency` 对象。  如果客户端侦听器尚未处于活动状态，它也将启动客户端侦听器。  
  
4.  订阅一个针对 `SqlDependency` 对象的 `OnChange` 事件的事件处理程序。  
  
5.  使用 `SqlCommand` 对象的任一 `Execute` 方法执行该命令。  因为该命令绑定到通知对象，所以服务器认识到它必须生成一个通知，并且队列信息将指向相关性队列。  
  
6.  停止到服务器的 `SqlDependency` 连接。  
  
 如果任何用户随后更改了基础数据，Microsoft SQL Server 会检测到有针对此更改的挂起通知并发布通知，此通知经过处理后通过调用 `SqlDependency.Start` 而创建的基础 `SqlConnection` 转发到客户端。  客户端侦听程序接收无效消息。  然后客户端侦听器定位关联的 `SqlDependency` 对象并触发 `OnChange` 事件。  
  
 下面的代码段演示创建示例应用程序所要使用的设计模式。  
  
```vb  
Sub Initialization()  
    ' Create a dependency connection.  
    SqlDependency.Start(connectionString, queueName)  
End Sub  
  
Sub SomeMethod()   
    ' Assume connection is an open SqlConnection.  
    ' Create a new SqlCommand object.  
    Using command As New SqlCommand( _  
      "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", _  
      connection)  
  
        ' Create a dependency and associate it with the SqlCommand.  
        Dim dependency As New SqlDependency(command)  
        ' Maintain the refence in a class member.  
        ' Subscribe to the SqlDependency event.  
        AddHandler dependency.OnChange, AddressOf OnDependencyChange  
  
        ' Execute the command.  
        Using reader = command.ExecuteReader()  
            ' Process the DataReader.  
        End Using  
    End Using  
End Sub   
  
' Handler method  
Sub OnDependencyChange(ByVal sender As Object, _  
    ByVal e As SqlNotificationEventArgs)   
    ' Handle the event (for example, invalidate this cache entry).  
End Sub  
  
Sub Termination()  
    ' Release the dependency  
    SqlDependency.Stop(connectionString, queueName)  
End Sub  
```  
  
```csharp  
void Initialization()  
{  
    // Create a dependency connection.  
    SqlDependency.Start(connectionString, queueName);  
}  
  
void SomeMethod()  
{  
    // Assume connection is an open SqlConnection.  
  
    // Create a new SqlCommand object.  
    using (SqlCommand command=new SqlCommand(  
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",   
        connection))  
    {  
  
        // Create a dependency and associate it with the SqlCommand.  
        SqlDependency dependency=new SqlDependency(command);  
        // Maintain the refence in a class member.  
  
        // Subscribe to the SqlDependency event.  
        dependency.OnChange+=new  
           OnChangeEventHandler(OnDependencyChange);  
  
        // Execute the command.  
        using (SqlDataReader reader = command.ExecuteReader())  
        {  
            // Process the DataReader.  
        }  
    }  
}  
  
// Handler method  
void OnDependencyChange(object sender,   
   SqlNotificationEventArgs e )  
{  
  // Handle the event (for example, invalidate this cache entry).  
}  
  
void Termination()  
{  
    // Release the dependency.  
    SqlDependency.Stop(connectionString, queueName);  
}  
```  
  
## 请参阅  
 [SQL Server 中的查询通知](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)