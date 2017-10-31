---
title: "如何：开发在 IIS 上运行的 WCF 数据服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 部署"
  - "WCF 数据服务, 开发"
  - "WCF 数据服务, 承载"
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 如何：开发在 IIS 上运行的 WCF 数据服务
本主题介绍如何使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 来基于 Internet Information Services \(IIS\) 上运行的 ASP.NET Web 应用程序所承载的 Northwind 示例数据库创建一个数据服务。  有关如何创建与 ASP.NET Development Server 上运行的 ASP.NET Web 应用程序相同的 Northwind 数据服务的示例，请参见 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)。  
  
> [!NOTE]
>  若要创建 Northwind 数据服务，您的本地计算机上必须已安装 Northwind 示例数据库。  若要下载此示例数据库，请访问 [SQL Server 的示例数据库](http://go.microsoft.com/fwlink/?linkid=24758)（可能为英文网页）下载页。  
  
 本主题说明如何使用实体框架提供程序创建数据服务。  还有其他一些数据服务提供程序可以使用。  有关详细信息，请参阅[数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)。  
  
 在创建服务之后，您必须显式提供对数据服务资源的访问权限。  有关详细信息，请参阅[如何：启用对数据服务的访问](../../../../docs/framework/data/wcf/how-to-enable-access-to-the-data-service-wcf-data-services.md)。  
  
### 创建在 IIS 上运行的 ASP.NET Web 应用程序  
  
1.  在 Visual Studio 中的**“文件”**菜单上，选择**“新建”**，然后选择**“项目”**。  
  
2.  在**“新建项目”**对话框中，选择 Visual Basic 或 Visual C\# 作为编程语言。  
  
3.  在**“模板”**窗格中，选择**“ASP.NET Web 应用程序”**。  注意：如果使用的是 Visual Studio Web Developer，则必须创建新的网站，而不是新的 Web 应用程序。  
  
4.  键入 `NorthwindService` 作为项目的名称。  
  
5.  单击“确定”。  
  
6.  在**“项目”**菜单上，选择**“NorthwindService 属性”**。  
  
7.  选择**“Web”**选项卡，然后选择**“使用本地 IIS Web 服务器”**。  
  
8.  单击**“创建虚拟目录”**，然后单击**“确定”**。  
  
9. 从具有管理员权限的命令提示符中，根据操作系统，执行以下命令之一：  
  
    -   32 位系统：  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i  
        ```  
  
    -   64 位系统：  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i  
        ```  
  
     这样将确保在计算机上注册 Windows Communication Foundation \(WCF\)。  
  
10. 从具有管理员权限的命令提示符中，根据操作系统，执行以下命令之一：  
  
    -   32 位系统：  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable  
        ```  
  
    -   64 位系统：  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable  
        ```  
  
     这将确保在计算机上安装了 WCF 之后，IIS 能够正常运行。  您可能必须重启 IIS。  
  
11. 当 ASP.NET 应用程序在 IIS7 上运行时，您还必须执行以下操作：  
  
    1.  打开 IIS 管理器并导航到**“默认网站”**下的 PhotoService 应用程序。  
  
    2.  在**“功能视图”**中双击**“身份验证”**。  
  
    3.  在**“身份验证”**页，选择**“匿名身份验证”**。  
  
    4.  在**“操作”**窗格，单击**“编辑”**，以在匿名用户将要连接到的网站下设置安全主体。  
  
    5.  在**“编辑匿名身份验证凭据”**对话框中，选择**“应用程序池标识”**。  
  
    > [!IMPORTANT]
    >  使用 Network Service 帐户时，您必须授予匿名用户与该账户关联的所有内部网络访问权限。  
  
12. 通过在 Visual Studio 中使用 SQL Server Management Studio、sqlcmd.exe 实用工具或 Transact\-SQL Editor，针对附加有 Northwind 数据库的 SQL Server 实例执行下面的 Transact\-SQL 命令：  
  
    ```sql  
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;  
    GO   
    ```  
  
     这将在 SQL Server 实例中为用于运行 IIS 的 Windows 帐户创建一个登录名。  这样，IIS 即可连接到 SQL Server 实例。  
  
13. 附加 Northwind 数据库后，执行下面的 Transact\-SQL 命令：  
  
    ```sql  
    USE Northwind  
    GO  
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]   
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];  
    GO  
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]   
    WITH DEFAULT_DATABASE=[Northwind];   
    GO  
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'  
    GO  
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'  
    GO   
    ```  
  
     这将为新登录名授予相应权限，使得 IIS 能够在 Northwind 数据库中读出和写入数据。  
  
### 定义数据模型  
  
1.  在**“解决方案资源管理器”**中，右击 ASP.NET 项目的名称，然后单击**“添加新项”**。  
  
2.  在**“添加新项”**对话框中，选择**“ADO.NET 实体数据模型”**。  
  
3.  键入 `Northwind.edmx` 作为数据模型的名称。  
  
4.  在实体数据模型向导中，选择**“从数据库生成”**，然后单击**“下一步”**。  
  
5.  通过执行下列步骤之一，将数据模型连接到数据库，然后单击**“下一步”**：  
  
    -   如果尚未配置数据库连接，请单击**“新建连接”**并创建一个新连接。  有关更多信息，请参见[如何：创建到 SQL Server 数据库的连接](http://go.microsoft.com/fwlink/?LinkId=123631)（可能为英文网页）。  此 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 实例必须附加了 Northwind 示例数据库。  
  
         \- 或 \-  
  
    -   如果已配置一个连接到 Northwind 数据库的数据库连接，请从连接列表中选择该连接。  
  
6.  在向导的最后一页中，选中数据库中所有表对应的复选框，并清除视图和存储过程对应的复选框。  
  
7.  单击**“完成”**关闭向导。  
  
    > [!NOTE]
    >  此生成的数据模型将在实体类型上公开外键属性。  使用 Visual Studio 2008 创建的数据模型不包括这些外键属性。  因此，在尝试访问使用 Visual Studio 2008 创建的 Northwind 数据服务之前，必须更新已创建的任何客户端应用程序的客户端数据服务类才能访问这一版本的 Northwind 数据服务。  
  
### 创建数据服务  
  
1.  在**“解决方案资源管理器”**中，右击 ASP.NET 项目的名称，然后单击**“添加新项”**。  
  
2.  在**“添加新项”**对话框中，选择**“ADO.NET 数据服务”**。  
  
3.  键入 `Northwind` 作为服务的名称。  
  
     Visual Studio 将为新服务创建 XML 标记和代码文件。  默认情况下，代码编辑器窗口将打开。  在**“解决方案资源管理器”**中，该服务的名称为 Northwind 并带有扩展名 .svc.cs 或 .svc.vb。  
  
4.  在数据服务的代码中，用数据模型的实体容器的类型（在此示例中为 `NorthwindEntities`）替换定义数据服务的类定义中的注释 `/* TODO: put your data source class name here */`。  该类定义应如下所示：  
  
     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]  
  
## 请参阅  
 [将数据作为服务公开](../../../../docs/framework/data/wcf/exposing-your-data-as-a-service-wcf-data-services.md)