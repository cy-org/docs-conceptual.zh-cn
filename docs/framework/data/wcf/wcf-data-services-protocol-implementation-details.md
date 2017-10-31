---
title: "WCF 数据服务协议实现详细信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 712d689b-fada-4cbb-bcdb-d65a3ef83b4c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# WCF 数据服务协议实现详细信息
## OData 协议实现详细信息  
 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 要求实现协议的数据服务提供某个最小功能集。  这些功能在协议文档中用“应该”和“必须”描述。其他可选功能用“可能”描述。本主题介绍了 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 当前未实现的这些可选功能。  有关更多信息，请参见 [OData 协议文档](http://go.microsoft.com/fwlink/?LinkID=184554)（可能为英文网页）。  
  
### 对 $format 查询选项的支持  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议支持 JavaScript 表示法 \(JSON\) 和 Atom 源，并且 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 提供 `$format` 系统查询选项来允许客户端请求响应源的格式。  此系统查询选项（如果数据服务支持）必须重写请求的 Accept 标头的值。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]支持返回 JSON 和 Atom 源。  但是，默认实现不支持 `$format` 查询选项，它只使用 Accept 标头的值来确定响应的格式。  某些情况下，您的数据服务可能需要支持 `$format` 查询选项，例如，当客户端不能设置 Accept 标头时。  为支持这些情况，您必须扩展您的数据服务以在 URI 中处理此选项。  可以通过以下方法将此功能添加到数据服务：从 MSDN 代码库网站下载 [JSONP 和 URL 控制的格式（该格式支持 ADO.NET Data Services）](http://go.microsoft.com/fwlink/?LinkId=208228)（可能为英文网页）示例项目，并将其添加到数据服务项目。  此示例删除 `$format` 查询选项并将 Accept 标头更改为 `application/json`。  当您包含此示例项目并将 `JSONPSupportBehaviorAttribute` 添加到您的数据服务类时，将允许服务处理 `$format` 查询选项 `$format=json`。  需要进一步自定义此示例项目以处理 `$format=atom` 或其他自定义格式。  
  
## WCF 数据服务行为  
 以下 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]行为未显式由 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议定义：  
  
### 默认排序行为  
 当发送到数据服务的查询请求包括 `$top` 或 `$skip` 系统查询选项但不包括 `$orderby` 系统查询选项时，返回的源按键属性升序排序。  这是因为需要顺序以确保结果正确分页。  为此，数据服务向查询中添加排序表达式。  在数据服务中启用服务器驱动的分页时，也会发生此行为。  有关更多信息，请参见[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。要控制返回的源的顺序，应在查询 URI 中包括 `$orderby`。  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)