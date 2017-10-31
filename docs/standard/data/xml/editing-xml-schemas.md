---
title: "编辑 XML 架构 | Microsoft Docs"
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
ms.assetid: fa09c8e5-c2b9-49d2-bb0d-40330cd13e4d
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 编辑 XML 架构
编辑 XML 架构是架构对象模型 \(SOM\) 最重要的功能之一。  SOM 的所有前架构编译属性均可以用于更改 XML 架构中的现有值。  然后，可以重新编译 XML 架构以反映更改。  
  
 编辑加载到 SOM 中的架构的第一步是遍历架构。  在尝试编辑架构之前，应熟悉如何使用 SOM API 遍历架构。  还应熟悉后架构编译信息集 \(PSCI\) 的前架构编译属性和后架构编译属性。  
  
## 编辑 XML 架构  
 在本节中提供了两个代码示例，这两个示例均编辑 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md) 主题中创建的客户架构。  第一个代码示例向 `Customer` 元素中添加新的 `PhoneNumber` 元素，第二个代码示例向 `FirstName` 元素中添加新的 `Title` 属性。  第一个示例还使用后架构编译 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> 集合遍历客户架构，而第二个代码示例使用前架构编译 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> 集合遍历客户架构。  
  
### PhoneNumber 元素示例  
 第一个代码示例向客户架构的 `Customer` 元素中添加新的 `PhoneNumber` 元素。  代码示例通过下列步骤编辑客户架构。  
  
1.  将客户架构添加到新的 <xref:System.Xml.Schema.XmlSchemaSet> 对象并进行编译。  在读取或编译架构时遇到的任何架构验证警告和错误由 <xref:System.Xml.Schema.ValidationEventHandler> 委托进行处理。  
  
2.  通过循环访问 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 属性，从 <xref:System.Xml.Schema.XmlSchemaSet> 中检索已编译的 <xref:System.Xml.Schema.XmlSchema> 对象。  因为架构已编译，所以，可以访问后架构编译信息集 \(PSCI\) 属性。  
  
3.  使用 <xref:System.Xml.Schema.XmlSchemaElement> 类创建 `PhoneNumber` 元素，使用 <xref:System.Xml.Schema.XmlSchemaSimpleType> 和 <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction> 类创建 `xs:string` 简单类型限制，将模式方面添加到限制的 <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction.Facets%2A> 属性，然后将限制添加到简单类型的 <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A> 并将简单类型添加到 `PhoneNumber` 元素的 <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A>。  
  
4.  在后架构编译 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> 集合的 <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> 集合中循环访问每个 <xref:System.Xml.Schema.XmlSchemaElement>。  
  
5.  如果元素的 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> 为 `"Customer"`，请使用 <xref:System.Xml.Schema.XmlSchemaComplexType> 类获取 `Customer` 元素的复杂类型并使用 <xref:System.Xml.Schema.XmlSchemaSequence> 类获取复杂类型的序列粒子。  
  
6.  使用序列的前架构编译 <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A> 集合将新的 `PhoneNumber` 元素添加到包含现有 `FirstName` 和 `LastName` 元素的序列中。  
  
7.  最后，使用 <xref:System.Xml.Schema.XmlSchemaSet> 类的 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 和 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 方法重新处理并编译已修改的 <xref:System.Xml.Schema.XmlSchema> 对象并将其写入控制台。  
  
 以下是完整的代码示例。  
  
 [!code-cpp[XmlSchemaEditExample1#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample1/CPP/XmlSchemaEditExample1.cpp#1)]
 [!code-csharp[XmlSchemaEditExample1#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample1/CS/XmlSchemaEditExample1.cs#1)]
 [!code-vb[XmlSchemaEditExample1#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample1/VB/XmlSchemaEditExample1.vb#1)]  
  
 以下是 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md) 主题中创建的客户架构经过修改的版本。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="xs:string" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
        <xs:element name="PhoneNumber">  
          <xs:simpleType>  
            <xs:restriction base="xs:string">  
              <xs:pattern value="\d{3}-\d{3}-\d(4)" />  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:element>  
      </xs:sequence>  
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /  
>  
    </xs:complexType>  
  </xs:element>  
  <xs:simpleType name="LastNameType">  
    <xs:restriction base="xs:string">  
      <xs:maxLength value="20" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
```  
  
### Title 属性示例  
 第二个代码示例向客户架构的 `FirstName` 元素中添加新的 `Title` 属性。  在第一个代码示例中，`FirstName` 元素的类型为 `xs:string`。  为了使 `FirstName` 元素包含属性以及字符串内容，其类型必须使用简单内容扩展内容模型更改为复杂类型。  
  
 代码示例通过下列步骤编辑客户架构。  
  
1.  将客户架构添加到新的 <xref:System.Xml.Schema.XmlSchemaSet> 对象并进行编译。  在读取或编译架构时遇到的任何架构验证警告和错误由 <xref:System.Xml.Schema.ValidationEventHandler> 委托进行处理。  
  
2.  通过循环访问 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 属性，从 <xref:System.Xml.Schema.XmlSchemaSet> 中检索已编译的 <xref:System.Xml.Schema.XmlSchema> 对象。  因为架构已编译，所以，可以访问后架构编译信息集 \(PSCI\) 属性。  
  
3.  使用 <xref:System.Xml.Schema.XmlSchemaComplexType> 类为 `FirstName` 元素创建新的复杂类型。  
  
4.  使用 <xref:System.Xml.Schema.XmlSchemaSimpleContent> 和 <xref:System.Xml.Schema.XmlSchemaSimpleContentExtension> 类创建新的简单内容扩展，基类型为 `xs:string`。  
  
5.  使用 <xref:System.Xml.Schema.XmlSchemaAttribute> 类创建新的 `Title` 属性，<xref:System.Xml.Schema.XmlSchemaAttribute.SchemaTypeName%2A> 为 `xs:string`，并将该属性添加到简单内容扩展。  
  
6.  将简单内容的内容模型设置为简单内容扩展，将复杂类型的内容模型设置为简单内容。  
  
7.  将新的复杂类型添加到前架构编译 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> 集合。  
  
8.  在前架构编译 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> 集合中循环访问每个 <xref:System.Xml.Schema.XmlSchemaObject>。  
  
> [!NOTE]
>  因为 `FirstName` 元素不是架构中的全局元素，所以，不能在 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> 或 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> 集合中使用。  代码示例通过首先定位 `Customer` 元素来定位 `FirstName` 元素。  
>   
>  第一个代码示例使用后架构编译 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> 集合遍历了架构。  在此示例中，前架构编译 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> 集合用于遍历架构。  尽管两个集合均提供对架构中的全局元素的访问，但是循环访问 <xref:System.Xml.Schema.XmlSchema.Items%2A> 集合使用的时间更长，因为必须循环访问架构中的所有全局元素，没有任何 PSCI 属性。  PSCI 集合（<xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName>、<xref:System.Xml.Schema.XmlSchema.Attributes%2A?displayProperty=fullName>、<xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A?displayProperty=fullName> 等）提供对其全局元素、属性和类型及其 PSCI 属性的直接访问。  
  
1.  如果 <xref:System.Xml.Schema.XmlSchemaObject> 为元素，该元素的 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> 为 `"Customer"`，请使用 <xref:System.Xml.Schema.XmlSchemaComplexType> 类获取 `Customer` 元素的复杂类型并使用 <xref:System.Xml.Schema.XmlSchemaSequence> 类获取复杂类型的序列粒子。  
  
2.  在前架构编译 <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=fullName> 集合中循环访问每个 <xref:System.Xml.Schema.XmlSchemaParticle>。  
  
3.  如果 <xref:System.Xml.Schema.XmlSchemaParticle> 为元素，该元素的 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> 为 `"FirstName"`，请将 `FirstName` 元素的 <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> 设置为新的 `FirstName` 复杂类型。  
  
4.  最后，使用 <xref:System.Xml.Schema.XmlSchemaSet> 类的 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 和 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 方法重新处理并编译已修改的 <xref:System.Xml.Schema.XmlSchema> 对象并将其写入控制台。  
  
 以下是完整的代码示例。  
  
 [!code-cpp[XmlSchemaEditExample2#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample2/CPP/XmlSchemaEditExample2.cpp#1)]
 [!code-csharp[XmlSchemaEditExample2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample2/CS/XmlSchemaEditExample2.cs#1)]
 [!code-vb[XmlSchemaEditExample2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample2/VB/XmlSchemaEditExample2.vb#1)]  
  
 以下是 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md) 主题中创建的客户架构经过修改的版本。  
  
```  
<?xml version="1.0" encoding=" utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="tns:FirstNameComplexType" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
      </xs:sequence>  
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /  
>  
    </xs:complexType>  
  </xs:element>  
  <xs:simpleType name="LastNameType">  
    <xs:restriction base="xs:string">  
      <xs:maxLength value="20" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:complexType name="FirstNameComplexType">  
    <xs:simpleContent>  
      <xs:extension base="xs:string">  
        <xs:attribute name="Title" type="xs:string" />  
      </xs:extension>  
    </xs:simpleContent>  
  </xs:complexType>  
</xs:schema>  
```  
  
## 请参阅  
 [XML 架构对象模型概述](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [读取和写入 XML 架构](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [遍历 XML 架构](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [包含或导入 XML 架构](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [用于编译架构的 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [后架构编译信息集](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)