---
title: "XML 架构对象模型概述 | Microsoft Docs"
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
ms.assetid: 896a1e12-5655-42c6-8cdd-89c12862b34b
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# XML 架构对象模型概述
Microsoft .NET Framework 中的架构对象模型 \(SOM\) 是一个丰富 API，可以通过编程创建、编辑和验证架构。  SOM 对 XML 架构文档的作用类似与文档对象模型 \(DOM\) 对 XML 文档的作用。  XML 架构文档是有效的 XML 文件，在加载到 SOM 之后，传达其他符合该架构的 XML 文档的结构和有效性的含义。  
  
 架构是一个 XML 文档，通过为特定架构指定 XML 文档的结构或模型来定义 XML 文档的类。  架构标识对于 XML 文档内容的约束，并描述符合该架构的 XML 文档为针对该特定架构视为有效而必须遵循的词汇（规则或语法）。  XML 文档验证是确保文档符合架构所指定的语法的过程。  
  
 .NET Framework 中的 SOM API 可以通过下列方式创建、编辑和验证架构。  
  
-   从文件中加载有效架构或将有效架构保存到文件中。  
  
-   使用强类型类创建内存中架构。  
  
-   与 <xref:System.Xml.Schema.XmlSchemaSet> 类进行交互，以缓存、编译和检索架构。  
  
-   与 <xref:System.Xml.XmlReader.Create%2A> 类的 <xref:System.Xml.XmlReader> 方法进行交互，以针对架构验证 XML 实例文档。  
  
-   生成用于创建和维护架构的编辑器。  
  
-   动态编辑架构，可以编译并保存该架构，供验证 XML 实例文档时使用。  
  
## 架构对象模型  
 SOM 由 <xref:System.Xml.Schema?displayProperty=fullName> 命名空间中与 XML 架构中的元素对应的丰富类集组成。  例如，`<xsd:schema>...</xsd:schema>` 元素映射到 <xref:System.Xml.Schema.XmlSchema?displayProperty=fullName> 类，所有可以包含在 `<xsd:schema/>` 元素中的信息都可以使用 <xref:System.Xml.Schema.XmlSchema> 类表示。  同样，`<xsd:element>...</xsd:element>` 和 `<xsd:attribute>...</xsd:attribute>` 元素分别映射到 <xref:System.Xml.Schema.XmlSchemaElement?displayProperty=fullName> 和 <xref:System.Xml.Schema.XmlSchemaAttribute?displayProperty=fullName> 类。  此映射继续为 XML 架构的所有元素在 <xref:System.Xml.Schema> 命名空间中创建 XML 架构对象模型，如下图中所示。  
  
 ![System.Xml.Schema 对象模型](../../../../docs/standard/data/xml/media/xmlschemaobjmodeloverview.png "XMLSchemaObjModelOverview")  
  
 有关 <xref:System.Xml.Schema> 命名空间中的每个类的更多信息，请参见 .NET Framework 类库中的 <xref:System.Xml.Schema> 命名空间参考文档。  
  
## 请参阅  
 [读取和写入 XML 架构](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [遍历 XML 架构](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [编辑 XML 架构](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [包含或导入 XML 架构](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [用于编译架构的 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [后架构编译信息集](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)