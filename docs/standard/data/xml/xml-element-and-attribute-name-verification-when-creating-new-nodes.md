---
title: "创建新节点时的 XML 元素和属性名验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b489f647-a175-4659-ada4-170058bb41d0
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# 创建新节点时的 XML 元素和属性名验证
XML 文档对象模型 \(DOM\) 在创建新元素节点或属性节点时检查名称的有效性。  如果名称包含非法字符，则将引发异常。  若要确保名称有效且编码正确，需要使用 **XmlConvert** 类在应用程序级别对该名称进行编码和解码。  **XmlWriter** 具有执行附加操作以确保生成格式正确的 XML 的方法。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)