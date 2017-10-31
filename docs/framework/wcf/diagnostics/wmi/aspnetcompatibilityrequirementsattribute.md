---
title: "AspNetCompatibilityRequirementsAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00908a39-a21b-4029-bbb9-33e5a6ed25a7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# AspNetCompatibilityRequirementsAttribute
AspNetCompatibilityRequirementsAttribute  
  
## 语法  
  
```  
class AspNetCompatibilityRequirementsAttribute : Behavior  
{  
  string RequirementsMode;  
};  
```  
  
## 方法  
 AspNetCompatibilityRequirementsAttribute 类不定义任何方法。  
  
## 属性  
 AspNetCompatibilityRequirementsAttribute 类具有以下属性。  
  
### RequirementsMode  
 数据类型：String  
  
 访问类型：只读  
  
 指示 Asp.Net 兼容模式是否处于活动状态。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceHostingEnvironment.AspNetCompatibilityEnabled%2A>