---
title: "如何：加载分页结果（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 延迟的内容"
  - "WCF 数据服务, 加载数据"
ms.assetid: bb786ea4-f3ef-4ad3-9a41-3a0b7feb6a1f
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：加载分页结果（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 允许数据服务限制单个响应源中返回的实体数。  在此情况下，源中的最后一项包含指向下一页数据的链接。  通过调用 <xref:System.Data.Services.Client.QueryOperationResponse%601>（在执行 <xref:System.Data.Services.Client.DataServiceQuery%601> 时返回）的 <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 方法，获取数据的下一页的 URI。然后使用此对象表示的 URI 加载结果的下一页。  有关详细信息，请参阅[加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例使用 `do…while` 循环从数据服务的分页结果中加载 `Customers` 实体。  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getcustomerspaged)]
 [!code-vb[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getcustomerspaged)]  
  
## 示例  
 下面的示例返回每个 `Customers` 实体的相关 `Orders` 实体，并使用  循环从数据服务中加载 `Customers` 实体页以及使用嵌套的 `while` 循环从数据服务中加载相关的 `Orders` 实体的页。  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getcustomerspagednested)]
 [!code-vb[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getcustomerspagednested)]  
  
## 请参阅  
 [加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)   
 [如何：加载相关实体](../../../../docs/framework/data/wcf/how-to-load-related-entities-wcf-data-services.md)