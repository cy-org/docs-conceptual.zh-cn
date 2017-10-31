---
title: "XElement 类概述 (C#)"
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
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
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
ms.openlocfilehash: 20c6c7aed7d00b26d08f3733147616313ad851f3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="xelement-class-overview-c"></a>XElement 类概述 (C#)
<xref:System.Xml.Linq.XElement> 类是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的基础类之一。 它表示一个 XML 元素。 可以使用该类创建元素；更改元素内容；添加、更改或删除子元素；向元素中添加属性；或以文本格式序列化元素内容。 还可以与 <xref:System.Xml?displayProperty=fullName> 中的其他类（例如 <xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.Xsl.XslCompiledTransform>）进行互操作。  
  
## <a name="xelement-functionality"></a>XElement 功能  
 本主题描述 <xref:System.Xml.Linq.XElement> 类提供的功能。  
  
### <a name="constructing-xml-trees"></a>构造 XML 树  
 可以使用各种方式构造 XML 树，包括以下方式：  
  
-   可以在代码中构造 XML 树。 有关详细信息，请参阅[创建 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)。  
  
-   可以从包括 <xref:System.IO.TextReader>、文本文件或 Web 地址 (URL) 在内的各种源解析 XML。 有关详细信息，请参阅[解析 XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)。  
  
-   可以使用 <xref:System.Xml.XmlReader> 来填充树。 有关详细信息，请参阅<xref:System.Xml.Linq.XNode.ReadFrom%2A>。  
  
-   如果您有一个可以将内容写入 <xref:System.Xml.XmlWriter> 的模块，则可以使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 方法来创建编写器，将该编写器传递到该模块，然后使用写入 <xref:System.Xml.XmlWriter> 的内容来填充 XML 树。  
  
 但是，创建 XML 树的最常见的方法如下：  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 另一个创建 XML 树的十分常用的方法是使用 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询的结果来填充 XML 树，如下面的示例所示：  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
### <a name="serializing-xml-trees"></a>序列化 XML 树  
 可以将 XML 树序列化为 <xref:System.IO.File>、<xref:System.IO.TextWriter> 或 <xref:System.Xml.XmlWriter>。  
  
 有关详细信息，请参阅[序列化 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)。  
  
### <a name="retrieving-xml-data-via-axis-methods"></a>通过轴方法检索 XML 数据  
 可以使用轴方法检索属性、子元素、子代元素和上级元素。 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询对轴方法进行操作，并提供了多种灵活而有效的方法导航和处理 XML 树。  
  
 有关详细信息，请参阅 [LINQ to XML 轴 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)。  
  
### <a name="querying-xml-trees"></a>查询 XML 树  
 可以编写从 XML 树提取数据的 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询。  
  
 有关详细信息，请参阅[查询 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)。  
  
### <a name="modifying-xml-trees"></a>修改 XML 树  
 可以通过各种方式修改元素，例如更改元素的内容或属性。 还可以从元素的父级移除元素。  
  
 有关详细信息，请参阅[修改 XML 树 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)

