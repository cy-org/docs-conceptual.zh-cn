---
title: "对 JSON 和其他数据传输格式的支持 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a527f1be-4e37-4beb-9a95-291480d19627
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 对 JSON 和其他数据传输格式的支持
JSON（JavaScript 对象符号）是一种高效的数据编码格式，可用于在客户端浏览器和支持 AJAX（异步 JavaScript 和 XML）的 Web 服务之间快速交换少量数据。  
  
## 本节内容  
 [独立 JSON 序列化](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)  
 描述独立 JSON 序列化。  
  
 [如何：对 JSON 数据进行序列化和反序列化](../../../../docs/framework/wcf/feature-details/how-to-serialize-and-deserialize-json-data.md)  
 演示如何使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 将 .NET 类型对象序列化为 JSON 编码数据，然后将 JSON 格式的数据反序列化回 .NET 类型的实例。  
  
 [JSON 和 XML 之间的映射](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md)  
 描述 JavaScript 对象符号 \(JSON\) 编码和 XML infoset 之间的对应关系，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 在内部使用这种对应关系来表示 JSON 编码数据和文档。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>   
 <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>