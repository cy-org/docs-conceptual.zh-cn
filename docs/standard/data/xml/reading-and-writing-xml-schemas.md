---
title: "读取和写入 XML 架构 | Microsoft Docs"
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
ms.assetid: b5757c4a-ea59-467e-ac62-be2bfe24eb77
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 读取和写入 XML 架构
架构对象模型 \(SOM\) API 可以用于从文件或其他源读取和写入 XML 架构定义语言 \(XSD\) 架构并使用 <xref:System.Xml.Schema?displayProperty=fullName> 命名空间中的类生成内存中 XML 架构，这些架构映射到万维网联合会 \(W3C\) XML 架构建议中定义的结构。  
  
## 读写 XML 架构  
 <xref:System.Xml.Schema.XmlSchema> 类提供 <xref:System.Xml.Schema.XmlSchema.Read%2A> 和 <xref:System.Xml.Schema.XmlSchema.Write%2A> 方法来读取和写入 XML 架构。  <xref:System.Xml.Schema.XmlSchema.Read%2A> 方法返回表示 XML 架构的 <xref:System.Xml.Schema.XmlSchema> 对象并使用可选的 <xref:System.Xml.Schema.ValidationEventHandler> 作为参数，以处理在读取 XML 架构时遇到的架构验证警告和错误。  
  
 <xref:System.Xml.Schema.XmlSchema.Write%2A> 方法将 XML 架构写入 <xref:System.IO.Stream>、<xref:System.IO.TextWriter> 和 <xref:System.Xml.XmlWriter> 对象，并且可以使用可选的 <xref:System.Xml.XmlNamespaceManager> 对象作为参数。  <xref:System.Xml.XmlNamespaceManager> 用于处理在 XML 架构中遇到的命名空间。  有关 <xref:System.Xml.XmlNamespaceManager> 类的更多信息，请参见[管理 XML 文档中的命名空间](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)。  
  
 以下代码示例说明如何在文件中读取和写入 XML 架构。  代码示例使用 `example.xsd` 文件，使用 `static` <xref:System.Xml.Schema.XmlSchema.Read%2A> 方法将其读入 <xref:System.Xml.Schema.XmlSchema> 对象，然后将文件写入控制台和新的 `new.xsd` 文件。  代码示例还将 <xref:System.Xml.Schema.ValidationEventHandler> 作为参数传递给 `static` <xref:System.Xml.Schema.XmlSchema.Read%2A> 方法，以处理在读取 XML 架构时遇到的任何架构验证警告或错误。  如果未指定 <xref:System.Xml.Schema.ValidationEventHandler> \(`null`\)，则不会报告任何警告或错误。  
  
 [!code-cpp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaReadWriteExample/CPP/XmlSchemaReadWriteExample.cpp#1)]
 [!code-csharp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaReadWriteExample/CS/XmlSchemaReadWriteExample.cs#1)]
 [!code-vb[XmlSchemaReadWriteExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaReadWriteExample/VB/XmlSchemaReadWriteExample.vb#1)]  
  
 该示例使用 `example.xsd` 作为输入。  
  
```  
<?xml version="1.0"?>  
<xs:schema id="play" targetNamespace="http://tempuri.org/play.xsd" elementFormDefault="qualified" xmlns="http://tempuri.org/play.xsd" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:element name='myShoeSize'>  
        <xs:complexType>  
            <xs:simpleContent>  
                <xs:extension base='xs:decimal'>  
                    <xs:attribute name='sizing' type='xs:string' />  
                </xs:extension>  
            </xs:simpleContent>  
        </xs:complexType>  
    </xs:element>  
</xs:schema>  
```  
  
## 请参阅  
 [XML 架构对象模型概述](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [生成 XML 架构](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [遍历 XML 架构](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [编辑 XML 架构](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [包含或导入 XML 架构](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [用于编译架构的 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [后架构编译信息集](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)   
 [管理 XML 文档中的命名空间](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)