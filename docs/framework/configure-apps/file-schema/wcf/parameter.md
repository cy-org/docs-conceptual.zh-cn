---
title: "&lt;参数&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;参数&gt;
指定当声明类型是泛型类型时的泛型参数。  
  
## 语法  
  
```  
  
<parameter index="integer"  
                      type=String" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|索引|当声明类型是泛型类型时，指定将返回已知类型的泛型参数。|  
|类型|一个字符串，描述用于序列化和反序列化的已知类型。|  
  
## index 特性  
  
|值|描述|  
|-------|--------|  
|"0"|泛型类型中的第一个参数。  例如，一个 <xref:System.Collections.Generic.List%601> 仅有一个参数。  如果此参数用作声明类型，则将 index 特性设置为“0”。|  
|"1"|泛型类型中的第二个参数。  例如，一个 <xref:System.Collections.Generic.Dictionary%602> 有两个参数。  如果通过第二个参数返回已知类型，则将 index 特性设置为“1”。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<knownType\>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowntype.md)|指定一个可由声明类型的字段或属性返回的已知类型。|  
  
## 备注  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]已知类型的更多信息，请参见[数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)和 <xref:System.Runtime.Serialization.DataContractSerializer>。  
  
 有关使用此元素的示例，请参见 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)。  
  
 此配置元素不能同时具有两个属性。  如果设置两个属性，则发生 <xref:System.Configuration.ConfigurationErrorsException>。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)   
 [\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)