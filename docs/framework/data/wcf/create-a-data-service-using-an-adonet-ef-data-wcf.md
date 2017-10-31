---
title: "如何：使用 ADO.NET 实体框架数据源创建数据服务（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 实体框架"
  - "WCF 数据服务, 提供程序"
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 如何：使用 ADO.NET 实体框架数据源创建数据服务（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 将实体数据作为数据服务公开。  如果数据源为关系数据库，则此实体数据是由 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]提供的。  本主题介绍如何在基于现有数据库的 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Web 应用程序中创建基于[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]的数据模型，以及如何使用此数据模型创建新的数据服务。  
  
 [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]还提供了一个可以在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 项目外部生成[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]模型的命令行工具。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  
  
### 将基于现有数据库的实体框架模型添加到现有 Web 应用程序  
  
1.  在**“项目”**菜单上单击**“添加新项”**。  
  
2.  在**“模板”**窗格中，单击**“数据”**类别，然后选择**“ADO.NET 实体数据模型”**。  
  
3.  键入模型名称，然后单击**“添加”**。  
  
     将显示“[!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)]向导”的第一页。  
  
4.  在**“选择模型内容”**对话框中，选择**“从数据库生成”**。  然后，单击**“下一步”**。  
  
5.  单击**“新建连接”**按钮。  
  
6.  在**“连接属性”**对话框中，键入服务器名称，选择身份验证方法，键入数据库名称，然后单击**“确定”**。  
  
     **“选择您的数据连接”**对话框将以您的数据库连接设置更新。  
  
7.  确保选中**“将 App.Config 中的实体连接设置另存为:”**复选框。  然后，单击**“下一步”**。  
  
8.  在**“选择数据库对象”**对话框中，选择计划在数据服务中公开的所有数据库对象。  
  
    > [!NOTE]
    >  数据服务不自动公开数据模型中包含的对象。  它们必须由服务本身显式公开。  有关详细信息，请参阅[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。  
  
9. 单击**“完成”**以完成该向导。  
  
     这将基于特定数据库创建默认数据模型。  [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]允许对数据模型进行自定义。  有关详细信息，请参阅[Tasks](http://msdn.microsoft.com/zh-cn/7166f1f1-4de8-4bd4-86b5-5e20a2ebaccb)。  
  
### 使用新数据模型创建数据服务  
  
1.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中，打开代表数据模型的 .edmx 文件。  
  
2.  在**“模型浏览器”**中，右击模型，单击**“属性”**，然后记下实体容器的名称。  
  
3.  在**“解决方案资源管理器”**中，右击 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目的名称，然后单击**“添加新项”**。  
  
4.  在**“添加新项”**对话框中，选择**“WCF 数据服务”**。  
  
5.  指定服务的名称，然后单击**“确定”**。  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 将为新服务创建 XML 标记和代码文件。  默认情况下，代码编辑器窗口将打开。  
  
6.  在数据服务代码中，将用于定义数据服务的类定义中的注释 `/* TODO: put your data source class name here */` 替换为从 <xref:System.Data.Objects.ObjectContext> 类继承且作为数据模型的实体容器的类型，如步骤 2 中所述。  
  
7.  在数据服务代码中，启用经过授权的客户端来访问数据服务公开的实体集。  有关详细信息，请参阅[创建数据服务](../../../../docs/framework/data/wcf/creating-the-data-service.md)。  
  
8.  若要使用 Web 浏览器测试 Northwind.svc 数据服务，请按照[从 Web 浏览器访问服务](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)主题中的说明操作。  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)   
 [如何：使用反射提供程序创建数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)   
 [如何：使用 LINQ to SQL 数据源创建数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-linq-to-sql-wcf.md)