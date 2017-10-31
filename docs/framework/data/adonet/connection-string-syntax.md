---
title: "连接字符串语法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 连接字符串语法
每个 .NET Framework 数据提供程序都有一个继承自 <xref:System.Data.Common.DbConnection> 的 `Connection` 对象，以及一个提供程序特定的 <xref:System.Data.Common.DbConnection.ConnectionString%2A> 属性。  每个提供程序的特定连接字符串语法记录在其 `ConnectionString` 属性中。  下表列出了 .NET Framework 中包含的四个数据提供程序。  
  
|.NET Framework data provider — .NET Framework 数据提供程序|描述|  
|----------------------------------------------------------|--------|  
|<xref:System.Data.SqlClient>|提供 Microsoft SQL Server 的数据访问。  有关连接字符串语法的更多信息，请参见 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>。|  
|<xref:System.Data.OleDb>|提供对使用 OLE DB 公开的数据源中的数据的访问。  有关连接字符串语法的更多信息，请参见 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>。|  
|<xref:System.Data.Odbc>|提供对使用 ODBC 公开的数据源中数据的访问。  有关连接字符串语法的更多信息，请参见 <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A>。|  
|<xref:System.Data.OracleClient>|提供对 Oracle 8.1.7 或更高版本中数据的访问。  有关连接字符串语法的更多信息，请参见 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>。|  
  
## 连接字符串生成器  
 ADO.NET 2.0 为 .NET Framework 数据提供程序引入了以下连接字符串生成器。  
  
-   <xref:System.Data.SqlClient.SqlConnectionStringBuilder>  
  
-   <xref:System.Data.OleDb.OleDbConnectionStringBuilder>  
  
-   <xref:System.Data.Odbc.OdbcConnectionStringBuilder>  
  
-   <xref:System.Data.OracleClient.OracleConnectionStringBuilder>  
  
 连接字符串生成器使您可以在运行时构造具有有效语法的连接字符串，从而不必在代码中手动串联连接字符串值。  有关详细信息，请参阅[连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)。  
  
## Windows 身份验证  
 建议使用 Windows 身份验证（有时也称为“集成安全性”）连接到支持其的数据源。  连接字符串中使用的语法根据提供程序的不同而不同。  下表演示用于 .NET Framework 数据提供程序的 Windows 身份验证语法。  
  
|提供程序|语法|  
|----------|--------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  
|`OleDb`|`Integrated Security=SSPI;`|  
|`Odbc`|`Trusted_Connection=yes;`|  
|`OracleClient`|`Integrated Security=yes;`|  
  
> [!NOTE]
>  `Integrated Security=true` 用于 `OleDb` 提供程序时会引发异常。  
  
## SqlClient 连接字符串  
 <xref:System.Data.SqlClient.SqlConnection> 连接字符串的语法记录在 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName> 属性中。  您可以使用 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 属性来获取或设置 SQL Server 数据库的连接字符串。  如果您需要连接到早期版本的 SQL Server，则必须使用适用于 OleDb 的 .NET Framework 数据提供程序 \(<xref:System.Data.OleDb>\)。  大多数连接字符串关键字还会在 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 中映射为属性。  
  
 下列各个语法形式都将使用 Windows 身份验证连接到本地服务器上的 **AdventureWorks** 数据库。  
  
```  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  
  
### SQL Server 登录  
 Windows 身份验证是用于连接到 SQL Server 的首选方法。  但是，如果需要 SQL Server 身份验证，请使用下列语法来指定用户名和密码。  在此示例中，星号用来表示有效用户名和密码。  
  
```  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  
  
> [!IMPORTANT]
>  `Persist`  ``  `Security Info` 关键字的默认设置为 `false`。  如果将其设置为 `true` 或 `yes`，则允许在打开连接后通过连接获取安全敏感信息（包括用户 ID 和密码）。  保持将 `Persist` `` `Security Info` 设置为 `false`，以确保不受信任的来源不能访问敏感的连接字符串信息。  
  
 若要连接到 SQL Server 的命名实例，请使用“*服务器名\\实例名*”语法。  
  
```  
Data Source=MySqlServer\MSSQL1;"  
```  
  
 在生成连接字符串时，您还可以将 `SqlConnectionStringBuilder` 的 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> 属性设置为实例名。  <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> 属性是只读的。  
  
> [!NOTE]
>  Windows 身份验证优先于 SQL Server 登录。  如果您同时指定 Integrated Security\=true 以及用户名和密码，将忽略用户名和密码，而使用 Windows 身份验证。  
  
### 类型系统版本更改  
 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName> 中的 `Type System Version` 关键字指定 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 类型的客户端表示形式。  有关 `Type System Version` 关键字的更多信息，请参见 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName>。  
  
## 连接并附加到 SQL Server Express 用户实例  
 用户实例是 SQL Server Express 中的一个功能。  它们允许以最低权限的本地 Windows 帐户运行的用户附加并运行 SQL Server 数据库，而无需具有管理权限。  使用用户 Windows 凭据执行用户实例，而不是作为服务执行用户实例。  
  
 有关使用用户实例的更多信息，请参见[SQL Server Express 用户实例](../../../../docs/framework/data/adonet/sql/sql-server-express-user-instances.md)。  
  
## 使用 TrustServerCertificate  
 `TrustServerCertificate` 关键字仅在连接到具有有效证书的 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 实例时有效。  当 `TrustServerCertificate` 设置为 `true` 时，传输层将使用 SSL 来加密通道并跳过证书链以验证信任。  
  
```  
"TrustServerCertificate=true;"   
```  
  
> [!NOTE]
>  如果 `TrustServerCertificate` 设置为 `true` 并已启动加密，将使用对服务器指定的加密级别，即使 `Encrypt` 在连接字符串中被设置为 `false`。  否则连接将会失败。  
  
### 启用加密  
 如果要在未向服务器提供证书的情况下启用加密，必须在 SQL Server 配置管理器中设置**“强制协议加密”**和**“信任服务器证书”**选项。  在此情况下，如果未向服务器提供可验证的证书，加密将使用未经验证的自签名服务器证书。  
  
 应用程序设置无法降低在 SQL Server 中配置的安全级别，但可以增强安全级别。  应用程序可以通过将 `TrustServerCertificate` 和 `Encrypt` 关键字设置为 `true` 来请求加密，以保证在未提供服务器证书和未对客户端配置**“强制协议加密”**的情况下仍能够进行加密。  但是，如果未在客户端配置中启用 `TrustServerCertificate`，则仍需要提供服务器证书。  
  
 下表描述了各种情况。  
  
|“强制协议加密”客户端设置|“信任服务器证书”客户端设置|“密加\/使用数据加密”连接字符串\/属性|“信任服务器证书”连接字符串\/特性|结果|  
|-------------------|--------------------|---------------------------|------------------------|--------|  
|No|不可用|否（默认值）|忽略|不加密。|  
|No|不可用|是|否（默认值）|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
|No|不可用|是|是|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
|是|No|忽略|忽略|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
|是|是|否（默认值）|忽略|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
|是|是|是|否（默认值）|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
|是|是|是|是|只有在具有可验证的服务器证书的情况下才能进行加密，否则连接尝试将失败。|  
  
 有关更多信息，请参见 SQL Server 联机丛书中的[使用未经验证的加密](http://go.microsoft.com/fwlink/?LinkId=120500)（可能为英文网页）。  
  
## OleDb 连接字符串  
 通过 <xref:System.Data.OleDb.OleDbConnection> 的 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> 属性，您可以获取或设置 OLE DB 数据源（如 Microsoft Access）的连接字符串。  也可以使用 <xref:System.Data.OleDb.OleDbConnectionStringBuilder> 类在运行时创建一个 `OleDb` 连接字符串。  
  
### OleDb 连接字符串语法  
 必须为 <xref:System.Data.OleDb.OleDbConnection> 连接字符串指定提供程序名称。  下列连接字符串使用 Jet 提供程序连接到 Microsoft Access 数据库。  请注意，如果数据库未受到保护（默认值），可选择 `UserID` 和 `Password` 关键字。  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0; Data Source=d:\Northwind.mdb;User ID=Admin;Password=;   
```  
  
 如果使用用户级安全保护 Jet 数据库，则必须提供工作组信息文件 \(.mdw\) 的位置。  工作组信息文件用于验证连接字符串中显示的凭据。  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=d:\Northwind.mdb;Jet OLEDB:System Database=d:\NorthwindSystem.mdw;User ID=*****;Password=*****;  
```  
  
> [!IMPORTANT]
>  可以在通用数据链接 \(UDL\) 文件中提供 **OleDbConnection** 的连接信息；但是，应避免这样做。  UDL 文件未加密，会以明文形式公开连接字符串信息。  因为 UDL 文件对您的应用程序来说是一个基于文件的外部资源，所以无法使用 .NET Framework 保护该文件。  **SqlClient** 不支持 UDL 文件。  
  
### 使用 DataDirectory 连接到 Access\/Jet  
 `DataDirectory` 不是 `SqlClient` 独占的。  它还可以用于 <xref:System.Data.OleDb> 和 <xref:System.Data.Odbc> .NET 数据提供程序。  下面的 <xref:System.Data.OleDb.OleDbConnection> 字符串示例演示连接到应用程序 app\_data 文件夹中的 Northwind.mdb 所需的语法。  系统数据库 \(System.mdw\) 也存储在该位置。  
  
```  
"Provider=Microsoft.Jet.OLEDB.4.0;  
Data Source=|DataDirectory|\Northwind.mdb;  
Jet OLEDB:System Database=|DataDirectory|\System.mdw;"  
```  
  
> [!IMPORTANT]
>  如果 Access\/Jet 数据库未受到保护，则不需要在连接字符串中指定系统数据库的位置。  默认情况下安全性为关，所有用户可作为内置管理员用户使用空白密码进行连接。  即使在正确实现用户级安全时，Jet 数据库仍很容易受到攻击。  由于 Access\/Jet 数据库的基于文件的安全性架构存在固有弱点，因此不建议在 Access\/Jet 数据库中存储敏感信息。  
  
### 连接到 Excel  
 Microsoft Jet 提供程序用于连接到 Excel 工作簿。  下列连接字符串中的 `Extended Properties` 关键字会设置特定于 Excel 的属性。"  HDR\=Yes;”指示第一行包含列名称，但不包含数据；“IMEX\=1;”指示驱动程序始终将“intermixed”数据列作为文本进行读取。  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\MyExcel.xls;Extended Properties=""Excel 8.0;HDR=Yes;IMEX=1""  
```  
  
 请注意，`Extended Properties` 所需的双引号字符还必须包含在双引号中。  
  
### Data Shape 提供程序连接字符串语法  
 在使用 Microsoft Data Shape 提供程序时，请同时使用 `Provider` 和 `Data Provider` 关键字。  下面的示例使用 Shape 提供程序连接到 SQL Server 的本地实例。  
  
```  
"Provider=MSDataShape;Data Provider=SQLOLEDB;Data Source=(local);Initial Catalog=pubs;Integrated Security=SSPI;"   
```  
  
## Odbc 连接字符串  
 <xref:System.Data.Odbc.OdbcConnection> 的 <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A> 属性允许您获取或设置 OLE DB 数据源的连接字符串或。  <xref:System.Data.Odbc.OdbcConnectionStringBuilder> 也支持 Odbc 连接字符串。  
  
 下列连接字符串使用 Microsoft 文本驱动程序。  
  
```  
Driver={Microsoft Text Driver (*.txt; *.csv)};DBQ=d:\bin  
```  
  
### 使用 DataDirectory 连接到 Visual FoxPro  
 下面的 <xref:System.Data.Odbc.OdbcConnection> 连接字符串示例演示如何使用 `DataDirectory` 连接到 Microsoft Visual FoxPro 文件。  
  
```  
"Driver={Microsoft Visual FoxPro Driver};  
SourceDB=|DataDirectory|\MyData.DBC;SourceType=DBC;"  
```  
  
## Oracle 连接字符串  
 <xref:System.Data.OracleClient.OracleConnection> 的 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 属性允许您获取或设置 OLE DB 数据源的连接字符串或。  <xref:System.Data.OracleClient.OracleConnectionStringBuilder> 也支持 Oracle 连接字符串。  
  
```  
Data Source=Oracle9i;User ID=*****;Password=*****;  
```  
  
 有关 ODBC 连接字符串语法的更多信息，请参见 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>。  
  
## 请参阅  
 [连接字符串](../../../../docs/framework/data/adonet/connection-strings.md)   
 [连接到数据源](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)