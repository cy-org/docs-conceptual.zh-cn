---
title: "&lt;knownType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee2b7be3-7148-4a3a-b861-48e7330615e5
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;knownType&gt;
指定在反序列化过程中将由 <xref:System.Runtime.Serialization.DataContractSerializer> 使用的类型。  该元素指定由某个“声明的类型”的字段或属性返回到“已知类型”。有关详细信息，请参阅[数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。  
  
## 语法  
  
```  
  
<knownType type="String">  
     <parameter index="Integer"  
                type="String" />  
</knownType>  
```  
  
## 类型  
 `string`  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|类型|指定类型（包括命名空间）、程序集名称、版本、区域性和公钥标记。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<参数\>](../../../../../docs/framework/configure-apps/file-schema/wcf/parameter.md)|当声明类型为泛型类型时指定参数索引。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)|向声明类型的集合中添加一个声明类型。|  
  
## 备注  
 有关已知类型的更多信息，请参见[数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)和 <xref:System.Runtime.Serialization.DataContractSerializer>。  
  
 有关使用此元素的示例，请参见 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)。  
  
## 示例  
  
```  
<add type="MyCompany.Library.Shape,   
           MyAssembly, Version=2.0.0.0, Culture=neutral,  
           PublicKeyToken=XXXXXX, processorArchitecture=MSIL">  
           <knownType type="MyCompany.Library.Circle,   
                      MyAssembly, Version=2.0.0.0, Culture=neutral,  
                      PublicKeyToken=XXXXXX,  
                      processorArchitecture=MSIL"/>  
</add>  
```  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)   
 [\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)