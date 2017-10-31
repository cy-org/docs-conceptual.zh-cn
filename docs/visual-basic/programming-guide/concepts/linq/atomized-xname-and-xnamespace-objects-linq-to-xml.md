---
title: "原子化 XName 和 XNamespace 对象 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 21ee7585-7df9-40b4-8c76-a12bb5f29bb3
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b08f3116f5acb404cf2c33072ec31fbaada4e7cb
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017


---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml-visual-basic"></a>原子化 XName 和 XNamespace 对象 (LINQ to XML) (Visual Basic)
<xref:System.Xml.Linq.XName>和<xref:System.Xml.Linq.XNamespace>对象*原子化*; 也就是说，如果它们包含相同的限定的名，它们是指同一对象。</xref:System.Xml.Linq.XNamespace></xref:System.Xml.Linq.XName> 这将提高查询性能：当比较两个原子化名称是否相等时，基础中间语言只需确定这两个引用是否指向同一个对象。 基础代码不必进行很耗费时间的字符串比较。  
  
## <a name="atomization-semantics"></a>原子化语义  
 原子化是指如果两个<xref:System.Xml.Linq.XName>对象具有相同的本地名称和它们处于相同的命名空间，则它们共享同一个实例。</xref:System.Xml.Linq.XName> 同样，如果两个<xref:System.Xml.Linq.XNamespace>对象具有相同的命名空间 URI，则它们共享同一个实例。</xref:System.Xml.Linq.XNamespace>  
  
 对于启用原子化对象的类，该类的构造函数必须是私有的，而不是公共的。 这是因为如果构造函数是公共的，则您可以创建非原子化对象。 <xref:System.Xml.Linq.XName><xref:System.Xml.Linq.XNamespace>类实现一个隐式转换运算符将字符串转换<xref:System.Xml.Linq.XName>或<xref:System.Xml.Linq.XNamespace>.</xref:System.Xml.Linq.XNamespace></xref:System.Xml.Linq.XName></xref:System.Xml.Linq.XNamespace>和</xref:System.Xml.Linq.XName> 这是获取这些对象的实例的方式。 不能通过使用构造函数来获得实例，因为构造函数是不可访问的。  
  
 <xref:System.Xml.Linq.XName>和<xref:System.Xml.Linq.XNamespace>还实现相等和不相等运算符，以确定两个比较对象是否正在对同一实例的引用。</xref:System.Xml.Linq.XNamespace></xref:System.Xml.Linq.XName>  
  
## <a name="example"></a>示例  
 下面的代码创建一些<xref:System.Xml.Linq.XElement>对象，并演示相同的名称共享同一个实例。</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim r1 As New XElement("Root", "data1")  
Dim r2 As XElement = XElement.Parse("<Root>data2</Root>")  
  
If DirectCast(r1.Name, Object) = DirectCast(r2.Name, Object) Then  
    Console.WriteLine("r1 and r2 have names that refer to the same instance.")  
Else  
    Console.WriteLine("Different")  
End If  
  
Dim n As XName = "Root"  
  
If DirectCast(n, Object) = DirectCast(r1.Name, Object) Then  
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.")  
Else  
    Console.WriteLine("Different")  
End If  
```  
  
 该示例产生下面的输出：  
  
```  
r1 and r2 have names that refer to the same instance.  
The name of r1 and the name in 'n' refer to the same instance.  
```  
  
 使用采用的轴方法的一种时如前面所述，原子化对象的好处是︰<xref:System.Xml.Linq.XName>作为参数，该轴方法只须确定这两个名称引用同一个实例，来选择所需的元素。</xref:System.Xml.Linq.XName>  
  
 下面的示例传入<xref:System.Xml.Linq.XName>到<xref:System.Xml.Linq.XContainer.Descendants%2A>方法调用中，这样就会由于使用原子化模式而具有更好的性能。</xref:System.Xml.Linq.XContainer.Descendants%2A> </xref:System.Xml.Linq.XName>  
  
```vb  
Dim root As New XElement("Root", New XElement("C1", 1), New XElement("Z1", New XElement("C1", 2), New XElement("C1", 1)))  
  
Dim query = From e In root.Descendants("C1") Where CInt(e) = 1e  
  
For Each z As var In query  
    Console.WriteLine(z)  
Next  
```  
  
 该示例产生下面的输出：  
  
```xml  
<C1>1</C1>  
<C1>1</C1>  
```  
  
## <a name="see-also"></a>另请参阅  
 [性能 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)

