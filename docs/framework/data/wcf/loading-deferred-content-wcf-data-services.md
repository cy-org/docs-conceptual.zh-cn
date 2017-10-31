---
title: "加载延迟的内容（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 客户端库"
  - "WCF 数据服务, 延迟的内容"
  - "WCF 数据服务, 加载数据"
ms.assetid: 32f9b588-c832-44c4-a7e0-fcce635df59a
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 加载延迟的内容（WCF 数据服务）
默认情况下，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 会限制查询返回的数据量。  不过，如果需要，您可以从该数据服务显式加载其他数据，包括相关实体、分页响应数据以及二进制数据流。  本主题介绍如何将这种延迟的内容加载到应用程序。  
  
## 相关实体  
 执行查询时，仅返回所处理实体集中的实体。  例如，当针对 Northwind 数据服务的某个查询返回 `Customers` 实体时，默认情况下不会返回相关的 `Orders` 实体，即使 `Customers` 和 `Orders` 之间存在关系也是如此。  此外，如果数据服务中启用了分页，则必须从该服务显式加载后续数据页。  可通过以下两种方法来加载相关实体：  
  
-   **预先加载**：您可以使用 `$expand` 查询选项来请求查询返回由于与查询所请求的实体集的关联而相关的实体。  使用 <xref:System.Data.Services.Client.DataServiceQuery%601> 的 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 方法将 `$expand` 选项添加到发送给数据服务的查询。  可以请求多个相关的实体集，方法是用逗号分隔它们，如下面的示例所示。  查询请求的所有实体均在单个响应中返回。  下面的示例将返回 `Orders` 以及 `Order_Details` 和 `Customers` 实体集：  
  
     [!code-csharp[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#expandorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#expandorderdetailsspecific)]  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]将实体集数量限制为 12，这是可通过使用 `$expand` 查询选项包括在单个查询中的数量。  
  
-   **显式加载**：您可以对 <xref:System.Data.Services.Client.DataServiceContext> 实例调用 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 方法来显式加载相关实体。  每次调用 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 方法都会创建一个对数据服务的单独请求。  下面的示例为 `Orders` 实体显式加载 `Order_Details`：  
  
     [!code-csharp[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#loadrelatedorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#loadrelatedorderdetailsspecific)]  
  
 在考虑要使用哪个选项时，请注意在对数据服务的请求数与单个响应中返回的数据量之间进行权衡。  如果您的应用程序需要关联的对象，并且您希望避免因显式检索这些对象的额外请求而导致延迟增加，请使用预先加载。  不过，如果应用程序仅需要特定相关实体实例的数据，则应考虑通过调用 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 方法显式加载这些实体。  有关详细信息，请参阅[如何：加载相关实体](../../../../docs/framework/data/wcf/how-to-load-related-entities-wcf-data-services.md)。  
  
## 分页内容  
 如果在数据服务中启用了分页，则数据服务返回的源中的项数受数据服务的配置的限制。  可以为每个实体集单独设置页限制。  有关详细信息，请参阅[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。  启用分页后，源中的最后一项包含指向下一页数据的链接。  此链接包含在一个 <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> 对象中。  通过对执行 <xref:System.Data.Services.Client.DataServiceQuery%601> 时返回的 <xref:System.Data.Services.Client.QueryOperationResponse%601> 调用 <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 方法可以获取指向下一页数据的 URI。  然后，使用返回的 <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> 对象加载下一页结果。  必须先枚举查询结果，然后再调用 <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 方法。  请考虑使用 `do…while` 循环首先枚举查询结果，然后再检查 `non-null` 下一个链接值。  如果 <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 方法返回 `null`（在 Visual Basic 中为 `Nothing`），则表示原始查询没有任何其他结果页。  下面的示例所演示的 `do…while` 循环从 Northwind 示例数据服务中加载分页的客户数据。  
  
 [!code-csharp[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#loadnextlink)]
 [!code-vb[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#loadnextlink)]  
  
 如果某个查询请求在单个响应中与所请求的实体集一起返回相关的实体，则分页限制可能会影响以内联形式包含在该响应中的嵌套源。  例如，如果在 Northwind 示例数据服务中为 `Customers` 实体集设置了分页限制，则还可以为相关的 `Orders` 实体集设置单独的分页限制，如下面来自定义 Northwind 示例数据服务的 Northwind.svc.cs 文件的示例所示。  
  
 [!code-csharp[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind.svc.cs#dataserviceconfigpaging)]
 [!code-vb[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind.svc.vb#dataserviceconfigpaging)]  
  
 在这种情况下，必须同时为顶级 `Customers` 和嵌套的 `Orders` 实体源实现分页。  下面的示例所演示的 `while` 循环用于加载与所选 `Customers` 实体相关的 `Orders` 实体的页。  
  
 [!code-csharp[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#loadnextorderslink)]
 [!code-vb[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#loadnextorderslink)]  
  
 有关详细信息，请参阅[如何：加载分页结果](../../../../docs/framework/data/wcf/how-to-load-paged-results-wcf-data-services.md)。  
  
## 二进制数据流  
 通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 能以数据流形式访问二进制大型对象 \(BLOB\) 数据。  流式处理会将对二进制数据的加载推迟到需要时再加载，并且客户端可以更有效地处理此数据。  为了利用此功能，数据服务必须实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 提供程序。  有关详细信息，请参阅[流提供程序](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)。  启用流式处理后，会在没有相关二进制数据的情况下返回实体类型。  在这种情况下，必须使用 <xref:System.Data.Services.Client.DataServiceContext> 类的 <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> 方法从服务访问二进制数据的数据流。  同样，使用 <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 方法可以作为流添加或更改实体的二进制数据。  有关详细信息，请参阅[使用二进制数据](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)