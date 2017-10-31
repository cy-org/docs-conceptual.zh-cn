---
title: "如何：在批处理中执行查询（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 批处理请求"
ms.assetid: 3b4db7df-bd33-43a1-8ea4-63a18e131f97
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：在批处理中执行查询（WCF 数据服务）
通过使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库，可以在单个批处理中对数据服务执行多个查询。  有关详细信息，请参阅[批处理操作](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例演示如何调用 <xref:Microsoft.SqlServer.ReportingServices.ReportingService.ExecuteBatch%2A> 方法来执行一个 <xref:System.Data.Services.Client.DataServiceRequest%601> 对象数组，该数组包含从 Northwind 数据服务同时返回 `Customers` 和 `Products` 对象的查询。  此示例将枚举返回的 <xref:System.Data.Services.Client.DataServiceResponse> 中的 <xref:System.Data.Services.Client.QueryOperationResponse%601> 对象的集合，并且还会枚举每个 <xref:System.Data.Services.Client.QueryOperationResponse%601> 中包含的对象的集合。  
  
 [!code-csharp[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#batchquery)]
 [!code-vb[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#batchquery)]  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)