---
title: "如何：定义服务操作（WCF 数据服务） | Microsoft Docs"
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
  - "服务操作 [WCF 数据服务]"
  - "WCF 数据服务, 服务操作"
ms.assetid: dfcd3cb1-2f07-4d0b-b16a-6b056c4f45fa
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：定义服务操作（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 公开在服务器上作为服务操作定义的方法。  服务操作允许数据服务通过 URI 提供对服务器上定义的方法的访问。  若要定义服务操作，请对方法应用 \[`WebGet]` 或 `[WebInvoke]` 特性。  若要支持查询运算符，服务操作必须返回一个 <xref:System.Linq.IQueryable%601> 实例。  服务操作可以通过 <xref:System.Data.Services.DataService%601> 的 <xref:System.Data.Services.DataService%601.CurrentDataSource%2A> 属性访问基础数据源。有关更多信息，请参见[服务操作](../../../../docs/framework/data/wcf/service-operations-wcf-data-services.md)。  
  
 本主题中的示例定义一个名为 `GetOrdersByCity` 的服务操作，该操作返回 `Orders` 和相关 `Order_Details` 对象的经筛选后的 <xref:System.Linq.IQueryable%601> 实例。  该示例访问作为 Northwind 示例数据服务数据源的 <xref:System.Data.Objects.ObjectContext> 实例。  此服务是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
### 在 Northwind 数据服务中定义服务操作  
  
1.  在 Northwind 数据服务项目中，打开 Northwind.svc 文件。  
  
2.  在 `Northwind` 类中，定义一个名为 `GetOrdersByCity` 的服务操作方法，如下所示：  
  
     [!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationdef)]
     [!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationdef)]  
  
3.  在 `Northwind` 类的 `InitializeService` 方法中，添加以下代码以支持对服务操作的访问：  
  
     [!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationconfig)]
     [!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationconfig)]  
  
### 查询 GetOrdersByCity 服务操作  
  
-   在 Web 浏览器中，输入以下 URI 之一以调用在以下示例中定义的服务操作：  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'`  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$top=2`  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc`  
  
## 示例  
 以下示例对 Northwind 数据服务实现一个名为 `GetOrderByCity` 的服务操作。  此操作根据提供的城市名称使用 ADO.NET 实体框架返回一组 `Orders` 和相关 `Order_Details` 对象，以作为 <xref:System.Linq.IQueryable%601> 实例。  
  
> [!NOTE]
>  由于此方法返回了一个 <xref:System.Linq.IQueryable%601> 实例，因此该服务操作终结点支持查询运算符。  
  
 [!code-csharp[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperation)]
 [!code-vb[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperation)]  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)