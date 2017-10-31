---
title: "如何：截获数据服务消息（WCF 数据服务） | Microsoft Docs"
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
  - "查询侦听器 [WCF 数据服务]"
  - "WCF 数据服务, 自定义"
ms.assetid: 24b9df1b-b54b-4795-a033-edf333675de6
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：截获数据服务消息（WCF 数据服务）
使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 可以截获请求消息，以便可以向操作添加自定义逻辑。  若要截获消息，请使用数据服务中的专门特性化的方法。  有关详细信息，请参阅[侦听器](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md)。  
  
 本主题中的示例使用 Northwind 示例数据服务。  此服务是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
### 为 Orders 实体集定义查询侦听器  
  
1.  在 Northwind 数据服务项目中，打开 Northwind.svc 文件。  
  
2.  在 `Northwind` 类的代码页中，添加以下 `using` 语句（在 Visual Basic 中为 `Imports`）。  
  
     [!code-csharp[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#usinglinqexpressions)]
     [!code-vb[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#usinglinqexpressions)]  
  
3.  在 `Northwind` 类中，定义一个名为 `OnQueryOrders` 的服务操作方法，如下所示：  
  
     [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptordef)]
     [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
### 为 Products 实体集定义变更侦听器  
  
1.  在 Northwind 数据服务项目中，打开 Northwind.svc 文件。  
  
2.  在 `Northwind` 类中，定义一个名为 `OnChangeProducts` 的服务操作方法，如下所示：  
  
     [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptordef)]
     [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
## 示例  
 下面的示例为 `Orders` 实体集定义一个返回 lambda 表达式的查询侦听器方法。  此表达式包含一个委托，该委托基于具有特定联系人姓名的相关 `Customers` 筛选所请求的 `Orders`。  该姓名反过来又由请求的用户确定。  此示例假定数据服务承载在使用 WCF 的 ASP.NET Web 应用程序中，并且已启用身份验证。  <xref:System.Web.HttpContext> 类用于检索当前请求的原则。  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptor)]
 [!code-vb[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptor)]  
  
## 示例  
 下面的示例为 `Products` 实体集定义变更侦听器方法。  此方法验证对该服务的 <xref:System.Data.Services.UpdateOperations> 或 <xref:System.Data.Services.UpdateOperations> 操作的输入，如果对断货的产品进行更改，则会引发异常。  此方法还将删除产品操作视为不支持的操作，从而阻止这一操作。  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptor)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptor)]  
  
## 请参阅  
 [如何：定义服务操作](../../../../docs/framework/data/wcf/how-to-define-a-service-operation-wcf-data-services.md)   
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)