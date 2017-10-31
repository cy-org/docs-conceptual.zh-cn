---
title: "XML 文档对象模型 (DOM) | Microsoft Docs"
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
ms.assetid: b5e52844-4820-47c0-a61d-de2da33e9f54
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# XML 文档对象模型 (DOM)
XML 文档对象模型 \(DOM\) 类是 XML 文档的内存中表示形式。  DOM 使您能够以编程方式读取、处理和修改 XML 文档。  **XmlReader** 类也读取 XML，但它提供非缓存的只进、只读访问。  这意味着使用 **XmlReader** 无法编辑属性值或元素内容，也无法插入和移除节点。  编辑是 DOM 的主要功能。  XML 数据在内存中表示是常见的结构化方法，尽管实际的 XML 数据在文件中时或从另一个对象传入时以线性方式存储。  以下是 XML 数据。  
  
## 输入  
  
```  
<?xml version="1.0"?>  
  <books>  
    <book>  
        <author>Carson</author>  
        <price format="dollar">31.95</price>  
        <pubdate>05/01/2001</pubdate>  
    </book>  
    <pubinfo>  
        <publisher>MSPress</publisher>  
        <state>WA</state>  
    </pubinfo>  
  </books>   
```  
  
 下图显示将此 XML 数据读入 DOM 结构中时如何构造内存。  
  
 ![XML 文档结构](../../../../docs/standard/data/xml/media/xml-to-domtree.gif "XML\_To\_DOMTree")  
XML 文档结构  
  
 在 XML 文档结构中，此图中的每个圆圈表示一个节点（称为 **XmlNode** 对象）。  **XmlNode** 对象是 DOM 树中的基本对象。  **XmlDocument** 类（扩展 **XmlNode**）支持用于对整个文档执行操作（例如，将文档加载到内存中或将 XML 保存到文件中）的方法。  此外，**XmlDocument** 提供了查看和处理整个 XML 文档中的节点的方法。  **XmlNode** 和 **XmlDocument** 都具有性能和可用性增强，并通过方法和属性执行下列操作：  
  
-   访问和修改 DOM 特定的节点，如元素节点、实体引用节点等。  
  
-   除检索节点包含的信息（如元素节点中的文本）外，还检索整个节点。  
  
    > [!NOTE]
    >  如果应用程序不需要 DOM 提供的结构或编辑功能，则 **XmlReader** 和 **XmlWriter** 类提供对 XML 的非缓存的只进流访问。  有关详细信息，请参阅 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter>。  
  
 **Node** 对象具有一组方法和属性以及基本的和定义完善的特性。  其中的某些特性包括：  
  
-   节点有单个父节点，父节点是与节点相邻的上一级节点。  唯一没有父级的节点是文档根，因为它是顶级节点，包含了文档本身和文档片段。  
  
-   大多数节点可以有多个子节点，子节点是与节点相邻的下一级节点。  以下是可以有子节点的节点类型列表。  
  
    -   **文档**  
  
    -   **DocumentFragment**  
  
    -   **EntityReference**  
  
    -   **元素**  
  
    -   **特性**  
  
     **XmlDeclaration**、**Notation**、**Entity**、**CDATASection**、**Text**、**Comment**、**ProcessingInstruction** 和 **DocumentType** 节点没有子节点。  
  
-   处于同一级别、在关系图中由 **book** 和 **pubinfo** 节点表示的节点是同级。  
  
 DOM 的一个特性是处理属性的方式。  属性是不属于父子关系和同级关系的节点。  属性被视为元素节点的属性，由名称和值对组成。  例如，如果存在由与元素 `format="dollar` 关联的 `price`" 组成的 XML 数据，则单词 `format` 是名称，`format` 属性的值是 `dollar`。  为检索 `format="dollar"`price 节点的  **属性，可以在游标位于  元素节点时调用 `price`GetAttribute 方法。** 有关更多信息，请参见[访问 DOM 中的属性](../../../../docs/standard/data/xml/accessing-attributes-in-the-dom.md)。  
  
 将 XML 读入内存时会创建节点。  然而，并非所有节点都是同一类型。  XML 中的元素具有不同于处理指令的规则和语法。  因此，在读取各种数据时，将为每个节点分配一种节点类型。  此节点类型确定节点的特性和功能。  
  
 有关在内存中生成的节点类型的更多信息，请参见 [XML 节点类型](../../../../docs/standard/data/xml/types-of-xml-nodes.md)。  有关在节点树中创建的对象的更多信息，请参见[将对象层次结构映射到 XML 数据](../../../../docs/standard/data/xml/mapping-the-object-hierarchy-to-xml-data.md)。  
  
 Microsoft 扩展了万维网联合会 \(W3C\) DOM 级别 1 和级别 2 中可用的 API，使 XML 文档的使用更容易。  在完全支持 W3C 标准的同时，附加的类、方法和属性增加了使用 W3C XML DOM 无法完成的功能。  新类使您能够访问关系数据，为您提供与 ADO.NET 数据同步、同时将数据作为 XML 公开的方法。  有关更多信息，请参见[使 DataSet 与 XmlDataDocument 同步](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)。  
  
 在将 XML 数据读入内存，以更改其结构、添加或移除节点或者与在元素包含的文本中一样修改节点所保存的数据时，DOM 最有用。  不过，在其他方案中，还有其他比 DOM 更快的类。  要对 XML 进行快速非缓存只进流访问，请使用 **XmlReader** 和 **XmlWriter**。  如果需要用游标模型和 **XPath** 进行随机访问，请使用 **XPathNavigator** 类。  
  
## 请参阅  
 [XML 节点类型](../../../../docs/standard/data/xml/types-of-xml-nodes.md)   
 [将对象层次结构映射到 XML 数据](../../../../docs/standard/data/xml/mapping-the-object-hierarchy-to-xml-data.md)