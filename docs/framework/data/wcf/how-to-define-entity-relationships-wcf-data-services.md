---
title: "如何：定义实体关系（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 更改数据"
ms.assetid: cc255524-1534-4fae-b83c-250933d5a72b
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：定义实体关系（WCF 数据服务）
在 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 中添加新实体时，不会自动定义新实体和相关实体之间的任何关系。  可创建和更改实体实例之间的关系，以及让客户端库在数据服务中反映这些更改。  有关详细信息，请参阅[更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例创建一个新的对象实例，然后对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> 方法以创建上下文中的项以及指向相关订单的链接。  调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，HTTP POST 消息将会发送到数据服务。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addorderdetailtoorderauto)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addorderdetailtoorderauto)]  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 方法将 `Order_Details` 对象添加到引用特定 `Products` 对象的相关 `Orders` 对象。  <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> 方法定义相应关系。  在此示例中，还显式设置了 `Order_Details` 对象的导航属性。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrder](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addorderdetailtoorder)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrder](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addorderdetailtoorder)]  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [如何：添加、修改和删除实体](../../../../docs/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services.md)