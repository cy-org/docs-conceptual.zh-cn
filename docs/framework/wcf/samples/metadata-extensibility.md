---
title: "元数据可扩展性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f92fcc76-0806-4c84-9d63-7aae0d3899de
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 元数据可扩展性
本节包含演示自定义元数据的示例。  
  
## 本节内容  
 [自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)  
 演示如何实现一个具有安全元数据终结点（使用非元数据交换绑定之一）的服务，以及如何配置 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 或客户端以从此类元数据终结点中获取元数据。  
  
 [自定义 WSDL 发布](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md)  
 演示如何在自定义 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> 特性上实现 <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=fullName>，以便在其他功能中将该特性的属性导出为 WSDL 批注。