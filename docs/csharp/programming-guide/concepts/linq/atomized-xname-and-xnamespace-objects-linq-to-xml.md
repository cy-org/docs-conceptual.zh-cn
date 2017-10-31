---
title: "原子化的 XName 和 XNamespace 对象 (LINQ to XML) (C#)"
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
ms.assetid: a5b21433-b49d-415c-b00e-bcbfb0d267d7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1731be2847e5e118340b93cd35205fc13ff9f75a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml-c"></a>原子化的 XName 和 XNamespace 对象 (LINQ to XML) (C#)
<xref:System.Xml.Linq.XName> 和 <xref:System.Xml.Linq.XNamespace> 对象进行了原子化；即，如果这两个对象包含相同的限定名，则它们将引用同一个对象。 这将提高查询性能：当比较两个原子化名称是否相等时，基础中间语言只需确定这两个引用是否指向同一个对象。 基础代码不必进行很耗费时间的字符串比较。  
  
## <a name="atomization-semantics"></a>原子化语义  
 原子化是指如果两个 <xref:System.Xml.Linq.XName> 对象具有相同的本地名称并且位于同一个命名空间中，则它们共享相同的实例。 同样，如果两个 <xref:System.Xml.Linq.XNamespace> 对象具有相同的命名空间 URI，则它们共享同一个实例。  
  
 对于启用原子化对象的类，该类的构造函数必须是私有的，而不是公共的。 这是因为如果构造函数是公共的，则您可以创建非原子化对象。 <xref:System.Xml.Linq.XName> 和 <xref:System.Xml.Linq.XNamespace> 类实现一个隐式转换运算符，以将字符串转换为 <xref:System.Xml.Linq.XName> 或 <xref:System.Xml.Linq.XNamespace>。 这是获取这些对象的实例的方式。 不能通过使用构造函数来获得实例，因为构造函数是不可访问的。  
  
 <xref:System.Xml.Linq.XName> 和 <xref:System.Xml.Linq.XNamespace> 还实现相等运算符和不相等运算符，以确定进行比较的两个对象是否引用相同的实例。  
  
## <a name="example"></a>示例  
 下面的代码创建一些 <xref:System.Xml.Linq.XElement> 对象，并演示相同的名称共享同一个实例。  
  
```csharp  
XElement r1 = new XElement("Root", "data1");  
XElement r2 = XElement.Parse("<Root>data2</Root>");  
  
if ((object)r1.Name == (object)r2.Name)  
    Console.WriteLine("r1 and r2 have names that refer to the same instance.");  
else  
    Console.WriteLine("Different");  
  
XName n = "Root";  
  
if ((object)n == (object)r1.Name)  
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.");  
else  
    Console.WriteLine("Different");  
```  
  
 该示例产生下面的输出：  
  
```  
r1 and r2 have names that refer to the same instance.  
The name of r1 and the name in 'n' refer to the same instance.  
```  
  
 如前面所述，原子化对象的好处是：当使用某个采用 <xref:System.Xml.Linq.XName> 作为参数的轴方法时，该轴方法只需确定这两个名称引用同一个实例来选择所需的元素。  
  
 下面的示例将 <xref:System.Xml.Linq.XName> 传递给 <xref:System.Xml.Linq.XContainer.Descendants%2A> 方法调用，该调用会由于使用原子化模式而获得更好的性能。  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("C1", 1),  
    new XElement("Z1",  
        new XElement("C1", 2),  
        new XElement("C1", 1)  
    )  
);  
  
var query = from e in root.Descendants("C1")  
            where (int)e == 1  
            select e;  
  
foreach (var z in query)  
    Console.WriteLine(z);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<C1>1</C1>  
<C1>1</C1>  
```  
  
## <a name="see-also"></a>另请参阅  
 [性能 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)

