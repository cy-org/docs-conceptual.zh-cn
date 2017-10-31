---
title: "&lt;declaredTypes&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "<declaredTypes> 元素"
  - "DataContractSerializer"
  - "dataContractSerializer 元素"
  - "declaredTypes 元素"
  - "KnownTypes"
ms.assetid: f35184e4-9d9e-4d37-8fb4-d5b58220eb3e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;declaredTypes&gt;
包含在进行反序列化时 <xref:System.Runtime.Serialization.DataContractSerializer> 使用的已知类型。  
  
 有关数据协定和已知类型的更多信息，请参见[数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。  
  
## 语法  
  
```  
  
<configuration>  
  <system.runtime.serialization>  
    <dataContractSerializer>  
      <declaredTypes>  
        <add type="String ">  
          <knownType type="String">  
                <parameter index="Integer"/>  
          </knownType>  
        </add>  
      </declaredTypes>  
    <dataContractSerializer>  
  </system.runtime.serialization>  
</configuration>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)|添加需要已知类型的类型。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md)|包含 <xref:System.Runtime.Serialization.DataContractSerializer> 的配置数据。|  
  
## 备注  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]已知类型的更多信息，请参见[数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)和 <xref:System.Runtime.Serialization.DataContractSerializer>。  
  
## 示例  
 下面的 XML 代码演示声明类型和添加到 `DataContractSerializer` 元素的已知类型。  此示例演示要添加的三个类型。  第一个类型是名为“Orders”的自定义类型，它使用一个名为“Item”的已知类型。  第二个声明类型 <xref:System.Collections.Generic.List%601>，它使用 `Item` 作为已知类型。  最后，第三个声明类型是 <xref:System.Collections.Generic.Dictionary%602>。  <xref:System.Collections.Generic.Dictionary%602> 类类型是泛型类型，并带有两个类型参数。  第一个参数表示键，第二个参数表示值。  下面的示例将第二个类型的 <xref:System.Collections.Generic.List%601>（值）添加到已知类型的列表中。  必须使用 `index` 属性来指定在已知类型中使用的类型参数。  在此例中，通过将 index 属性设置为“1”（基于零的集合）来指示值类型。  
  
```  
<configuration>  
  <system.runtime.serialization>  
    <dataContractSerializer>  
      <declaredTypes>  
        <add type="Examples.Types.Orders, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />  
        </add>  
        <add type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />  
        </add>  
        <add type="System.Collections.Generic.Dictionary`2, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
            <parameter index="1"/>  
          </knownType>  
        </add>  
      </declaredTypes>  
    <dataContractSerializer>  
  </system.runtime.serialization>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)   
 [数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)