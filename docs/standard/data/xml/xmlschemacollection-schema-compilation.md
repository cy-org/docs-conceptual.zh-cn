---
title: "XmlSchemaCollection 架构编译 | Microsoft Docs"
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
ms.assetid: 76f28770-7126-428f-9ed5-7b5ae8bad5ee
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# XmlSchemaCollection 架构编译
**XmlSchemaCollection** 是一个缓存或库，可以在其中存储和验证 XML 数据缩减\(XDR\) 和 XML 架构定义语言 \(XSD\) 架构。  **XmlSchemaCollection** 在内存中缓存架构，而不是从文件或 URL 访问架构，从而提高了性能。  
  
> [!NOTE]
>  尽管 **XmlSchemaCollection** 类既存储 XDR 架构也存储 XML 架构，但任何接受或返回 **XmlSchema** 对象的方法和属性都只支持 XML 架构。  
  
> [!IMPORTANT]
>  现在，<xref:System.Xml.Schema.XmlSchemaCollection> 类已过时，已由 <xref:System.Xml.Schema.XmlSchemaSet> 类所取代。  有关 <xref:System.Xml.Schema.XmlSchemaSet> 类的更多信息，请参见 [用于编译架构的 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)。  
  
## 向集合中添加架构  
 使用 **XmlSchemaCollection** 的 **Add** 方法向集合中加载架构，这时架构将与一个命名空间 URI 相关联。  对于 XML 架构，命名空间 URI 通常是该架构的目标命名空间。  对于 XDR 架构，命名空间 URI 是在将架构添加到集合时指定的命名空间。  
  
## 检查集合中是否存在架构  
 通过使用 **Contains** 方法，可以检查集合中是否存在架构。  **Contains** 方法接受 **XmlSchema** 对象（仅对于 XML 架构）或代表与架构关联的命名空间 URI 的字符串（对于 XML 架构和 XDR 架构）。  
  
## 从集合中检索架构  
 通过使用 **Item** 属性，可以从集合中检索架构。  **Item** 属性接受代表与架构关联的命名空间 URI 的字符串（通常是它的目标命名空间）并返回 **XmlSchema** 对象。  **Item** 属性仅适用于 XML 架构。  对于 XDR 架构，返回值总是空引用，因为它们没有可用的对象模型。  
  
## 使用 XmlSchemaCollection 验证 XML 文档  
 可以使用 **XmlSchemaCollection** 验证 XML 实例文档，方法是创建 **XmlSchemaCollection** 对象，将架构添加到集合中，然后设置 **XmlValidatingReader** 的 **Schemas** 属性，以将已创建的 **XmlSchemaCollection** 分配给 **XmlValidatingReader**。  
  
### 提高的性能  
 如果根据同一个架构验证多个文档，建议您使用 **XmlSchemaCollection**，这是因为它在内存中缓存架构，从而提供了更好的性能。  
  
 下面的代码示例创建 **XmlSchemaCollection** 对象，将架构添加到集合中并设置 **Schemas** 属性。  
  
```vb  
Dim tr as XmlTextReader = new XmlTextReader("Books.xml")  
Dim vr as XmlValidatingReader = new XmlValidatingReader(tr)  
Dim xsc as XmlSchemaCollection = new XmlSchemaCollection  
xsc.Add("urn:bookstore-schema", "Books.xsd")  
vr.Schemas.Add(xsc)  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("Books.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
xsc.Add("urn:bookstore-schema", "Books.xsd");    
vr.Schemas.Add(xsc);  
```  
  
## 请参阅  
 [使用 XmlSchemaCollection 进行 XDR 验证](../../../../docs/standard/data/xml/xdr-validation-with-xmlschemacollection.md)   
 [使用 XmlSchemaCollection 进行 XML 架构 \(XSD\) 验证](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemacollection.md)