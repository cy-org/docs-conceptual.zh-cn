---
title: "元数据格式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: baad1e68-28fc-4a6a-8a43-75e47e7fa871
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 元数据格式
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 支持下表中的元数据格式。  
  
## 元数据的规范和用法  
  
|协议|规范和用法|  
|--------|-----------|  
|WSDL 1.1|[Web 服务描述语言 \(WSDL\) 1.1](http://go.microsoft.com/fwlink/?LinkId=94859)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 Web 服务描述语言 \(WSDL\) 描述服务。|  
|XML 架构|[XML 架构第 2 部分：数据类型第二版](http://go.microsoft.com/fwlink/?LinkId=94861)（可能为英文网页）和 [XML 架构第 1 部分：结构第二版](http://go.microsoft.com/fwlink/?LinkId=94862)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 XML 架构描述消息中使用的数据类型。|  
|WS Policy|[Web 服务策略 1.2 \- 框架 \(WS\-Policy\)](http://go.microsoft.com/fwlink/?LinkId=94864)（可能为英文网页）<br /><br /> [Web 服务策略 1.5 \- 框架](http://go.microsoft.com/fwlink/?LinkId=94865)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 WS\-Policy 1.2 或 1.5 规范与特定于域的断言一起使用来描述服务要求和功能。|  
|WS Policy 附件|[Web 服务策略 1.2 \- 附件 \(WS\-PolicyAttachment\)](http://go.microsoft.com/fwlink/?LinkId=94866)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 WS\-Policy 附件以在 WSDL 中的不同范围附加策略表达式。|  
|WS 元数据交换|[Web 服务元数据交换 \(WS\-MetadataExchange\) 1.1 版](http://go.microsoft.com/fwlink/?LinkId=94868)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 WS\-MetadataExchange 以检索 XML 架构、WSDL 和 WS\-Policy。|  
|WSDL 的 WS 寻址绑定|[Web 服务寻址 1.0 \- WSDL 绑定](http://go.microsoft.com/fwlink/?LinkId=94869)（可能为英文网页）<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 WSDL 的 WS\-Addressing 绑定以在 WSDL 中附加寻址信息。|  
  
## 请参阅  
 [系统提供的互操作性绑定支持的 Web 服务协议](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)   
 [WSDL 和策略](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)