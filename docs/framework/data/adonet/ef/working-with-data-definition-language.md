---
title: "使用数据定义语言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec50083d-44f4-4093-9b23-5eacd601f96e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用数据定义语言
从 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 版本 4 开始，[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]支持数据定义语言 \(DDL\)。  这样，您将能够基于连接字符串和存储元数据 \(SSDL\) 模型创建或删除数据库实例。  
  
 <xref:System.Data.Objects.ObjectContext> 的以下方法使用连接字符串和 SSDL 内容来完成以下操作：创建或删除数据库，检查数据库是否存在，以及查看生成的 DDL 脚本：  
  
-   <xref:System.Data.Objects.ObjectContext.CreateDatabase%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.CreateDatabaseScript%2A>  
  
> [!NOTE]
>  假定有足够的权限可执行 DDL 命令。  
  
 以上列出的方法将大部分工作都委托给基础 ADO.NET 数据提供程序。  该提供程序负责确保用于生成数据库对象的命名约定与用于查询和更新的约定保持一致。  
  
 下面的示例演示如何基于现有模型生成数据库。  它还将新的实体对象添加到对象上下文中，然后将该对象保存到数据库中。  
  
## 过程  
  
#### 基于现有模型定义数据库  
  
1.  创建控制台应用程序。  
  
2.  向应用程序中添加现有模型。  
  
    1.  添加一个名为 `SchoolModel` 的空模型。  若要创建空模型，请参见[How to: Create a New .edmx File](http://msdn.microsoft.com/zh-cn/beb8189e-e51c-4051-839c-9902c224abf2)主题。  
  
     将 SchoolModel.edmx 文件添加到您的项目中。  
  
    1.  从 [School Model](http://msdn.microsoft.com/zh-cn/859a9587-81ea-4a45-9bc0-f8d330e1adac)主题中复制 School 模型的概念、存储和映射内容。  
  
    2.  打开 SchoolModel.edmx 文件并将内容粘贴在 `edmx:Runtime` 标记中。  
  
3.  将以下代码添加到主函数中。  此类代码将连接字符串初始化为数据库服务器，查看 DDL 脚本，创建数据库，将新实体添加到上下文，并将更改保存到数据库。  
  
     [!code-csharp[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/csharp/VS_Snippets_Data/DP ObjectServices Concepts/CS/Source.cs#ddl)]
     [!code-vb[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP ObjectServices Concepts/VB/Source.vb#ddl)]