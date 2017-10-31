---
title: "推断架构节点类型和结构的规则 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: d74ce896-717d-4871-8fd9-b070e2f53cb0
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 推断架构节点类型和结构的规则
本主题介绍架构推断过程如何将 XML 文档中的节点类型转换为 XML 架构定义语言 \(XSD\) 结构。  
  
## 元素推断规则  
 本节说明元素声明的推断规则。  其中将推断八种元素声明结构：  
  
1.  简单类型的元素  
  
2.  空元素  
  
3.  具有属性的空元素  
  
4.  具有属性和简单内容的元素  
  
5.  具有一系列子元素的元素  
  
6.  具有一系列子元素和属性的元素  
  
7.  具有一系列子元素选择的元素  
  
8.  具有一系列子元素和属性选择的元素  
  
> [!NOTE]
>  所有 `complexType` 声明均推断为匿名类型。  唯一推断的全局元素是根元素；所有其他元素都是局部元素。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
### 简单类型化的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为简单类型元素推断的架构。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>text</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root" type="xs:string" />`<br /><br /> `\</xs:schema>`|  
  
### 空元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为空元素推断的架构。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="empty" />`<br /><br /> `\</xs:schema>`|  
  
### 具有属性的空元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有属性的空元素推断的架构。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty attribute1="text"/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="empty">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 具有属性和简单内容的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有属性和简单内容的元素推断的架构。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">value</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:simpleContent>`<br /><br /> `\<xs:extension base="xs:string">`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:extension>`<br /><br /> `\</xs:simpleContent>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 具有一系列子元素的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有一系列子元素的元素推断的架构。  
  
> [!NOTE]
>  即使元素只有一个子元素，仍作为一系列子元素对待。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:element name="subElement" />`<br /><br /> `\</xs:sequence>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 具有一系列子元素和属性的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有一系列子元素和属性的元素推断的架构。  
  
> [!NOTE]
>  即使元素只有一个子元素，仍作为一系列子元素对待。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:sequence>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 具有一系列子元素选择的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有一系列子元素选择的元素推断的架构。  
  
> [!NOTE]
>  在推断出的架构中，`xs:choice` 元素的 `maxOccurs` 属性设置为 `"unbounded"`。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:choice maxOccurs="unbounded">`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:choice>`<br /><br /> `\</xs:sequence>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 具有一系列子元素和属性选择的元素  
 下表显示 <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> 方法的 XML 输入以及生成的 XML 架构。  粗体的元素显示为具有一系列子元素和属性选择的元素推断的架构。  
  
> [!NOTE]
>  在推断出的架构中，`xs:choice` 元素的 `maxOccurs` 属性设置为 `"unbounded"`。  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
|XML|架构|  
|---------|--------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:choice maxOccurs="unbounded">`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:choice>`<br /><br /> `\</xs:sequence>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### 属性处理  
 只要在节点中遇到新属性，就会使用 `use="required"` 将新属性添加到推断出的节点定义中。  下次在该实例中发现同一个节点时，推断过程会将当前实例的属性与已推断出的属性进行比较。  如果该实例中缺少某些已推断出的属性，`use="optional"` 将添加到属性定义中。  新属性将使用 `use="optional"` 添加到现有声明中。  
  
### 匹配项约束  
 在架构推断过程中，会为推断出的架构组件生成 `minOccurs` 和 `maxOccurs` 属性，值为 `"0"` 或 `"1"` 以及 `"1"` 或 `"unbounded"`。  只有值 `"0"` 和 `"1"` 无法验证 XML 文档时，才会使用值 `"1"` 和 `"unbounded"`（例如，如果 `MinOccurs="0"` 没有准确描述某个元素，则使用 `minOccurs="1"`）。  
  
### 混合内容  
 如果某个元素包含混合内容（例如混合了文本和元素），将为推断出的复杂类型定义生成 `mixed="true"` 属性。  
  
## 其他节点类型推断规则  
 下表说明处理指令、注释、实体引用、CDATA、文档类型和命名空间节点的推断规则。  
  
|节点类型|转换|  
|----------|--------|  
|处理指令|已忽略。|  
|注释|已忽略。|  
|实体引用|<xref:System.Xml.Schema.XmlSchemaInference> 类不处理实体引用。  如果 XML 文档包含实体引用，需要使用可以展开实体的读取器。  例如，可以将 <xref:System.Xml.XmlTextReader.EntityHandling%2A> 属性设置为 <xref:System.Xml.EntityHandling> 的 <xref:System.Xml.XmlTextReader> 作为参数传递。  如果遇到实体引用，并且读取器没有展开实体，将引发异常。|  
|CDATA|XML 文档中的任何 `<![CDATA[   ]]` 节均将推断为 `xs:string`。|  
|文档类型|已忽略。|  
|命名空间|已忽略。|  
  
 有关架构推断过程的更多信息，请参见[从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)。  
  
## 请参阅  
 <xref:System.Xml.Schema.XmlSchemaInference>   
 [XML 架构对象模型 \(SOM\)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)   
 [推断 XML 架构](../../../../docs/standard/data/xml/inferring-an-xml-schema.md)   
 [从 XML 文档推断架构](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)   
 [推断简单类型的规则](../../../../docs/standard/data/xml/rules-for-inferring-simple-types.md)