---
title: "MtomMessageEncodingBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a9c6c3d-e561-4b2d-a693-7e84bdd3534a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# MtomMessageEncodingBindingElement
MtomMessageEncodingBindingElement  
  
## 语法  
  
```  
class MtomMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  string Encoding;  
  sint32 MaxReadPoolSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## 方法  
 MtomMessageEncodingBindingElement 类不定义任何方法。  
  
## 属性  
 MtomMessageEncodingBindingElement 类具有以下属性：  
  
### Encoding  
 数据类型：String  
  
 访问类型：只读  
  
 要用来在绑定上发出消息的字符集编码。  
  
### MaxReadPoolSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 一个整数，指定在无需分配新读取器的情况下可以同时读取的消息数。  
  
### MaxWritePoolSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 一个整数，指定在无需分配新编写器的情况下可以同时发送的消息数。  
  
### ReaderQuotas  
 数据类型：XmlDictionaryReaderQuotas  
  
 访问类型：只读  
  
 读取器的配额。  
  
## 要求  
  
|MOF|在 Servicemodel.mof 中声明。|  
|---------|-----------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>