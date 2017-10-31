---
title: "连接字符串生成器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 连接字符串生成器
在 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 的早期版本中，不会对具有串联字符串值的连接字符串进行编译时检查，因此在运行时，不正确的关键字会产生 <xref:System.ArgumentException>。  每个 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序支持的连接字符串关键字的语法不同，这使得手动构造有效连接字符串变得很困难。  为了解决这个问题，[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 为每个 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序引入了新的连接字符串生成器。  每个数据提供程序包括一个从 <xref:System.Data.Common.DbConnectionStringBuilder> 继承的强类型连接字符串生成器类。  下表列出了 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序及其关联的连接字符串生成器类。  
  
|提供程序|ConnectionStringBuilder 类|  
|----------|-------------------------------|  
|<xref:System.Data.SqlClient>|<xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OleDb>|<xref:System.Data.OleDb.OleDbConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.Odbc>|<xref:System.Data.Odbc.OdbcConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OracleClient>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=fullName>|  
  
## 连接字符串注入式攻击  
 当使用动态字符串串联根据用户输入生成连接字符串时，可能发生连接字符串注入式攻击。  如果未验证字符串并且未转义恶意文本或字符，则攻击者可能会访问服务器上的敏感数据或其他资源。  例如，攻击者可以通过提供分号并追加其他值来发起攻击。  连接字符串通过“last one wins”算法分析，恶意的输入被替换为合法的值。  
  
 连接字符串生成器类旨在排除推测，防止出现语法错误和安全漏洞。  它们提供与每个数据提供程序允许的已知键\/值对相对应的方法和属性。  每个类都保持一个固定的同义词集合，可以将同义词转换为相应的已知键名。  将执行键\/值对的有效性检查，无效对会引发异常。  此外，还会以一种安全方式处理插入的值。  
  
 下面的示例演示 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 如何处理为 `Initial Catalog` 设置插入的额外值。  
  
```vb  
Dim builder As New System.Data.SqlClient.SqlConnectionStringBuilder  
builder("Data Source") = "(local)"  
builder("Integrated Security") = True  
builder("Initial Catalog") = "AdventureWorks;NewValue=Bad"  
Console.WriteLine(builder.ConnectionString)  
```  
  
```csharp  
System.Data.SqlClient.SqlConnectionStringBuilder builder =  
  new System.Data.SqlClient.SqlConnectionStringBuilder();  
builder["Data Source"] = "(local)";  
builder["integrated Security"] = true;  
builder["Initial Catalog"] = "AdventureWorks;NewValue=Bad";  
Console.WriteLine(builder.ConnectionString);  
```  
  
 输出结果表明，通过用双引号转义该额外值而不作为新的键\/值对将其追加到连接字符串，<xref:System.Data.SqlClient.SqlConnectionStringBuilder> 可以正确处理此额外值。  
  
```  
data source=(local);Integrated Security=True;  
initial catalog="AdventureWorks;NewValue=Bad"  
```  
  
## 从配置文件生成连接字符串  
 如果事先知道连接字符串的某些元素，则可以将其存储在配置文件中，并在运行时检索它们以构造完整连接字符串。  例如，可能事先知道数据库的名称，但不知道服务器的名称。  或者，您可能希望用户在运行时提供用户名和密码，而不能在连接字符串中插入其他值。  
  
 连接字符串生成器的一个重载构造函数将 <xref:System.String> 作为参数，这可让您提供部分连接字符串，然后通过用户输入使这部分连接字符串成为完整字符串。  该部分连接字符串可以存储在配置文件中并在运行时进行检索。  
  
> [!NOTE]
>  <xref:System.Configuration> 命名空间允许通过编程方式访问配置文件（对 Web 应用程序使用 <xref:System.Web.Configuration.WebConfigurationManager>，对 Windows 应用程序使用 <xref:System.Configuration.ConfigurationManager>）。  有关使用连接字符串和配置文件的更多信息，请参见[连接字符串和配置文件](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)。  
  
### 示例  
 此示例演示如何从配置文件中检索部分连接字符串并通过设置 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 的 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>、<xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> 和 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> 属性完成该连接字符串。  配置文件定义如下。  
  
```  
<connectionStrings>  
  <clear/>  
  <add name="partialConnectString"   
    connectionString="Initial Catalog=Northwind;"  
    providerName="System.Data.SqlClient" />  
</connectionStrings>  
```  
  
> [!NOTE]
>  必须在项目中设置对 `System.Configuration.dll` 的引用，才能运行代码。  
  
 [!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/CS/source.cs#1)]
 [!code-vb[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/VB/source.vb#1)]  
  
## 请参阅  
 [连接字符串](../../../../docs/framework/data/adonet/connection-strings.md)   
 [隐私和数据安全](../../../../docs/framework/data/adonet/privacy-and-data-security.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)