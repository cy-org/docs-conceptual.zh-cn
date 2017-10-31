---
title: "如何：添加、修改和删除实体（WCF 数据服务） | Microsoft Docs"
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
ms.assetid: a00f8933-b232-4445-95ba-adc634f055d8
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：添加、修改和删除实体（WCF 数据服务）
使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库，通过对 <xref:System.Data.Services.Client.DataServiceContext> 中的对象执行等效操作，可以创建、更新和删除数据服务中的实体数据。  有关详细信息，请参阅[更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例创建一个新的对象实例，然后对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 方法以创建上下文中的项。  调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，HTTP POST 消息将会发送到数据服务。  
  
 [!code-csharp[Astoria Northwind Client#AddProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addproduct)]
 [!code-vb[Astoria Northwind Client#AddProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addproduct)]  
  
## 示例  
 下面的示例检索和修改现有的对象，然后对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> 方法以将上下文中的项标记为已更新。  调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，HTTP MERGE 消息将会发送到数据服务。  
  
 [!code-csharp[Astoria Northwind Client#ModifyCustomer](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#modifycustomer)]
 [!code-vb[Astoria Northwind Client#ModifyCustomer](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#modifycustomer)]  
  
## 示例  
 下面的示例对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 方法以将上下文中的项标记为删除。  调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，HTTP DELETE 消息将会发送到数据服务。  
  
 [!code-csharp[Astoria Northwind Client#DeleteProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#deleteproduct)]
 [!code-vb[Astoria Northwind Client#DeleteProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#deleteproduct)]  
  
## 示例  
 下面的示例创建一个新的对象实例，然后对 <xref:System.Data.Services.Client.DataServiceContext> 调用 <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> 方法以创建上下文中的项以及指向相关订单的链接。  调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，HTTP POST 消息将会发送到数据服务。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addorderdetailtoorderauto)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addorderdetailtoorderauto)]  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [如何：将现有实体附加到 DataServiceContext 中](../../../../docs/framework/data/wcf/attach-an-existing-entity-to-dc-wcf-data.md)   
 [如何：定义实体关系](../../../../docs/framework/data/wcf/how-to-define-entity-relationships-wcf-data-services.md)   
 [批处理操作](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)