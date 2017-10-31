---
title: "创建数据服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34d1d971-5e18-4c22-9bf6-d3612e27ea59
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 创建数据服务
在此任务中，您将创建一个示例数据服务，该数据服务使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 来公开一个基于 Northwind 示例数据库的 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源。此任务涉及以下基本步骤：  
  
1.  创建一个 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序。  
  
2.  使用[!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)]工具定义数据模型。  
  
3.  向 Web 应用程序添加数据服务。  
  
4.  启用对数据服务的访问。  
  
> [!NOTE]
>  在完成此任务时创建的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序将在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 提供的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Development Server 上运行。  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Development Server 仅支持来自本地计算机的访问。  为了便于在开发的过程中测试数据服务和解决问题，可考虑通过使用 Internet Information Services \(IIS\) 运行承载数据服务的应用程序。  有关详细信息，请参阅[如何：开发在 IIS 上运行的 WCF 数据服务](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)。  
  
### 创建 ASP.NET Web 应用程序  
  
1.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中的**“文件”**菜单上，选择**“新建”**，然后选择**“项目”**。  
  
2.  在**“新建项目”**对话框中的“[!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]”或“[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]”下，选择**“Web”**模板，然后选择**“ASP.NET Web 应用程序”**。  
  
    > [!NOTE]
    >  如果使用的是 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Web Developer，则必须创建新的网站，而不是创建新的 Web 应用程序。  
  
3.  键入 `NorthwindService` 作为项目的名称。  
  
4.  单击“确定”。  
  
5.  （可选）为 Web 应用程序指定一个特定的端口号。  注意：在快速入门的其余部分使用端口号 `12345`。  
  
    1.  在**“解决方案资源管理器”**中，右击刚刚创建的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目的名称，然后单击**“属性”**。  
  
    2.  选择**“Web”**选项卡，并将**“特定端口”**文本框的值设置为 `12345`。  
  
### 定义数据模型  
  
1.  在**“解决方案资源管理器”**中，右击 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目的名称，然后单击**“添加新项”**。  
  
2.  在**“添加新项”**对话框中，单击“数据”模板，然后选择**“ADO.NET 实体数据模型”**。  
  
3.  键入 `Northwind.edmx` 作为数据模型的名称。  
  
4.  在“[!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)]向导”中，选择**“从数据库生成”**，然后单击**“下一步”**。  
  
5.  通过执行下列步骤之一，将数据模型连接到数据库，然后单击**“下一步”**：  
  
    -   如果尚未配置数据库连接，请单击**“新建连接”**并创建一个新连接。  有关更多信息，请参见[如何：创建到 SQL Server 数据库的连接](http://go.microsoft.com/fwlink/?LinkId=123631)（可能为英文网页）。  此 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 实例必须附加了 Northwind 示例数据库。  
  
         \- 或 \-  
  
    -   如果已配置一个连接到 Northwind 数据库的数据库连接，请从连接列表中选择该连接。  
  
6.  在向导的最后一页中，选中数据库中所有表对应的复选框，并清除视图和存储过程对应的复选框。  
  
7.  单击**“完成”**关闭向导。  
  
    > [!NOTE]
    >  此生成的数据模型将在实体类型上公开外键属性。  使用 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 2008 创建的数据模型不包括这些外键属性。  因此，在尝试访问使用 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 2008 创建的 Northwind 数据服务之前，必须更新已创建的所有客户端应用程序的客户端数据服务类，然后才能访问这一版本的 Northwind 数据服务。  
  
### 创建数据服务  
  
1.  在**“解决方案资源管理器”**中，右击 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目的名称，然后单击**“添加新项”**。  
  
2.  在**“添加新项”**对话框中，选择**“WCF 数据服务”**。  
  
3.  键入 `Northwind` 作为服务的名称。  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 将为新服务创建 XML 标记和代码文件。  默认情况下，代码编辑器窗口将打开。  在**“解决方案资源管理器”**中，该服务的名称为 Northwind 并带有扩展名 .svc.cs 或 .svc.vb。  
  
4.  在数据服务的代码中，用数据模型的实体容器的类型（在此示例中为 `NorthwindEntities`）替换定义数据服务的类定义中的注释 `/* TODO: put your data source class name here */`。  该类定义应如下所示：  
  
     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]  
  
### 启用对数据服务资源的访问  
  
1.  在数据服务的代码中，用下列代码替换 `InitializeService` 函数中的占位符代码：  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#allreadconfig)]  
  
     这使得授权客户端能够对指定实体集的资源进行读写访问。  
  
    > [!NOTE]
    >  任何可以访问该 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序的客户端也能够访问由数据服务公开的资源。  在生产数据服务中，为防止对资源进行未经授权的访问，还应保护应用程序本身的安全。  有关详细信息，请参阅[WCF 数据服务的安全](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)。  
  
## 后续步骤  
 您已经成功地创建了一个公开基于 Northwind 示例数据库的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的新数据服务，并且已经为具有 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序的相应权限的客户端启用对该源的访问权。  接下来，将从 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 启动数据服务，并通过 Web 浏览器提交 HTTP GET 请求来访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源：  
  
 [从 Web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)  
  
## 请参阅  
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)