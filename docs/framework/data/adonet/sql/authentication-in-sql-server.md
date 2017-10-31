---
title: "SQL Server 中的身份验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# SQL Server 中的身份验证
[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 支持两种身份验证模式，即 Windows 身份验证模式和混合模式。  
  
-   Windows 身份验证是默认模式（通常称为集成安全），因为此 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 安全模型与 Windows 紧密集成。  信任特定 Windows 用户和组帐户登录 SQL Server。  已经过身份验证的 Windows 用户不必提供附加的凭据。  
  
-   混合模式支持由 Windows 和 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 进行身份验证。  用户名和密码保留在 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 内。  
  
> [!IMPORTANT]
>  我们建议尽可能使用 Windows 身份验证。  Windows 身份验证使用一系列加密消息来验证 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中的用户。  使用 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录时，将跨网络传递 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录名和密码，这样会降低它们的安全性。  
  
 使用 Windows 身份验证时，用户已登录到 Windows，无需另外登录到 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]。  下面的 `SqlConnection.ConnectionString` 可指定 Windows 身份验证，而无需用户名或密码。  
  
```  
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
>  登录名与数据库用户名不同。  您必须通过单独的操作将登录或 Windows 组映射到数据库用户或角色。  然后向用户或角色授予访问数据库对象的权限。  
  
## 身份验证方案  
 在下列情形中，Windows 身份验证通常为最佳选择：  
  
-   存在域控制器。  
  
-   应用程序和数据库位于同一台计算机上。  
  
-   您正在使用 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] Express 或 LocalDB 的实例。  
  
 SQL Server 登录常常在以下情况中使用：  
  
-   您有工作组。  
  
-   用户从其他不受信任的域进行连接。  
  
-   Internet 应用程序（例如 [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)]）。  
  
> [!NOTE]
>  指定 Windows 身份验证不会禁用 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录。  使用 ALTER LOGIN DISABLE [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 语句可禁用具有高级权限的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录。  
  
## 登录类型  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 支持三种登录类型：  
  
-   本地 Windows 用户帐户或受信任的域帐户。  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 依靠 Windows 来对 Windows 用户帐户进行身份验证。  
  
-   Windows 组。  向 Windows 组授予访问权限会向作为该组的成员的所有 Windows 用户登录授予访问权限。  
  
-   [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录。  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 将用户名和密码的哈希都存储在 master 数据库中，使用内部身份验证方法来验证登录尝试。  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 提供了从证书或非对称密钥创建的登录名，仅用于代码签名。  这些登录名不能用于连接到 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]。  
  
## 混合模式身份验证  
 如果您必须使用混合模式身份验证，则必须创建 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录名，这些登录名存储在 SQL Server 中。  然后，您必须在运行时提供 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 用户名和密码。  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 使用名为 `sa`（“system administrator”的缩写）的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录名进行安装。  为 `sa` 登录分配一个强密码，并且不要在应用程序中使用 `sa` 登录。  `sa` 登录名会映射到 `sysadmin` 固定服务器角色，它对整个服务器有不能撤销的管理凭据。  如果攻击者以系统管理员的身份获取了访问权限，则可能造成的危害是无法预计的。  默认情况下，Windows `BUILTIN\Administrators` 组（本地管理员组）的所有成员均为 `sysadmin` 角色的成员，但可以从该角色中移除这些成员。  
  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 提供了在 [!INCLUDE[winxpsvr](../../../../../includes/winxpsvr-md.md)] 或更高版本上运行时 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 登录的 Windows 密码策略机制。  密码复杂性策略通过增加可能密码的数量来阻止强力攻击。  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 可将 [!INCLUDE[winxpsvr](../../../../../includes/winxpsvr-md.md)] 中使用的相同复杂性和到期策略应用于 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中使用的密码。  
  
> [!IMPORTANT]
>  连接来自用户输入的连接字符串会使您遭受连接字符串注入攻击。  可使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 在运行时创建语法构成有效的连接字符串。  有关详细信息，请参阅[连接字符串生成器](../../../../../docs/framework/data/adonet/connection-string-builders.md)。  
  
## 外部资源  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书中的[主体](http://msdn.microsoft.com/library/bb543165.aspx)（可能为英文网页）|介绍了 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中的登录名和其他安全主体。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 中的应用程序安全机制方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [连接到数据源](../../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [连接字符串](../../../../../docs/framework/data/adonet/connection-strings.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)