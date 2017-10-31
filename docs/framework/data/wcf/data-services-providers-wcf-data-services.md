---
title: "数据服务提供程序（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 提供程序"
ms.assetid: a0160b1b-3d9c-4cc8-8391-cb0986a60a41
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 数据服务提供程序（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]支持多个用于将数据作为[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源公开的提供程序模型。  本主题提供的信息有助于为数据源选择最佳的 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]提供程序。  
  
## 数据源提供程序  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]支持以下用于定义数据服务的数据模型的提供程序。  
  
|提供程序|描述|  
|----------|--------|  
|实体框架提供程序|该提供程序使用 ADO.NET 实体框架，使您能够通过定义映射到关系数据的数据模型，将关系数据与数据服务一起使用。  数据源可以为 SQL Server 或任何其他通过第三方提供程序支持实体框架的数据源。  如果您拥有关系数据源，例如 SQL Server 数据库，则应使用实体框架提供程序。  有关详细信息，请参阅[实体框架提供程序](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)。|  
|反射提供程序|该提供程序使用反射，使您能够基于可以作为 <xref:System.Linq.IQueryable%601> 接口的实例公开的现有数据类定义数据模型。  更新通过实现 <xref:System.Data.Services.IUpdatable> 接口而启用。  如果拥有在运行时定义的静态数据类，应使用该提供程序，例如由 LINQ to SQL 生成的提供程序或由类型化 DataSet 定义的提供程序。  有关详细信息，请参阅[反射提供程序](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md)。|  
|自定义数据服务提供程序|[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]包括一组提供程序，用于基于后期绑定数据类型动态定义数据模型。  当要公开的数据未知时、当正在设计应用程序时或当实体框架或反射提供程序不足时，应实现这些接口。  有关详细信息，请参阅[自定义数据服务提供程序](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)。|  
  
## 其他数据服务提供程序  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]具有以下附加数据服务提供程序，它可增强通过使用其他提供程序之一定义的数据源的性能。  
  
|提供程序|描述|  
|----------|--------|  
|流提供程序|此提供程序用于使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 公开二进制大型对象数据类型。  流提供程序通过实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 接口而创建。  此提供程序可与任一数据源提供程序一起实现。  有关详细信息，请参阅[流提供程序](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)。|  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)   
 [承载数据服务](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)