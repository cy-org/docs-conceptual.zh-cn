---
title: "XmlSerializerOperationBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8911aa1b-e34b-4161-a3ae-7468d89a6861
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# XmlSerializerOperationBehavior
XmlSerializerOperationBehavior  
  
## 语法  
  
```  
class XmlSerializerOperationBehavior : Behavior  
{  
  string Style;  
  string Use;  
};  
```  
  
## 方法  
 XmlSerializerOperationBehavior 类不定义任何方法。  
  
## 属性  
 XmlSerializerOperationBehavior 类具有下列属性：  
  
### Style  
 数据类型：String  
  
 访问类型：只读  
  
 定义 SOAP 消息的样式。  
  
### Use  
 数据类型：String  
  
 访问类型：只读  
  
 指定 SOAP 编码样式。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>