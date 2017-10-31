---
title: "安全数据访问 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 473ebd69-21a3-4627-b95e-4e04d035c56f
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 安全数据访问
要编写安全的 ADO.NET 代码，必须了解基础数据存储（即数据库）中提供的安全机制。  您还需要考虑应用程序可能包含的其他功能或组件对安全性的影响。  
  
## 身份验证、授权和权限  
 连接到 Microsoft SQL Server 后，您便可以使用 Windows 身份验证（也称为集成安全），它使用当前活动 Windows 用户的标识，而不是传递用户 ID 和密码。  由于不会在连接字符串中公开用户凭据，因此强烈建议使用 Windows 身份验证。  如果无法使用 Windows 身份验证连接到 SQL Server，请考虑使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 在运行时创建连接字符串。  
  
 用于身份验证的凭据需要根据应用程序的类型进行不同地处理。  例如，在 Windows 窗体应用程序中，可以提示用户提供身份验证信息，也可以使用用户的 Windows 凭据。  但是，Web 应用程序通常使用应用程序自身提供的凭据来访问数据，而不是使用用户提供的凭据。  
  
 用户经过身份验证后，其操作范围取决于向他们授予的权限。  始终遵循最小特权原则，并且仅授予绝对必需的权限。  
  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)|描述用于保护连接信息的最佳安全做法和技术，例如使用受保护配置来加密连接字符串。|  
|[Recommendations for Data Access Strategies](http://msdn.microsoft.com/zh-cn/72411f32-d12a-4de8-b961-e54fca7faaf5)|提供用于访问数据和执行数据库操作的建议。|  
|[连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)|描述如何在运行时根据用户输入生成连接字符串。|  
|[SQL Server 安全性概述](../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)|描述 SQL Server 安全架构。|  
  
## 参数化命令和 SQL 注入  
 使用参数化命令可帮助抵御 SQL 注入攻击，这种攻击的攻击者会将命令“注入”SQL 语句，从而危及服务器的安全。  通过确保将从外部源接收的值仅作为值（而不是作为 Transact\-SQL 语句的一部分）进行传递，参数化命令可抵御 SQL 注入攻击。  这样，便不会在数据源中执行插入到值中的 Transact\-SQL 命令。  相反，只会将这些命令作为参数值来计算。  除具备安全优势外，参数化命令还提供一种便捷方法，使用该方法可组织随 Transact\-SQL 语句传递或传递到存储过程的值。  
  
 有关使用参数化命令的更多信息，请参见下列资源。  
  
|资源|描述|  
|--------|--------|  
|[DataAdapter 参数](../../../../docs/framework/data/adonet/dataadapter-parameters.md)|描述如何对 `DataAdapter` 使用参数。|  
|[使用存储过程修改数据](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)|描述如何指定参数和获取返回值。|  
|[使用 SQL Server 中的存储过程管理权限](../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)|描述如何使用 SQL Server 存储过程包装数据访问。|  
  
## 脚本攻击  
 脚本攻击是另一种形式的注入，它使用插入到网页中的恶意字符。  浏览器无法验证这些插入字符，并且会将它们作为页面的一部分进行处理。  
  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[Script Exploits Overview](../Topic/Script%20Exploits%20Overview.md)|描述如何抵御脚本攻击和 SQL 语句攻击。|  
  
## 探测攻击  
 攻击者通常使用异常信息（如服务器、数据库或表的名称）来发动对系统的攻击。  由于异常包含有关您的应用程序或数据源的特定信息，因此您可以通过仅向客户端公开必要信息来帮助更好地保护应用程序和数据源。  
  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[异常处理基础知识](../../../../docs/standard/exceptions/exception-handling-fundamentals.md)|描述 try\/catch\/finally 结构化异常处理的基本形式。|  
|[异常的最佳做法](../../../../docs/standard/exceptions/best-practices-for-exceptions.md)|描述处理异常的最佳做法。|  
  
## 保护 Microsoft Access 和 Excel 数据源  
 当具有最少的安全要求或没有安全要求时，Microsoft Access 和 Microsoft Excel 可充当 ADO.NET 应用程序的数据存储区。  其安全功能作为一种阻止手段固然有效，但其作用仅限于阻止不了解情况的用户乱摸乱动而已。  Access 和 Excel 的物理数据文件位于文件系统上，并且注定可供所有用户访问。  这使得这些文件易受到攻击，从而导致文件失窃或数据丢失，因为他人可轻松复制或更改这些文件。  如果需要强有力的安全措施，请使用 SQL Server 或其他基于服务器的数据库，这样便无法从文件系统读取物理数据文件。  
  
 有关保护 Access 和 Excel 数据的更多信息，请参见下列资源。  
  
|资源|描述|  
|--------|--------|  
|[Access 2007 安全注意事项和指南](http://go.microsoft.com/fwlink/?LinkId=98354)（可能为英文网页）|描述 Access 2007 的安全技术，如加密文件、管理密码、将数据库转换为新的 ACCDB 和 ACCDE 格式以及使用其他安全选项。|  
|[通过用户级安全帮助保护 Access 数据库 \(MDB\)](http://go.microsoft.com/fwlink/?LinkId=47697)（可能为英文网页）|适用于 Access 2003。  提供用于实施用户级安全以保护 Access 2003 数据的说明。|  
|[理解工作组信息文件在 Access 安全中的角色](http://support.microsoft.com/kb/305542)（可能为英文网页）|说明工作组信息文件在 Access 2003 安全性中的作用和关系。|  
|[有关 Microsoft Access 2.0 至 2000 版的 Microsoft Access 安全性常见问题](http://go.microsoft.com/fwlink/?LinkId=47698)（可能为英文网页）|Microsoft Access 可下载版本的安全性常见问题。|  
|[安全和防护疑难解答](http://go.microsoft.com/fwlink/?LinkId=47703)（可能为英文网页）|演示与 Excel 2003 安全性有关的常见问题的解决方案。|  
  
## 企业服务  
 COM\+ 包含其自己的安全模型，该模型依赖于 Windows NT 帐户和进程\/线程模拟。  <xref:System.EnterpriseServices> 命名空间提供的包装允许 .NET 应用程序通过 <xref:System.EnterpriseServices.ServicedComponent> 类来集成托管代码与 COM\+ 安全服务。  
  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[COM\+ Role\-Based Security and the .NET Framework](http://msdn.microsoft.com/zh-cn/02ab22ef-e5e2-4d29-b33a-6e03d94c4981)|讨论如何集成托管代码与 COM\+ 安全服务。|  
  
## 与非托管代码交互操作  
 .NET Framework 提供与非托管代码（包括 COM 组件、COM\+ 服务、外部类型库及许多操作系统服务）的交互。  使用非托管代码时会超出托管代码的安全边界。  您的代码和调用它的任何代码都必须具有非托管代码权限（指定了 <xref:System.Security.Permissions.SecurityPermissionFlag> 标志的 <xref:System.Security.Permissions.SecurityPermission>）。  非托管代码会无意中将安全漏洞引入您的应用程序中。  因此，除非绝对必要，否则应避免与非托管代码进行交互。  
  
 有关更多信息，请参见以下资源。  
  
|资源|描述|  
|--------|--------|  
|[与非托管代码交互操作](../../../../docs/framework/interop/index.md)|包含描述如何向 .NET Framework 公开 COM 组件以及如何向 COM 公开 .NET Framework 组件的主题。|  
|[Advanced COM Interoperability](http://msdn.microsoft.com/zh-cn/3ada36e5-2390-4d70-b490-6ad8de92f2fb)|包含高级主题，如主互操作程序集、线程和自定义封送处理。|  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 安全性](../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Recommendations for Data Access Strategies](http://msdn.microsoft.com/zh-cn/72411f32-d12a-4de8-b961-e54fca7faaf5)   
 [保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)   
 [连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)