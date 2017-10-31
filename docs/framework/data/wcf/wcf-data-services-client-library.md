---
title: "WCF 数据服务客户端库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "HTML"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "DataServiceContext 类, 关于 DataServiceContext 类"
  - "DataServiceQuery 类, 关于 DataServiceQuery 类"
  - "WCF 数据服务, 客户端库"
ms.assetid: 21075e50-8917-413e-a8ea-35a0f6e65aa5
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# WCF 数据服务客户端库
任何应用程序都可与基于[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 的数据服务交互，前提是该应用程序可以发送 HTTP 请求并处理数据服务返回的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。通过这种互操作性，您可以从广泛范围的 Web 应用程序来访问基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的服务。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]包括多个客户端库，当从基于 .NET Framework 或 Silverlight 的应用程序使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源时，这些客户端库提供更丰富的编程体验。  
  
 客户端库的两大主要类为 <xref:System.Data.Services.Client.DataServiceContext> 类和 <xref:System.Data.Services.Client.DataServiceQuery%601> 类。  <xref:System.Data.Services.Client.DataServiceContext> 类封装针对指定数据服务支持的操作。  尽管 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务是无状态的，但上下文不是。  因此，可使用 <xref:System.Data.Services.Client.DataServiceContext> 类在数据服务的各个交互之间保持客户端的状态，以支持诸如更改管理之类的功能。  该类还对更改的标识和跟踪进行管理。  <xref:System.Data.Services.Client.DataServiceQuery%601> 类表示一个针对特定实体集的查询。  
  
 本节介绍如何使用客户端库从 .NET Framework 客户端应用程序访问和更改数据。  有关如何结合使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库与基于 Silverlight 的应用程序的更多信息，请参见 [WCF 数据服务 \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkId=186016)（可能为英文网页）。  您还可使用其他客户端库在其他类型的应用程序中使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  有关更多信息，请参见 [OData SDK](http://go.microsoft.com/fwlink/?LinkID=185796)。  
  
## 本节内容  
 [生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)  
 介绍如何生成基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的客户端库和客户端数据服务类。  
  
 [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
 介绍如何使用客户端库从基于 .NET Framework 的应用程序查询数据服务。  
  
 [加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)  
 介绍如何加载未包含在初始查询响应中的附加内容。  
  
 [更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)  
 介绍如何使用客户端库来创建、修改和删除实体和关系。  
  
 [异步操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)  
 介绍客户端库提供的用于以异步方式使用数据服务的功能。  
  
 [批处理操作](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)  
 介绍如何使用客户端库在一个批处理中向数据服务发送多个请求。  
  
 [将数据绑定到控件](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)  
 介绍如何将控件绑定到数据服务返回的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
 [调用服务操作](../../../../docs/framework/data/wcf/calling-service-operations-wcf-data-services.md)  
 介绍如何使用客户端库调用服务操作。  
  
 [管理数据服务上下文](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)  
 介绍用于管理客户端库的行为的选项。  
  
 [使用二进制数据](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)  
 介绍如何访问和更改数据服务作为数据流返回的二进制数据。  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)