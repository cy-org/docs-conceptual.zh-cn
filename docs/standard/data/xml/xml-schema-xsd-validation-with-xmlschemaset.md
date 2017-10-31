---
title: "使用 XmlSchemaSet 进行 XML 架构 (XSD) 验证 | Microsoft Docs"
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
ms.assetid: 359b10eb-ec05-4cc6-ac96-c2b060afc4de
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 使用 XmlSchemaSet 进行 XML 架构 (XSD) 验证
XML 文档可以根据 <xref:System.Xml.Schema.XmlSchemaSet> 中的 XML 架构定义语言 \(XSD\) 架构进行验证。  
  
## 验证 XML 文档  
 XML 文档通过 <xref:System.Xml.XmlReader> 类的 <xref:System.Xml.XmlReader.Create%2A> 方法进行验证。  若要验证 XML 文档，请构造一个 <xref:System.Xml.XmlReaderSettings> 对象，其中包含用于验证 XML 文档的 XML 架构定义语言 \(XSD\) 架构。  
  
> [!NOTE]
>  <xref:System.Xml.Schema> 命名空间包含扩展方法，在使用 [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) 时，这些扩展方法可以简化针对 XSD 文件验证 XML 树的过程。  有关使用 LINQ to XML 验证 XML 文档的更多信息，请参见[如何：使用 XSD 进行验证](../Topic/How%20to:%20Validate%20Using%20XSD%20\(LINQ%20to%20XML\).md)。  
  
 通过将架构作为参数传递给 <xref:System.Xml.Schema.XmlSchemaSet> 的 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 方法，可以将单个架构或一组架构（作为 <xref:System.Xml.Schema.XmlSchemaSet>）添加到 <xref:System.Xml.Schema.XmlSchemaSet>。  请注意，在验证文档时，文档的目标命名空间必须匹配架构集中架构的目标命名空间。  
  
 下面是示例 XML 文档。  
  
 [!code-xml[XSDInference Examples#5](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xml#5)]  
  
 下面是验证示例 XML 文档的架构。  
  
 [!code-xml[XSDInference Examples#6](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xsd#6)]  
  
 在下面的代码示例中，上面的架构添加到 <xref:System.Xml.XmlReaderSettings> 对象的 <xref:System.Xml.Schema.XmlSchemaSet> <xref:System.Xml.XmlReaderSettings.Schemas%2A> 属性中。  <xref:System.Xml.XmlReaderSettings> 对象作为参数传递给验证上述 XML 文档的 <xref:System.Xml.XmlReader> 对象的 <xref:System.Xml.XmlReader.Create%2A> 方法。  
  
 <xref:System.Xml.XmlReaderSettings> 对象的 <xref:System.Xml.XmlReaderSettings.ValidationType%2A> 属性设置为 `Schema`，强制通过 <xref:System.Xml.XmlReader> 对象的 <xref:System.Xml.XmlReader.Create%2A> 方法验证 XML 文档。  将 <xref:System.Xml.Schema.ValidationEventHandler> 添加到 <xref:System.Xml.XmlReaderSettings> 对象以处理 XML 文档和架构验证过程中发现的错误所引发的任何 <xref:System.Xml.Schema.XmlSeverityType> 或 <xref:System.Xml.Schema.XmlSeverityType> 事件。  
  
 [!code-cpp[XmlSchemaSetOverall Example#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaSetOverall Example/CPP/xmlschemasetexample.cpp#1)]
 [!code-csharp[XmlSchemaSetOverall Example#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaSetOverall Example/CS/xmlschemasetexample.cs#1)]
 [!code-vb[XmlSchemaSetOverall Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaSetOverall Example/VB/xmlschemasetexample.vb#1)]  
  
## 请参阅  
 [用于编译架构的 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [使用 XML 架构](../../../../docs/standard/data/xml/working-with-xml-schemas.md)