---
title: "将数据作为服务公开（WCF 数据服务） | Microsoft Docs"
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
  - "入门, WCF 数据服务"
  - "WCF 数据服务, 配置"
  - "WCF 数据服务, 入门"
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 将数据作为服务公开（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]与 Visual Studio 集成，使您可以更轻松地将服务定义为作为[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源公开数据。  创建一个用于公开 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的数据服务涉及以下基本步骤：  
  
1.  **定义** **数据模型**。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 本身支持基于 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)的数据模型。  有关详细信息，请参阅[如何：使用 ADO.NET 实体框架数据源创建数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-an-adonet-ef-data-wcf.md)。  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 还支持基于公共语言运行时 \(CLR\) 对象的数据模型，这些对象返回 <xref:System.Linq.IQueryable%601> 接口的实例。  这使您能够部署基于 .NET Framework 中的列表、数组和集合的数据服务。若要启用对这些数据结构的创建、更新和删除操作，还必须实现 <xref:System.Data.Services.IUpdatable> 接口。  有关详细信息，请参阅[如何：使用反射提供程序创建数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)。  
  
     对于更高级的方案，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]包括一组提供程序，用于基于后期绑定数据类型定义数据模型。  有关详细信息，请参阅[自定义数据服务提供程序](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)。  
  
2.  **创建数据服务。** 大多数基本数据服务公开一个从 <xref:System.Data.Services.DataService%601> 类继承的类和一个作为实体容器的命名空间限定名称的 `T` 类型。  有关详细信息，请参阅[定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)。  
  
3.  **配置数据服务。** 默认情况下，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 禁用对由实体容器公开的资源的访问。<xref:System.Data.Services.DataServiceConfiguration> 接口可用于配置对资源和服务操作的访问，指定受支持的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 版本，以及定义其他服务范围的行为，如批处理行为或可在单个响应中返回的最大实体数量。有关更多信息，请参见[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。  
  
 有关如何创建基于 Northwind 示例数据库的简单数据服务的示例，请参见[快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)。  
  
## 请参阅  
 [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)   
 [概述](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)