---
title: "&lt;serviceAuthenticationManager&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5d69e64f-f325-4d55-8e2d-0fb30f222dda
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;serviceAuthenticationManager&gt;
提供一个工作流配置元素，该元素在服务级别建立传输、消息或发起方的有效性。  
  
## 语法  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <serviceAuthenticationManager serviceAuthenticationManagerType =”String”/>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|serviceAuthenticationManagerType|一个字符串，指定当前行为的身份验证策略类型。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行为元素。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ServiceAuthenticationElement>