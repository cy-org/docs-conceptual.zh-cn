---
title: "ServiceAppDomain | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f28e5186-a66d-46c1-abe9-b50e07f8cb4f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceAppDomain
将服务映射到应用程序域。  
  
## 语法  
  
```  
class ServiceAppDomain  
{  
  Service ref;  
  AppDomainInfo ref;  
};  
```  
  
## 方法  
 ServiceAppDomain 类不定义任何方法。  
  
## 属性  
 ServiceAppDomain 类具有以下属性：  
  
### ref  
 数据类型：Service               
 限定符：键  
  
 访问类型：只读  
  
 此应用程序域的服务。  
  
### ref  
 数据类型：AppDomainInfo               
 限定符：键  
  
 访问类型：只读  
  
 包含应用程序域的属性。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|