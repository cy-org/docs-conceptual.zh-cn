---
title: "使用 XPathNavigator 修改 XML 数据 | Microsoft Docs"
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
ms.assetid: 03a7c5a1-b296-4af4-b209-043c958dc0a5
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 使用 XPathNavigator 修改 XML 数据
<xref:System.Xml.XPath.XPathNavigator> 类提供一组方法用于修改 XML 文档中的节点和值。  要使用这些方法，<xref:System.Xml.XPath.XPathNavigator> 对象必须可编辑，即其 <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 属性必须为 `true`。  
  
 可以编辑 XML 文档的 <xref:System.Xml.XPath.XPathNavigator> 对象由 <xref:System.Xml.XmlDocument> 类的 <xref:System.Xml.XmlDocument.CreateNavigator%2A> 方法创建。  由 <xref:System.Xml.XPath.XPathDocument> 类创建的 <xref:System.Xml.XPath.XPathNavigator> 对象是只读的，如果尝试使用由 <xref:System.Xml.XPath.XPathDocument> 对象创建的 <xref:System.Xml.XPath.XPathNavigator> 对象的编辑方法，将引发 <xref:System.NotSupportedException>。  
  
 有关创建可编辑的 <xref:System.Xml.XPath.XPathNavigator> 对象的更多信息，请参见[使用 XPathDocument 和 XmlDocument 读取 XML 数据](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)。  
  
## 修改节点  
 更改节点值的一种简单的方法是，使用 <xref:System.Xml.XPath.XPathNavigator> 类的 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 和 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 方法。  
  
 下表列出在不同节点类型上使用这些方法的结果。  
  
|<xref:System.Xml.XPath.XPathNodeType>|更改的数据|  
|---------------------------------------------------------------------------------------------------------------------------------------------|-----------|  
|<xref:System.Xml.XPath.XPathNodeType>|不支持。|  
|<xref:System.Xml.XPath.XPathNodeType>|元素的内容。|  
|<xref:System.Xml.XPath.XPathNodeType>|属性的值。|  
|<xref:System.Xml.XPath.XPathNodeType>|文本内容。|  
|<xref:System.Xml.XPath.XPathNodeType>|内容（不包括目标）。|  
|<xref:System.Xml.XPath.XPathNodeType>|注释的内容。|  
|<xref:System.Xml.XPath.XPathNodeType>|不受支持。|  
  
> [!NOTE]
>  不支持编辑 <xref:System.Xml.XPath.XPathNodeType> 节点或 <xref:System.Xml.XPath.XPathNodeType> 节点。  
  
 <xref:System.Xml.XPath.XPathNavigator> 类还提供一组方法，用于插入和移除节点。  有关在 XML 文档中插入和移除节点的更多信息，请参见[使用 XPathNavigator 插入 XML 数据](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)和[使用 XPathNavigator 移除 XML 数据](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)主题。  
  
### 修改非类型化的值  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 方法只需将作为参数传递的非类型化的 `string` 值作为 <xref:System.Xml.XPath.XPathNavigator> 对象当前所处的节点的值插入。  插入的值没有任何类型或不验证新值是否符合节点的类型（如果架构信息可用）。  
  
 在以下示例中，<xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 方法用于更新 `contosoBooks.xml` 文件中的所有 `price` 元素。  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 该示例使用 `contosoBooks.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### 修改类型化的值  
 如果节点的类型为 W3C XML 架构的简单类型，在设置值之前，将针对简单类型的各个方面检查通过 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 方法插入的新值。  如果新值不符合节点的类型（例如在类型为 `xs:positiveInteger` 的元素上设置值 `-1`），将引发异常。  
  
 以下示例尝试将 `contosoBooks.xml` 文件中第一个 `book` 元素的 `price` 元素的值更改为 <xref:System.DateTime> 值。  因为在 `contosoBooks.xsd` 文件中将 `price` 元素的 XML 架构类型定义为 `xs:decimal`，所以，这样做将引发异常。  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetTypedValue(DateTime.Now)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.SetTypedValue(DateTime.Now);  
```  
  
 该示例使用 `contosoBooks.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 该示例还使用 `contosoBooks.xsd` 作为输入。  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
#### 编辑强类型的 XML 数据的结果  
 <xref:System.Xml.XPath.XPathNavigator> 类使用 W3C XML 架构作为描述强类型 XML 的基础。  元素和属性可以基于对 W3C XML 架构文档的验证，使用类型信息添加批注。  可以包含其他元素或属性的元素称为复杂类型，而只能包含文本内容的元素称为简单类型。  
  
> [!NOTE]
>  属性只能具有简单类型。  
  
 如果元素或属性符合其类型定义特定的所有规则，将被认为架构有效。  具有简单类型 `xs:int` 的元素必须包含介于 \-2147483648 到 2147483647 之间的数值，才属于架构有效。  对于复杂类型，元素的架构有效性取决于其子元素和属性的架构有效性。  因此，如果元素符合其复杂类型定义，其所有子元素和属性也符合各自的类型定义。  同样，即使元素只有一个子元素或属性不符合其类型定义，或有效性未知，该元素也将无效或属于有效性未知。  
  
 假设元素的有效性取决于其子元素和属性的有效性，对任意一项的修改都会造成元素有效性的改变（如果元素以前有效）。  尤其是，如果插入、更新或删除了元素的子元素或属性，元素的有效性将变为未知。  此情况通过将元素的 <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> 属性的 <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> 属性设置 <xref:System.Xml.Schema.XmlSchemaValidity> 来表示。  另外，此结果将在 XML 文档中循环向上层叠，因为元素的父元素（及其父元素，依此类推）的有效性也将变为未知。  
  
 有关架构有效性以及 <xref:System.Xml.XPath.XPathNavigator> 类的更多信息，请参见[使用 XPathNavigator 验证架构](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)。  
  
### 修改属性  
 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 和 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 方法可以用于修改非类型化和类型化的属性节点以及“修改节点”一节中列出的其他节点类型。  
  
 以下示例更改 `books.xml` 文件中第一个 `book` 元素的 `genre` 属性值。  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
navigator.MoveToChild("book", String.Empty)  
navigator.MoveToAttribute("genre", String.Empty)  
  
navigator.SetValue("non-fiction")  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
navigator.MoveToChild("book", String.Empty);  
navigator.MoveToAttribute("genre", String.Empty);  
  
navigator.SetValue("non-fiction");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 有关 <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> 和 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 方法的更多信息，请参见“修改非类型化的值”和“修改类型化的值”小节。  
  
## InnerXml 和 OuterXml 属性  
 <xref:System.Xml.XPath.XPathNavigator> 类的 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 和 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 属性更改 <xref:System.Xml.XPath.XPathNavigator> 对象当前所处的节点的 XML 标记。  
  
 <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 属性更改 <xref:System.Xml.XPath.XPathNavigator> 对象当前所处的子节点以及给定 XML `string` 的已分析内容的 XML 标记。  同样，<xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 属性更改 <xref:System.Xml.XPath.XPathNavigator> 对象当前所处的子节点以及当前节点本身的 XML 标记。  
  
 以下示例使用 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 属性修改 `price` 元素的值，并在 `contosoBooks.xml` 文件中的第一个 `book` 元素上插入新的 `discount` 属性。  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml");  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>"  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>";  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 该示例使用 `contosoBooks.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
## 修改命名空间节点  
 在文档对象模型 \(DOM\) 中，将命名空间声明看做就好像是可以插入、更新和删除的常规属性。  <xref:System.Xml.XPath.XPathNavigator> 类不允许对命名空间节点执行此类操作，因为更改命名空间节点的值可能会更改元素和属性在命名空间节点范围内的标识，如以下示例中所示。  
  
```  
<root xmlns="http://www.contoso.com">  
    <child />  
</root>  
```  
  
 如果上面的 XML 示例通过以下方式更改，可以有效地为文档中的每个元素重命名，因为每个元素的命名空间 URI 的值已更改。  
  
```  
<root xmlns="urn:contoso.com">  
    <child />  
</root>  
```  
  
 <xref:System.Xml.XPath.XPathNavigator> 类允许插入与所插入范围的命名空间声明不冲突的命名空间节点。  在这种情况下，命名空间声明不是在 XML 文档中的较低范围声明，不会造成以下示例中所示的重命名情况。  
  
```  
<root xmlns:a="http://www.contoso.com">  
    <parent>  
        <a:child />  
    </parent>  
</root>  
```  
  
 如果上面的 XML 示例通过以下方式更改，命名空间声明将在 XML 文档中其他命名空间声明范围以下正确地传播。  
  
```  
<root xmlns:a="http://www.contoso.com">  
    <parent a:parent-id="1234" xmlns:a="http://www.contoso.com/parent-id">  
        <a:child xmlns:a="http://www.contoso.com/">  
    </parent>  
</root>  
```  
  
 在上面的 XML 示例中，在 `http://www.contoso.com/parent-id` 命名空间的 `parent` 元素上插入了属性 `a:parent-id`。  <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> 方法用于在位于 `parent` 元素时插入属性。  `http://www.contoso.com` 命名空间声明通过 <xref:System.Xml.XPath.XPathNavigator> 类自动插入，以保持 XML 文档其他部分的一致性。  
  
## 修改实体引用节点  
 <xref:System.Xml.XmlDocument> 对象中的实体引用节点是只读的，不能使用 <xref:System.Xml.XPath.XPathNavigator> 或 <xref:System.Xml.XmlNode> 类进行编辑。  如果尝试修改实体引用节点，将引发 <xref:System.InvalidOperationException>。  
  
## 修改 xsi:nil 节点  
 W3C XML 架构建议引入了元素可为零的概念。  如果元素可为零，元素可能会没有任何内容并且仍然有效。  元素可为零的概念与对象可为 `null` 的概念类似。  主要区别是 `null` 对象不能通过任何方式访问，而 `xsi:nil` 元素仍具有可以访问的属性，但是没有任何内容（子元素或文本）。  如果 XML 文档中的某个元素上存在值为 `true` 的 `xsi:nil` 属性，表示元素没有任何内容。  
  
 如果使用 <xref:System.Xml.XPath.XPathNavigator> 对象向 `xsi:nil` 属性值为 `true` 的有效元素中添加内容，其 `xsi:nil` 属性的值将设置为 `false`。  
  
> [!NOTE]
>  如果 `xsi:nil` 属性设置为 `false` 的元素的内容已删除，该属性的值不会更改为 `true`。  
  
## 保存 XML 文档  
 使用 <xref:System.Xml.XmlDocument> 类的方法保存本主题中所述的编辑方法对 <xref:System.Xml.XmlDocument> 对象的更改。  有关保存对 <xref:System.Xml.XmlDocument> 对象的更改的更多信息，请参见[保存和编写文档](../../../../docs/standard/data/xml/saving-and-writing-a-document.md)。  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [使用 XPathNavigator 插入 XML 数据](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)   
 [使用 XPathNavigator 移除 XML 数据](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)