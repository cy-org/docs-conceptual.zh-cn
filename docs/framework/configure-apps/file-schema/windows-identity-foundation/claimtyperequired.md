---
title: "&lt;claimTypeRequired&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c469d71f-6c77-4a24-97aa-53efa126ceef
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;claimTypeRequired&gt;
指定所需的传入安全令牌的报销申请的一组。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <claimTypeRequired>  
    </claimTypeRequired>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<claimType\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimtype.md)|指定一个可选或必需当时传入安全令牌。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定的服务级别标识设置。|