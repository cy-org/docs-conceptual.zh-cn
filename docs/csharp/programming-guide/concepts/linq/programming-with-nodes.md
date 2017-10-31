---
title: "使用节点进行编程 (C#)"
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
ms.assetid: c38df0f2-c805-431a-93ff-9103a4284c2f
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
ms.openlocfilehash: 6afa5c9ca5fdf4a8c64be826ead86e96aa94a446
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="programming-with-nodes-c"></a>使用节点进行编程 (C#)
需要编写 XML 编辑器、转换系统或报告编写器这类程序的 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 开发人员通常需要编写在比元素和属性更细的粒度下运行的程序。 开发人员通常需要在节点级别上工作，操作文本节点、处理指令和添加注释。 本主题提供有关在节点级别进行编程的一些详细信息。  
  
## <a name="node-details"></a>节点详细信息  
 在节点级别上工作的程序员需要了解有关编程的许多细节。  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>XDocument 的子节点的父属性设置为 Null  
 <xref:System.Xml.Linq.XObject.Parent%2A> 属性包含父 <xref:System.Xml.Linq.XElement>，而不是父节点。 <xref:System.Xml.Linq.XDocument> 的子节点没有父 <xref:System.Xml.Linq.XElement>。 它们的父级是文档，因此这些节点的 <xref:System.Xml.Linq.XObject.Parent%2A> 属性设置为 null。  
  
 下面的示例演示这一操作：  
  
```csharp  
XDocument doc = XDocument.Parse(@"<!-- a comment --><Root/>");  
Console.WriteLine(doc.Nodes().OfType<XComment>().First().Parent == null);  
Console.WriteLine(doc.Root.Parent == null);  
```  
  
 该示例产生下面的输出：  
  
```  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>可以存在相邻文本节点  
 在许多 XML 编程模型中，相邻的文本节点始终会合并到一起。 这有时也称为文本节点的规范化。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 不规范化文本节点。 如果向同一个元素添加两个文本节点，则会产生相邻文本节点。 但如果将指定内容添加为字符串而不是 <xref:System.Xml.Linq.XText> 节点，则 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 可能会将该字符串与相邻的文本节点合并在一起。  
  
 下面的示例演示这一操作：  
  
```csharp  
XElement xmlTree = new XElement("Root", "Content");  
  
Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());  
  
// this does not add a new text node  
xmlTree.Add("new content");  
Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());  
  
// this does add a new, adjacent text node  
xmlTree.Add(new XText("more text"));  
Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());  
```  
  
 该示例产生下面的输出：  
  
```  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>可以存在空文本节点  
 在某些 XML 编程模型中，文本节点保证不包含空字符串。 原因是这种文本节点对 XML 的序列化没有影响。 但由于可以存在相邻文本节点这一相同的原因，如果您通过将文本节点的值设置为空字符串来移除文本节点中的文本，则不会删除文本节点本身。  
  
```csharp  
XElement xmlTree = new XElement("Root", "Content");  
XText textNode = xmlTree.Nodes().OfType<XText>().First();  
  
// the following line does not cause the removal of the text node.  
textNode.Value = "";  
  
XText textNode2 = xmlTree.Nodes().OfType<XText>().First();  
Console.WriteLine(">>{0}<<", textNode2);   
```  
  
 该示例产生下面的输出：  
  
```  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>空文本节点影响序列化  
 如果一个元素仅包含一个空的子文本节点，则会用长标记语法序列化该元素：`<Child></Child>`。 如果一个元素不包含任何子节点，则会用短标记语法序列化该元素：`<Child />`。  
  
```csharp  
XElement child1 = new XElement("Child1",  
    new XText("")  
);  
XElement child2 = new XElement("Child2");  
Console.WriteLine(child1);  
Console.WriteLine(child2);   
```  
  
 该示例产生下面的输出：  
  
```xml  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>命名空间是 LINQ to XML 树中的属性  
 即使命名空间声明与特性具有完全相同的语法，在某些编程接口（如 XSLT 和 XPath）中，也不会将命名空间声明视为属性。 但在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中，命名空间存储为 XML 树中的 <xref:System.Xml.Linq.XAttribute> 对象。 如果您循环访问包含命名空间声明的元素的属性，则会在返回的集合中看到作为一项列出的命名空间声明。  
  
 <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A> 属性 (property) 指示某一属性 (attribute) 是否为命名空间声明。  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>");  
foreach (XAttribute att in root.Attributes())  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, att.IsNamespaceDeclaration);  
```  
  
 该示例产生下面的输出：  
  
```  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>XPath 轴方法不返回 XDocument 的子空白  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 允许 <xref:System.Xml.Linq.XDocument> 具有子文本节点，但这些文本节点只能包含空白。 但是，XPath 对象模型不包括空白作为文档的子节点，因此在使用 <xref:System.Xml.Linq.XDocument> 轴循环访问 <xref:System.Xml.Linq.XContainer.Nodes%2A> 的子级时，将返回空白文本节点。 但在使用 XPath 轴方法循环访问 <xref:System.Xml.Linq.XDocument> 的子级时，不会返回空白文本节点。  
  
```csharp  
// Create a document with some white space child nodes of the document.  
XDocument root = XDocument.Parse(  
@"<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
  
<Root/>  
  
<!--a comment-->  
", LoadOptions.PreserveWhitespace);  
  
// count the white space child nodes using LINQ to XML  
Console.WriteLine(root.Nodes().OfType<XText>().Count());  
  
// count the white space child nodes using XPathEvaluate  
Console.WriteLine(((IEnumerable)root.XPathEvaluate("text()")).OfType<XText>().Count());   
```  
  
 该示例产生下面的输出：  
  
```  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>XDeclaration 对象不是节点  
 在循环访问 <xref:System.Xml.Linq.XDocument> 的子节点时，将看不到 XML 声明对象。 它是文档的属性，不是文档的子节点。  
  
```csharp  
XDocument doc = new XDocument(  
    new XDeclaration("1.0", "utf-8", "yes"),  
    new XElement("Root")  
);  
doc.Save("Temp.xml");  
Console.WriteLine(File.ReadAllText("Temp.xml"));  
  
// this shows that there is only one child node of the document  
Console.WriteLine(doc.Nodes().Count());  
```  
  
 该示例产生下面的输出：  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />  
1  
```  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

