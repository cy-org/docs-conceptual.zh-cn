---
title: "如何：执行异步数据服务查询（WCF 数据服务） | Microsoft Docs"
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
  - "异步操作 [WCF 数据服务]"
  - "WCF 数据服务, 异步操作"
ms.assetid: 902a2dc1-d0e9-4b00-90a8-becc4cb1f6a7
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：执行异步数据服务查询（WCF 数据服务）
通过使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库，您可异步执行客户端\-服务器操作，例如执行查询和保存更改。有关更多信息，请参见[异步操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)。  
  
> [!NOTE]
>  对于必须在特定线程中调用回调的应用程序，必须显式封送 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法的执行。  有关详细信息，请参阅[异步操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的示例显示如何通过调用 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 方法以启动查询来执行异步查询。  内联委托调用 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法以显示查询结果。  
  
 [!code-csharp[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#executequeryasync)]
 [!code-vb[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#executequeryasync)]  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)