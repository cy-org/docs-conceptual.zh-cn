---
title: "创建 .NET Framework 客户端应用程序（WCF 数据服务快速入门） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 创建 .NET Framework 客户端应用程序（WCF 数据服务快速入门）
这是 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 快速入门的最后一项任务。  在此任务中，将向解决方案中添加一个控制台应用程序，并将对[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源的引用添加到此新建的客户端应用程序中，然后使用生成的客户端数据服务类和客户端库从此客户端应用程序访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
> [!NOTE]
>  访问数据源不需要基于 .NET Framework 的客户端应用程序。  使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的任何应用程序组件都可以访问该数据服务。  有关详细信息，请参阅[在客户端应用程序中使用数据服务](../../../../docs/framework/data/wcf/using-a-data-service-in-a-client-application-wcf-data-services.md)。  
  
### 使用 Visual Studio 创建客户端应用程序  
  
1.  在**“解决方案资源管理器”**中，右击解决方案，单击**“添加”**，然后单击**“新建项目”**。  
  
2.  在**“项目类型”**中，单击**“Windows”**，然后在**“模板”**窗格中选择**“WPF 应用程序”**。  
  
3.  输入 `NorthwindClient` 作为项目名称，然后单击**“确定”**。  
  
4.  打开文件 MainWindow.xaml 并用下列代码替换 XAML 代码：  
  
     [!code-xml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml#window1xaml)]  
  
### 在项目中添加数据服务引用  
  
1.  右击“NorthwindClient”项目，单击**“添加服务引用”**，然后单击**“发现”**。  
  
     这将显示在第一个任务中创建的 Northwind 数据服务。  
  
2.  在**“命名空间”**文本框中，键入 `Northwind`，然后单击**“确定”**。  
  
     这将在项目中添加一个新的代码文件，其中包含用于作为对象访问数据服务资源并与其交互的数据类。  这些数据类是在命名空间 `NorthwindClient.Northwind` 中创建的。  
  
### 在 WPF 应用程序中访问数据服务数据  
  
1.  在**“解决方案资源管理器”**中的**“NorthwindClient”**下，右击项目，然后单击**“添加引用”**。  
  
2.  在“添加引用”对话框中，单击**“.NET”**选项卡，选择“System.Data.Services.Client.dll”程序集，然后单击**“确定”**。  在**“解决方案资源管理器”**中的**“NorthwindClient”**下，打开 MainWindow.xaml 文件的代码页，然后添加下列 `using` 语句（在 Visual Basic 中为 `Imports`）。  
  
     [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#using)]
     [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#using)]  
  
3.  将用于查询数据服务并将结果绑定到 <xref:System.Data.Services.Client.DataServiceCollection%601> 的下列代码插入到 `MainWindow` 类：  
  
    > [!NOTE]
    >  必须用承载 Northwind 数据服务的实例的服务器和端口替换主机名 `localhost:12345`。  
  
     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#querycode)]  
  
4.  将用于保存更改的下列代码插入到 `MainWindow` 类：  
  
     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#savechanges)]  
  
### 生成并运行 NorthwindClient 应用程序  
  
1.  在**“解决方案资源管理器”**中，右击“NorthwindClient”项目，然后选择**“设为启动项目”**。  
  
2.  按 F5 键启动该应用程序。  
  
     这将生成解决方案并启动客户端应用程序。  将从服务请求数据并将其显示在控制台中。  
  
3.  编辑数据网格的**“数量”**列中的值，然后单击**“保存”**。  
  
     将更改保存到数据服务。  
  
    > [!NOTE]
    >  此版本的 NorthwindClient 应用程序不支持添加和删除实体。  
  
## 后续步骤  
 您已成功创建了用于访问 Northwind [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 示例源的客户端应用程序。  您还完成了 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 快速入门。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]从 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的更多信息，请参见[WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)。  
  
## 请参阅  
 [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)   
 [资源](../../../../docs/framework/data/wcf/wcf-data-services-resources.md)