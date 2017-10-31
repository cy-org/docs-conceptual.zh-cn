---
title: "SQL Server Express 用户实例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server Express 用户实例
Microsoft SQL Server 学习版 \(SQL Server Express\) 支持用户实例功能，只有在使用用于 SQL Server 的 .NET Framework 数据提供程序 \(`SqlClient`\) 时该功能才可用。  用户实例是 SQL Server Express 数据库引擎的单独实例，该单独实例由父实例生成。  不是其本地计算机的管理员的用户可以将用户实例附加和连接到 SQL Server Express 数据库。  在每个用户一个实例的基础上，每个实例在单个用户的安全上下文中运行。  
  
## 用户实例功能  
 用户实例对于在最小特权的用户帐户 \(LUA\) 下运行 Windows 的用户很有用，因为每个用户对在其计算机上运行的实例拥有 SQL Server 系统管理员 \(`sysadmin`\) 特权，而不必还以 Windows 管理员运行。  对具有有限权限的用户实例执行的软件无法进行系统范围的更改，因为 SQL Server Express 的实例在用户的非管理员 Windows 帐户下运行，而不是作为服务运行。  每个用户实例均独立于其父实例和在同一计算机上运行的其他任何用户实例。  对用户实例运行的数据库仅以单用户模式打开，而多个用户则无法连接到在用户实例上运行的数据库，  而且还将对用户实例禁用复制和分布式查询。  
  
 有关更多信息，请参见 SQL Server 2005 联机丛书中的“用户实例”。  
  
> [!NOTE]
>  对于已经是其各自计算机的管理员的用户不需要用户实例，而且对于涉及多个数据库用户的方案也不需要用户实例。  
  
## 启用用户实例  
 若要生成用户实例，必须运行 SQL Server Express 的父实例。  安装 SQL Server Express 后，默认情况下将启用用户实例，且对父实例执行 **sp\_configure** 系统存储过程的系统管理员可以显式启用或禁用用户实例。  
  
```  
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
 用于用户实例的网络协议必须为本地命名管道。  无法对 SQL Server 的远程实例启动用户实例，且不允许使用 SQL Server 登录名。  
  
## 连接到用户实例  
 `User Instance`  和 `AttachDBFilename` <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 关键字允许 <xref:System.Data.SqlClient.SqlConnection> 连接到用户实例。  <xref:System.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` 和 `AttachDBFilename` 属性也支持用户实例。  
  
 请注意如下所示的有关连接字符串示例的内容：  
  
-   `Data Source` 关键字是指生成用户实例的 SQL Server Express 的父实例。  默认实例为 .  \\sqlexpress。  
  
-   将 `Integrated Security` 设置为 `true`。  若要连接到用户实例，需要 Windows 身份验证；不支持 SQL Server 登录名。  
  
-   `User Instance` 设置为 `true`，这样就可调用用户实例。  （默认值为 `false`。）  
  
-   `AttachDbFileName` 连接字符串关键字用于附加主数据库文件 \(.mdf\)，该文件必须包含完整路径名。  `AttachDbFileName` 还与 <xref:System.Data.SqlClient.SqlConnection> 连接字符串中的“extended properties”和“initial file name”键相对应。  
  
-   包含在管道符号中的 `|DataDirectory|` 替代字符串是指打开连接的应用程序的数据目录，该字符串提供指示 .mdf 和 .ldf 数据库以及日志文件位置的相对路径。  如果要在其他位置查找这些文件，则必须提供这些文件的完整路径。  
  
```  
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  您也可以使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> <xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 和 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 属性在运行时构建连接字符串。  
  
### 使用 &#124;DataDirectory&#124; 替代字符串  
 在 ADO.NET 2.0 中，随着 `|DataDirectory|`（包含在管道符号中）替代字符串的引入，对 `AttachDbFileName` 进行了扩展。  `DataDirectory` 与 `AttachDbFileName` 结合使用可指示数据文件的相对路径，从而允许开发人员创建基于数据源的相对路径（而无需指定完整路径）的连接字符串。   ``  
  
 `DataDirectory` 点的物理位置取决于应用程序的类型。  在此示例中，要附加的 Northwind.mdf 文件位于应用程序的 \\app\_data 文件夹中。  
  
```  
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
 使用 `DataDirectory` 时，目录结构中的结果文件的路径不能高于替代字符串指向的目录。  例如，如果完全展开的 `DataDirectory` 为 C:\\AppDirectory\\app\_data，则上面显示的示例连接字符串有效，因为它在 c:\\AppDirectory 之下。  但是，如果尝试将 `DataDirectory` 指定为 `|DataDirectory|\..\data`，将会产生一个错误，因为 \\data 不是 \\AppDirectory 的子目录。  
  
 如果连接字符串的替代字符串格式不正确，将会引发 <xref:System.ArgumentException>。  
  
> [!NOTE]
>  <xref:System.Data.SqlClient> 会将替代字符串解析为本地计算机文件系统的完整路径。  因此，不支持远程服务器、HTTP 和 UNC 路径名。  如果在服务器未在本地计算机上的情况下打开连接，会引发异常。  
  
 打开 <xref:System.Data.SqlClient.SqlConnection> 时，会将其从默认 SQL Server Express 实例重定向到在调用方帐户下运行的已启动运行时的实例。  
  
> [!NOTE]
>  可能需要增大 <xref:System.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 值，因为加载用户实例所用时间可能比常规实例所用时间要长。  
  
 以下代码段打开新的 `SqlConnection`，在控制台窗口中显示连接字符串，然后在退出 `using` 代码块时关闭连接。  
  
```vb  
Private Sub OpenSqlConnection()  
    ' Retrieve the connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    Using connection As New SqlConnection(connectionString)  
        connection.Open()  
        Console.WriteLine("ConnectionString: {0}", _  
           connection.ConnectionString)  
    End Using  
End Sub  
```  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  在 SQL Server 内运行的公共语言运行库 \(CLR\) 代码中不支持用户实例。  如果对在连接字符串中具有 `User Instance=true` 的 <xref:System.Data.SqlClient.SqlConnection> 调用 `Open`，则会引发 <xref:System.InvalidOperationException>。  
  
## 用户实例连接的生存期  
 与作为服务运行的其他 SQL Server 版本不同，SQL Server Express 实例不需要手动启动和停止。  每次用户登录和连接到用户实例时，如果该用户实例尚未运行，则会启动该用户实例。  用户实例数据库设置 `AutoClose` 选项，这样数据库就会在一段非活动期后自动关闭。  已启动的 sqlservr.exe 进程会在实例的上一次连接关闭后的有限超时期限内继续运行，因此，如果在超时过期之前打开了另一连接，则不需要重新启动 sqlservr.exe 进程。  如果在超时过期之前没有打开新连接，则用户实例将自动关闭。  父实例的系统管理员通过使用 **sp\_configure** 更改 **user instance timeout** 选项，可为用户实例设置超时期限的持续时间。  默认值为 60 分钟。  
  
> [!NOTE]
>  如果 `Min Pool Size` 用于其值大于 0 的连接字符串中，则连接池将始终保持几个打开的连接，且用户实例将不会自动关闭。  
  
## 用户实例工作方式  
 为每个用户首次生成用户实例时，会将 **master** 和 **msdb** 系统数据库从模板数据文件夹复制到用户的本地应用程序数据存储库目录下的某个路径中，以供用户实例专用。  此路径通常为 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`。  启动用户实例时，**tempdb**、日志和跟踪文件也将被写入到此目录中。  将为该实例生成一个名称，且保证此名称对每个用户均是唯一的。  
  
 默认情况下，会授予 Windows Builtin\\Users 组的所有成员在本地实例上连接的权限，以及对 SQL Server 二进制文件进行读取和执行的权限。  验证持有用户实例的调用用户的凭据后，该用户就会成为该实例的 `sysadmin`。  只为用户实例启用共享内存，这意味着只能对本地计算机执行操作。  
  
 必须授予用户对连接字符串中指定的 .mdf 和 .ldf 文件的读写权限。  
  
> [!NOTE]
>  .mdf 和 .ldf 文件分别表示数据库和日志文件。  这两个文件为一个匹配集，因此在备份和还原操作期间必须小心谨慎。  数据库文件包含有关日志文件确切版本的信息，如果数据库与错误的日志文件耦合，则该数据库打不开。  
  
 若要避免数据损坏，则应使用独占访问权打开用户实例中的数据库。  如果两个不同的用户实例共享同一计算机上的同一个数据库，则第一个实例上的用户必须在关闭该数据库后，才能在第二个实例中打开该数据库。  
  
## 用户实例方案  
 用户实例向数据库应用程序开发人员提供 SQL Server 数据存储区，该数据存储区不依赖于在开发计算机上拥有管理员帐户的开发人员。  用户实例基于 Access\/Jet 模型，在该模型中，数据库应用程序仅连接到某个文件，且用户会自动拥有对所有数据库对象的完全权限，而无需系统管理员干预来授予权限。  用户实例应在以下情形中工作：用户在最小特权的用户帐户 \(LUA\) 下运行，没有对服务器或本地计算机的管理员权限，但需要创建数据库对象和应用程序。  用户实例允许用户在运行时创建在用户自己的安全上下文中运行的实例，而不是在较大权限系统服务的安全上下文中运行的实例。  
  
> [!IMPORTANT]
>  仅当所有使用应用程序均完全受信任时，才应使用用户实例。  
  
 用户实例方案包括：  
  
-   不需要共享数据的任何单用户应用程序。  
  
-   ClickOnce 部署。  如果 .NET Framework 2.0（或更高版本）和 SQL Server Express 已安装在目标计算机上，则可以由非管理员用户安装并使用通过 ClickOnce 操作而下载的安装程序包。  请注意，如果 SQL Server Express 为安装程序的一部分，则管理员必须安装 SQL Server Express。  有关详细信息，请参阅[ClickOnce Deployment for Windows Forms Applications](http://msdn.microsoft.com/zh-cn/34d8c770-48f2-460c-8d67-4ea5684511df)。  
  
-   使用 Windows 身份验证的专用 ASP.NET 宿主。  Intranet 上可以承载单个 SQL Server Express 实例。  应用程序使用 ASPNET Windows 帐户进行连接，而不是使用模拟进行连接。  用户实例不应用于第三方或共享宿主方案中，在这样的方案中，所有应用程序将共享同一用户实例，而不再保持彼此独立。  
  
## 请参阅  
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [连接字符串](../../../../../docs/framework/data/adonet/connection-strings.md)   
 [连接到数据源](../../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)