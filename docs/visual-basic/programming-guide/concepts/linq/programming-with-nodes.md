---
title: "使用节点 (Visual Basic 中) 进行编程 |Microsoft 文档"
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
ms.assetid: d8422a9b-dd37-44a3-8aac-2237ed9561e0
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 52fb60b95b869a79900f84c2a1a7a6151bb5b58f
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="programming-with-nodes-visual-basic"></a>使用节点 (Visual Basic 中) 进行编程
需要编写 XML 编辑器、转换系统或报告编写器这类程序的 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 开发人员通常需要编写在比元素和属性更细的粒度下运行的程序。 开发人员通常需要在节点级别上工作，操作文本节点、处理指令和添加注释。 本主题提供有关在节点级别进行编程的一些详细信息。  
  
## <a name="node-details"></a>节点详细信息  
 在节点级别上工作的程序员需要了解有关编程的许多细节。  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>XDocument 的子节点的父属性设置为 Null  
 <xref:System.Xml.Linq.XObject.Parent%2A>属性包含父<xref:System.Xml.Linq.XElement>，不是父节点。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XObject.Parent%2A> 子节点<xref:System.Xml.Linq.XDocument>没有父<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> 它们的父级是文档中，因此<xref:System.Xml.Linq.XObject.Parent%2A>对这些节点的属性设置为 null。</xref:System.Xml.Linq.XObject.Parent%2A>  
  
 下面的示例演示这一操作：  
  
```vb  
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")  
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)  
Console.WriteLine(doc.Root.Parent Is Nothing)  
```  
  
 该示例产生下面的输出：  
  
```  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>可以存在相邻文本节点  
 在许多 XML 编程模型中，相邻的文本节点始终会合并到一起。 这有时也称为文本节点的规范化。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 不规范化文本节点。 如果向同一个元素添加两个文本节点，则会产生相邻文本节点。 但是，如果您将指定为一个字符串，而不是内容添加<xref:System.Xml.Linq.XText>节点，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]可能会将合并具有相邻的文本节点的字符串。</xref:System.Xml.Linq.XText>  
  
 下面的示例演示这一操作：  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
' This does not add a new text node.  
xmlTree.Add("new content")  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
'// This does add a new, adjacent text node.  
xmlTree.Add(New XText("more text"))  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
```  
  
 该示例产生下面的输出：  
  
```  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>可以存在空文本节点  
 在某些 XML 编程模型中，文本节点保证不包含空字符串。 原因是这种文本节点对 XML 的序列化没有影响。 但由于可以存在相邻文本节点这一相同的原因，如果您通过将文本节点的值设置为空字符串来移除文本节点中的文本，则不会删除文本节点本身。  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()  
  
' The following line does not cause the removal of the text node.  
textNode.Value = ""  
  
Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()  
Console.WriteLine(">>{0}<<", textNode2)  
```  
  
 该示例产生下面的输出：  
  
```  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>空文本节点影响序列化  
 如果一个元素仅包含一个空的子文本节点，则会用长标记语法序列化该元素：`<Child></Child>`。 如果一个元素不包含任何子节点，则会用短标记语法序列化该元素：`<Child />`。  
  
```vb  
Dim child1 As XElement = New XElement("Child1", _  
    New XText("") _  
)  
Dim child2 As XElement = New XElement("Child2")  
Console.WriteLine(child1)  
Console.WriteLine(child2)  
```  
  
 该示例产生下面的输出：  
  
```  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>命名空间是 LINQ to XML 树中的属性  
 即使命名空间声明与特性具有完全相同的语法，在某些编程接口（如 XSLT 和 XPath）中，也不会将命名空间声明视为属性。 但是，在[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]，命名空间存储为<xref:System.Xml.Linq.XAttribute>XML 树中的对象。</xref:System.Xml.Linq.XAttribute> 如果您循环访问包含命名空间声明的元素的属性，则会在返回的集合中看到作为一项列出的命名空间声明。  
  
 <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>属性指示属性是否为命名空间声明。</xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>  
  
```vb  
Dim root As XElement = _   
<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>  
For Each att As XAttribute In root.Attributes()  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _  
                      att.IsNamespaceDeclaration)  
Next  
```  
  
 该示例产生下面的输出：  
  
```  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>XPath 轴方法不返回 XDocument 的子空白  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]允许的子文本节点<xref:System.Xml.Linq.XDocument>，只要文本节点只能包含空白。</xref:System.Xml.Linq.XDocument> 但是，XPath 对象模型不包括空白作为子节点的一个文档，因此当遍历的子级<xref:System.Xml.Linq.XDocument>使用<xref:System.Xml.Linq.XContainer.Nodes%2A>轴，将返回空白文本节点。</xref:System.Xml.Linq.XContainer.Nodes%2A> </xref:System.Xml.Linq.XDocument> 但是，当您遍历的子级<xref:System.Xml.Linq.XDocument>使用 XPath 轴方法，空白文本节点将不会返回。</xref:System.Xml.Linq.XDocument>  
  
```vb  
' Create a document with some white space child nodes of the document.  
Dim root As XDocument = XDocument.Parse( _  
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _  
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _  
LoadOptions.PreserveWhitespace)  
  
' Count the white space child nodes using LINQ to XML.  
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())  
  
' Count the white space child nodes using XPathEvaluate.  
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)  
Console.WriteLine(nodes.OfType(Of XText)().Count())  
```  
  
 该示例产生下面的输出：  
  
```  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>XDeclaration 对象不是节点  
 当您循环访问的子节点<xref:System.Xml.Linq.XDocument>，则将看不到 XML 声明对象。</xref:System.Xml.Linq.XDocument> 它是文档的属性，不是文档的子节点。  
  
```vb  
Dim doc As XDocument = _  
<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
<Root/>  
  
doc.Save("Temp.xml")  
Console.WriteLine(File.ReadAllText("Temp.xml"))  
  
' This shows that there is only one child node of the document.  
Console.WriteLine(doc.Nodes().Count())  
```  
  
 该示例产生下面的输出：  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />  
1  
```  
  
## <a name="see-also"></a>另请参阅  
 [高级的 LINQ to XML 编程 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

