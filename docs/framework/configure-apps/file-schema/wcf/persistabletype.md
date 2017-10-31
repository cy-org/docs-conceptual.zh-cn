---
title: "&lt;persistableType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5425fe6-523a-4076-aab4-2c2515b1d830
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;persistableType&gt;
指定所有永久类型。  
  
## 语法  
  
```  
  
<comContracts>  
  <comContract>  
      <persistableTypes>  
         <persistableType id="string"  
            name="string">  
         </persistableType>  
      </persistableTypes>  
  </comContract>  
</comContracts>  
```  
  
## 类型  
 `Type`  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|id|一个必需的属性，包含一个指定持久类型唯一标识符的字符串。|  
|name|一个可选属性，包含一个指定持久类型名称的字符串。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<persistableTypes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistabletypes.md)|一个 `persistableType` 元素集合。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ComPersistableTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ComPersistableTypeElement>   
 [\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)   
 [与 COM\+ 应用程序集成](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [如何：配置 COM\+ 服务设置](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)