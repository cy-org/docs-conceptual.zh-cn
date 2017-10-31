---
title: "ActivityTransfer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc40ef17-2a92-4ce2-853c-6ba8e5d571f3
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# ActivityTransfer
活动传输事件  
  
## 语法  
  
```  
class ActivityTransfer : WSAT_TraceEvent  
{  
  object ActivityID;  
  object RelatedActivityID;  
};  
```  
  
## 方法  
 ActivityTransfer 类不定义任何方法。  
  
## 属性  
 ActivityTransfer 类具有以下属性：  
  
### ActivityID  
  
-   数据类型：object                   
     访问类型：只读  
  
-   活动 ID  
  
### RelatedActivityID  
  
-   数据类型：object                   
     访问类型：只读  
  
-   相关活动 ID  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义。|