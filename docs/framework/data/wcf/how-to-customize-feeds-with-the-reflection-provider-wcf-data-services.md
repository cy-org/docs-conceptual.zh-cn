---
title: "如何：使用反射提供程序自定义源（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务, 自定义"
  - "WCF 数据服务, 自定义源"
ms.assetid: 00c23dcf-9bb8-459a-a012-6c4d9bcad7e9
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：使用反射提供程序自定义源（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 使您可以在数据服务响应中自定义 Atom 序列化，以便可以将实体属性映射到在 AtomPub 协议中定义的未使用的元素。  本主题演示如何为使用反射提供程序定义的数据模型中的实体类型定义映射特性。  有关详细信息，请参阅[源自定义](../../../../docs/framework/data/wcf/feed-customization-wcf-data-services.md)。  
  
 [如何：使用反射提供程序创建数据服务](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md) 主题中解释了此示例的数据模型  
  
## 示例  
 在以下示例中，`Order` 类型的两个属性均映射到现有的 Atom 元素。  `Item` 类型的 `Product` 属性映射到单独的命名空间中的自定义源特性。  
  
 [!code-csharp[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria custom feeds/cs/orderitems.svc.cs#customiqueryablefeeds)]
 [!code-vb[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria custom feeds/vb/orderitems.svc.vb#customiqueryablefeeds)]  
  
## 示例  
 上面的示例为 URI `http://myservice/OrderItems.svc/Orders(0)?$expand=Items` 返回以下结果。  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResultInline](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria custom feeds/xml/iqueryablefeedresultinline.xml#iqueryablefeedresultinline)]  
  
## 请参阅  
 [反射提供程序](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md)