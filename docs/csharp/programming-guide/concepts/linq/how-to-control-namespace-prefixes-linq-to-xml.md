---
title: "如何：控制命名空间前缀 (C#) (LINQ to XML)"
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
ms.assetid: 64de5186-b81a-4ddd-8327-8693df59a01b
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
ms.openlocfilehash: 1e56dcf74725940019cda1bf340b2f3ac4e1f6c4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-control-namespace-prefixes-c-linq-to-xml"></a>如何：控制命名空间前缀 (C#) (LINQ to XML)
本主题介绍在序列化 XML 树时如何控制命名空间前缀。  
  
 在很多情况下，不需要控制命名空间前缀。  
  
 但是，某些 XML 编程工具需要命名空间前缀的特定控制。 例如，您可能正在操作 XSLT 样式表或 XAML 文档，其中包含引用特定命名空间前缀的嵌入式 XPath 表达式，在这种情况下，一定要使用这些特定前缀对文档进行序列化。  
  
 这是控制命名空间前缀的最常见的原因。  
  
 需要控制命名空间前缀的另一个常见原因是：您希望用户手动编辑 XML 文档，而且您希望创建方便用户键入的命名空间前缀。 例如，您可能正在生成 XSD 文档。 架构约定建议您使用 `xs` 或 `xsd` 作为架构命名空间的前缀。  
  
 若要控制命名空间前缀，请插入声明命名空间的属性。 如果使用特定前缀声明命名空间，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 将在序列化时尝试接受此命名空间前缀。  
  
 若要创建一个声明具有前缀的命名空间的属性，请创建一个属性，该属性的名称的命名空间为 <xref:System.Xml.Linq.XNamespace.Xmlns%2A>，该属性的名称为命名空间前缀。 该属性的值即是命名空间的 URI。  
  
## <a name="example"></a>示例  
 本示例声明两个命名空间。 它指定 `http://www.adventure-works.com` 命名空间具有 `aw` 前缀，`www.fourthcoffee.com` 命名空间具有 `fc` 前缀。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 命名空间 (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)

