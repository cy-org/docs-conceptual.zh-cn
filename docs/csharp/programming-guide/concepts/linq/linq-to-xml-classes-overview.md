---
title: "LINQ to XML 类概述 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: bf666100-5392-4968-97f4-f6b9d3287d7b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: de9664f56a0ab075d2c74b45d0eebab541213d06
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-xml-classes-overview-c"></a>LINQ to XML 类概述 (C#)
本主题提供 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 命名空间中 <xref:System.Xml.Linq> 类的列表及每个类的简短说明。  
  
## <a name="linq-to-xml-classes"></a>LINQ to XML 类  
  
### <a name="xattribute-class"></a>XAttribute 类  
 <xref:System.Xml.Linq.XAttribute> 表示一个 XML 属性。 有关详细信息和示例，请参阅 [XAttribute 类概述 (C#)](../../../../csharp/programming-guide/concepts/linq/xattribute-class-overview.md)。  
  
### <a name="xcdata-class"></a>XCData 类  
 <xref:System.Xml.Linq.XCData> 表示一个 CDATA 文本节点。  
  
### <a name="xcomment-class"></a>XComment 类  
 <xref:System.Xml.Linq.XComment> 表示一个 XML 注释。  
  
### <a name="xcontainer-class"></a>XContainer 类  
 <xref:System.Xml.Linq.XContainer> 是适用于可能具有子节点的所有节点的抽象基类。 下面的类派生自 <xref:System.Xml.Linq.XContainer> 类：  
  
-   <xref:System.Xml.Linq.XElement>  
  
-   <xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>XDeclaration 类  
 <xref:System.Xml.Linq.XDeclaration> 表示一个 XML 声明。 XML 声明用于声明 XML 版本和文档的编码。 此外，XML 声明还指定 XML 文档是否为独立文档。 如果文档是独立文档，则在外部 DTD 或从内部子集引用的外部参数实体中不存在外部标记声明。  
  
### <a name="xdocument-class"></a>XDocument 类  
 <xref:System.Xml.Linq.XDocument> 表示一个 XML 文档。 有关详细信息和示例，请参阅 [XDocument 类概述 (C#)](../../../../csharp/programming-guide/concepts/linq/xdocument-class-overview.md)。  
  
### <a name="xdocumenttype-class"></a>XDocumentType 类  
 <xref:System.Xml.Linq.XDocumentType> 表示一个 XML 文档类型定义 (DTD)。  
  
### <a name="xelement-class"></a>XElement 类  
 <xref:System.Xml.Linq.XElement> 表示一个 XML 元素。 有关详细信息和示例，请参阅 [XElement 类概述 (C#)](../../../../csharp/programming-guide/concepts/linq/xelement-class-overview.md)。  
  
### <a name="xname-class"></a>XName 类  
 <xref:System.Xml.Linq.XName> 表示元素 (<xref:System.Xml.Linq.XElement>) 和属性 (<xref:System.Xml.Linq.XAttribute>) 的名称。 有关详细信息和示例，请参阅 [XDocument 类概述 (C#)](../../../../csharp/programming-guide/concepts/linq/xdocument-class-overview.md)。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 旨在使 XML 名称尽可能简单。 XML 名称由于复杂而通常被视为 XML 中的高级主题。 有证据证明，这种复杂性不是由开发人员编程时通常使用的命名空间造成的，而是由命名空间前缀造成的。 使用命名空间前缀可以减少输入 XML 时需要的击键数或使 XML 更具可读性。 但是，前缀通常只是使用完整的 XML 命名空间的快捷方式，而且在大多数情况下都不是必需的。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 通过将所有前缀解析为其对应的 XML 命名空间来简化 XML 名称。 如果需要，可以通过 <xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A> 方法可以使用前缀。  
  
 如果有必要，可以控制命名空间前缀。 在某些情况下，如果使用的是其他 XML 系统（如 XSLT 或 XAML），则需要控制命名空间前缀。 例如，如果 XPath 表达式使用命名空间前缀且嵌入在 XSLT 样式表中，则将必须确保使用与 XPath 表达式中使用的前缀相匹配的命名空间前缀来序列化 XML 文档。  
  
### <a name="xnamespace-class"></a>XNamespace 类  
 <xref:System.Xml.Linq.XNamespace> 表示 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XAttribute> 的命名空间。 命名空间是 <xref:System.Xml.Linq.XName> 的一个组件。  
  
### <a name="xnode-class"></a>XNode 类  
 <xref:System.Xml.Linq.XNode> 是一个抽象类，它表示 XML 树的节点。 下面的类派生自 <xref:System.Xml.Linq.XNode> 类：  
  
-   <xref:System.Xml.Linq.XText>  
  
-   <xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XComment>  
  
-   <xref:System.Xml.Linq.XProcessingInstruction>  
  
-   <xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>XNodeDocumentOrderComparer 类  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer> 提供用于比较节点的文档顺序的功能。  
  
### <a name="xnodeequalitycomparer-class"></a>XNodeEqualityComparer 类  
 <xref:System.Xml.Linq.XNodeEqualityComparer> 提供用于比较节点的值是否相等的功能。  
  
### <a name="xobject-class"></a>XObject 类  
 <xref:System.Xml.Linq.XObject> 是 <xref:System.Xml.Linq.XNode> 和 <xref:System.Xml.Linq.XAttribute> 的抽象基类。 它提供批注和事件功能。  
  
### <a name="xobjectchange-class"></a>XObjectChange 类  
 <xref:System.Xml.Linq.XObjectChange> 指定对 <xref:System.Xml.Linq.XObject> 引发事件时的事件类型。  
  
### <a name="xobjectchangeeventargs-class"></a>XObjectChangeEventArgs 类  
 <xref:System.Xml.Linq.XObjectChangeEventArgs> 为 <xref:System.Xml.Linq.XObject.Changing> 和 <xref:System.Xml.Linq.XObject.Changed> 事件提供数据。  
  
### <a name="xprocessinginstruction-class"></a>XProcessingInstruction 类  
 <xref:System.Xml.Linq.XProcessingInstruction> 表示一个 XML 处理指令。 处理指令将信息传递给处理 XML 的应用程序。  
  
### <a name="xtext-class"></a>XText 类  
 <xref:System.Xml.Linq.XText> 表示一个文本节点。 多数情况下都不必使用此类。 此类主要用于混合内容。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)

