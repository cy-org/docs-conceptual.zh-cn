---
title: "如何：启用对数据服务的访问（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 配置"
ms.assetid: 3d830bcd-32b4-4f26-9287-d58a071452c6
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 如何：启用对数据服务的访问（WCF 数据服务）
在 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]中，您必须显式授予对数据服务公开的资源的访问权限。  这意味着您在创建新的数据服务之后，仍必须显式提供对实体集形式的各个资源的访问。  本主题演示如何允许对 Northwind 数据服务中的五个实体集进行读和写访问，该服务在您完成 [quickstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) 时创建。因为 <xref:System.Data.Services.EntitySetRights> 枚举通过使用 <xref:System.FlagsAttribute> 定义，您可以使用逻辑 OR 运算符来指定一个实体集的多个权限。  
  
> [!NOTE]
>  任何可以访问该 ASP.NET 应用程序的客户端也能够访问由数据服务公开的资源。  在生产数据服务中，为防止对资源进行未经授权的访问，还应保护应用程序本身的安全。  有关详细信息，请参阅[NIB: ASP.NET Security](http://msdn.microsoft.com/zh-cn/04b37532-18d9-40b4-8e5f-ee09a70b311d)。  
  
### 启用对数据服务的访问  
  
-   在数据服务的代码中，用下列代码替换 `InitializeService` 函数中的占位符代码：  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#allreadconfig)]  
  
     这使得客户端能够对 `Orders` 和 `Order_Details` 实体集进行读写访问，以及对 `Customers` 实体集进行只读访问。  
  
## 请参阅  
 [如何：开发在 IIS 上运行的 WCF 数据服务](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)   
 [配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)