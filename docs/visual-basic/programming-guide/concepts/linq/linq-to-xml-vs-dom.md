---
title: "LINQ to XML 与DOM (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 18c36130-d598-40b7-9007-828232252978
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 88b6bddcdeec2859844f5d5f94777146d488b5fb
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-vs-dom-visual-basic"></a>LINQ to XML 与DOM (Visual Basic)
本部分介绍一些主要差异[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]和当前主导 XML 编程 API (W3C 文档对象模型 (DOM)。  
  
## <a name="new-ways-to-construct-xml-trees"></a>构造 XML 树的新方式  
 在 W3C DOM 中，应当从下至上生成 XML 树；即先创建文档，然后创建元素，再将元素添加到文档。  
  
 例如，以下是创建使用 DOM， <xref:System.Xml.XmlDocument>::</xref:System.Xml.XmlDocument>的 Microsoft 实现的 XML 树的典型方法  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
Dim phone1 As XmlElement = doc.CreateElement("Phone")  
phone1.SetAttribute("Type", "Home")  
phone1.InnerText = "206-555-0144"  
Dim phone2 As XmlElement = doc.CreateElement("Phone")  
phone2.SetAttribute("Type", "Work")  
phone2.InnerText = "425-555-0145"  
Dim street1 As XmlElement = doc.CreateElement("Street1")  
street1.InnerText = "123 Main St"  
Dim city As XmlElement = doc.CreateElement("City")  
city.InnerText = "Mercer Island"  
Dim state As XmlElement = doc.CreateElement("State")  
state.InnerText = "WA"  
Dim postal As XmlElement = doc.CreateElement("Postal")  
postal.InnerText = "68042"  
Dim address As XmlElement = doc.CreateElement("Address")  
address.AppendChild(street1)  
address.AppendChild(city)  
address.AppendChild(state)  
address.AppendChild(postal)  
Dim contact As XmlElement = doc.CreateElement("Contact")  
contact.AppendChild(name)  
contact.AppendChild(phone1)  
contact.AppendChild(phone2)  
contact.AppendChild(address)  
Dim contacts As XmlElement = doc.CreateElement("Contacts")  
contacts.AppendChild(contact)  
doc.AppendChild(contacts)  
Console.WriteLine(doc.OuterXml)  
```  
  
 这种编码方式不会提供很多有关 XML 树结构的可视信息。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]支持此方法构造 XML 树，但也支持另一种方法*功能性构造法*。 在 Visual Basic 中，函数构造使用 XML 文本来生成 XML 树。  
  
 下面演示如何通过使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 功能性构造法构造相同的 XML 树：  
  
```vb  
Dim contacts = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone Type="Home">206-555-0144</Phone>  
            <Phone Type="Work">425-555-0145</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
 请注意，缩进用于构造 XML 树的代码可显示基础 XML 的结构。  
  
 有关详细信息，请参阅[创建 XML 树 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)。  
  
## <a name="working-directly-with-xml-elements"></a>直接使用 XML 元素  
 在使用 XML 编程时，主要关注的通常是 XML 元素，也可能关注属性。 在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中，可以直接使用 XML 元素和属性。 例如，可以执行以下操作：  
  
-   创建 XML 元素而根本不使用文档对象。 当必须使用 XML 树的片段时，这可简化编程。  
  
-   直接从 XML 文件加载 `T:System.Xml.Linq.XElement` 对象。  
  
-   将 `T:System.Xml.Linq.XElement` 对象序列化为文件或流。  
  
 比较而言，W3C DOM 中的 XML 文档用作 XML 树的逻辑容器。 在 DOM 中，必须在 XML 文档的上下文中创建 XML 节点，包括元素和属性。 下面是在 DOM 中创建一个 name 元素的代码片段：  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
doc.AppendChild(name)  
```  
  
 如果要跨多个文档使用某个元素，则必须跨文档导入节点。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]避免了这一复杂。  
  
 如果使用 LINQ to XML，则使用<xref:System.Xml.Linq.XDocument>类仅当您想要在文档的根级别添加注释或处理指令。</xref:System.Xml.Linq.XDocument>  
  
## <a name="simplified-handling-of-names-and-namespaces"></a>名称和命名空间的简化处理  
 处理名称、命名空间和命名空间前缀通常是 XML 编程的复杂部分。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]通过不需要处理命名空间前缀，从而简化了名称和命名空间。 可以轻松控制命名空间前缀。 但如果您决定不显式控制命名空间前缀，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 将会在序列化过程中分配命名空间前缀（如果需要）或使用默认命名空间进行序列化（如果不需要）。 如果使用默认命名空间，则生成的文档中将没有命名空间前缀。 有关详细信息，请参阅[处理 XML 命名空间 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)。  
  
 DOM 的另一个问题是它不允许您更改节点的名称。 您必须创建新节点并将所有子节点复制到此节点，从而会失去原始节点标识。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]使您能够设置可避免此问题<xref:System.Xml.Linq.XName>节点上的属性。</xref:System.Xml.Linq.XName>  
  
## <a name="static-method-support-for-loading-xml"></a>对加载 XML 的静态方法支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 允许您通过使用静态方法而不是实例方法来加载 XML。 这简化了加载和分析。 有关详细信息，请参阅[如何︰ 从文件 (Visual Basic 中) 的负载 XML](../../../../visual-basic/programming-guide/concepts/linq/how-to-load-xml-from-a-file.md)。  
  
## <a name="removal-of-support-for-dtd-constructs"></a>移除对 DTD 构造的支持  
 通过移除对实体和实体引用的支持，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 进一步简化了 XML 编程。 实体因管理复杂而很少使用。 移除对它们的支持可提高性能并简化编程接口。 在填充 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 树时，会展开所有 DTD 实体。  
  
## <a name="support-for-fragments"></a>对片段的支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 未提供 `XmlDocumentFragment` 类的等效项。 在许多情况下，但是，`XmlDocumentFragment`概念可以处理由该查询将被类型化为结果<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XNode>，或<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XNode> </xref:System.Collections.Generic.IEnumerable%601>  
  
## <a name="support-for-xpathnavigator"></a>对 XPathNavigator 的支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]提供了对支持<xref:System.Xml.XPath.XPathNavigator>中的扩展方法通过<xref:System.Xml.XPath?displayProperty=fullName>命名空间。</xref:System.Xml.XPath?displayProperty=fullName> </xref:System.Xml.XPath.XPathNavigator> 有关详细信息，请参阅<xref:System.Xml.XPath.Extensions?displayProperty=fullName>。</xref:System.Xml.XPath.Extensions?displayProperty=fullName>  
  
## <a name="support-for-white-space-and-indentation"></a>对空白和缩进的支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 处理空白的方式比 DOM 更简单。  
  
 一种常用情况是读取缩进的 XML，在内存中创建一个没有任何空白文本节点（即不保留空白）的 XML 树，对该 XML 执行某些操作，然后保存带缩进的 XML。 在序列化带格式的 XML 时，只保留 XML 树中有意义的空白。 这是 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的默认行为。  
  
 另一个常见的情况是读取和修改已经有意缩进的 XML。 您可能不想以任何方式更改这种缩进。 在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中，可以通过在加载或解析 XML 时保留空白，并在序列化 XML 时禁用格式设置来实现此目的。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]将空白存储为<xref:System.Xml.Linq.XText>节点，而不是具有专门<xref:System.Xml.XmlNodeType>节点类型，像 DOM 那样。</xref:System.Xml.XmlNodeType> </xref:System.Xml.Linq.XText>  
  
## <a name="support-for-annotations"></a>对批注的支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 元素支持可扩展的批注集。 这对于跟踪有关元素的杂项信息（如架构信息、关于元素是否绑定到 UI 的信息或应用程序特定的任何其他信息）很有用。 有关详细信息，请参阅[LINQ to XML 批注](http://msdn.microsoft.com/library/e2f0052d-61e2-48d4-9ea4-356c9cab35d5)。  
  
## <a name="support-for-schema-information"></a>对架构信息的支持  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]通过扩展方法提供对 XSD 验证的支持<xref:System.Xml.Schema?displayProperty=fullName>命名空间。</xref:System.Xml.Schema?displayProperty=fullName> 你可以验证 XML 树是否符合 XSD。 你可以用架构验证后信息集 (PSVI) 填充 XML 树。 有关详细信息，请参阅[如何︰ 验证使用 XSD](http://msdn.microsoft.com/library/481a97fa-6e96-46f2-8c9a-415555fac33b)和<xref:System.Xml.Schema.Extensions>。</xref:System.Xml.Schema.Extensions>  
  
## <a name="see-also"></a>另请参阅  
 [入门 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/getting-started-linq-to-xml.md)
