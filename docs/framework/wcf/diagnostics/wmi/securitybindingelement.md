---
title: "SecurityBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef93b6e6-3524-48a8-94d3-c8837f1872f9
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# SecurityBindingElement
SecurityBindingElement  
  
## 语法  
  
```  
class SecurityBindingElement : BindingElement  
{  
  string DefaultAlgorithmSuite;  
  boolean IncludeTimestamp;  
  string KeyEntropyMode;  
  LocalServiceSecuritySettings LocalServiceSecuritySettings;  
  string MessageSecurityVersion;  
  string SecurityHeaderLayout;  
};  
```  
  
## 方法  
 SecurityBindingElement 类未定义任何方法。  
  
## 属性  
 SecurityBindingElement 类具有下列属性：  
  
### DefaultAlgorithmSuite  
 数据类型：String  
  
 访问类型：只读  
  
 指定要用于绑定的算法。  
  
### IncludeTimestamp  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否每个消息都包含时间戳。  
  
### KeyEntropyMode  
 数据类型：String  
  
 访问类型：只读  
  
 用于创建密钥的熵的来源。  
  
### LocalServiceSecuritySettings  
 数据类型：LocalServiceSecuritySettings  
  
 访问类型：只读  
  
 本地服务的特定于绑定的安全属性。  
  
### MessageSecurityVersion  
 数据类型：String  
  
 访问类型：只读  
  
 消息安全使用的版本。  
  
### SecurityHeaderLayout  
 数据类型：String  
  
 访问类型：只读  
  
 此绑定的安全标头中的元素顺序。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>