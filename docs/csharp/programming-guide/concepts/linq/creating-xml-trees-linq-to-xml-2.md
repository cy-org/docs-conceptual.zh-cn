---
title: "在 C# 中创建 XML 树 (LINQ to XML)"
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
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
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
ms.openlocfilehash: ac95fcf49736b554c8a3d4d0061f63b3ac4d3f65
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-xml-trees-in-c-linq-to-xml"></a>在 C# 中创建 XML 树 (LINQ to XML)
本节提供有关使用 C# 来创建 XML 树的信息。  
  
 有关使用 LINQ 查询结果作为 <xref:System.Xml.Linq.XElement> 内容的信息，请参阅[功能构造 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md)。  
  
## <a name="constructing-elements"></a>构造元素  
 通过 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XAttribute> 构造函数的签名，可以将元素或属性的内容作为参数传递到构造函数。 由于其中一个构造函数使用可变数目的参数，因此可以传递任意数目的子元素。 当然，这些子元素中的每一个都可以包含它们自己的子元素。 对任意元素，可以添加任意多个属性。  
  
 在添加 <xref:System.Xml.Linq.XNode>（包括 <xref:System.Xml.Linq.XElement>）或 <xref:System.Xml.Linq.XAttribute> 对象时，如果新内容没有父级，则直接将这些对象附加到 XML 树中。 如果新内容已经有父级，并且是另一 XML 树的一部分，则克隆新内容，并将新克隆的内容附加到 XML 树。 本主题最后一个示例对此进行了演示。  
  
 若要创建 `contacts`<xref:System.Xml.Linq.XElement>，可以使用下面的代码：  
  
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
  
 如果正确缩进，则构造 <xref:System.Xml.Linq.XElement> 对象的代码十分类似于基础 XML 的结构。  
  
## <a name="xelement-constructors"></a>XElement 构造函数  
 <xref:System.Xml.Linq.XElement> 类使用下面的构造函数用于函数构造。 请注意，对于 <xref:System.Xml.Linq.XElement>，存在其他一些构造函数，但是由于它们不用于函数构造，因此没有在此列出。  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`XElement(XName name, object content)`|创建 <xref:System.Xml.Linq.XElement>。 `name` 参数指定元素的名称；`content` 指定元素的内容。|  
|`XElement(XName name)`|创建一个 <xref:System.Xml.Linq.XElement>，其 <xref:System.Xml.Linq.XName> 初始化为指定名称。|  
|`XElement(XName name, params object[] content)`|创建一个 <xref:System.Xml.Linq.XElement>，其 <xref:System.Xml.Linq.XName> 初始化为指定名称。 从参数列表的内容创建属性和/或子元素。|  
  
 `content` 参数极其灵活。 它支持作为 <xref:System.Xml.Linq.XElement> 的有效子对象的任何类型的对象。 下面的规则适用于在此参数中传递的不同类型的对象：  
  
-   字符串添加为文本内容。  
  
-   <xref:System.Xml.Linq.XElement> 添加为子元素。  
  
-   <xref:System.Xml.Linq.XAttribute> 添加为属性。  
  
-   <xref:System.Xml.Linq.XProcessingInstruction>、<xref:System.Xml.Linq.XComment> 或 <xref:System.Xml.Linq.XText> 添加为子内容。  
  
-   枚举 <xref:System.Collections.IEnumerable>，并且这些规则递归应用于结果。  
  
-   对任何其他类型，调用其 `ToString` 方法，结果添加为文本内容。  
  
### <a name="creating-an-xelement-with-content"></a>创建包含内容的 XElement  
 可以使用单个方法调用来创建一个包含简单内容的 <xref:System.Xml.Linq.XElement>。 为此，请指定内容作为第二个参数，如下所示：  
  
```csharp  
XElement n = new XElement("Customer", "Adventure Works");  
Console.WriteLine(n);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
 可以将任意类型的对象作为内容进行传递。 例如，下面的代码创建一个包含浮点数作为内容的元素：  
  
```csharp  
XElement n = new XElement("Cost", 324.50);  
Console.WriteLine(n);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Cost>324.5</Cost>  
```  
  
 该浮点数被装箱并传递给构造函数。 装箱的数字转换为字符串，然后用作元素的内容。  
  
### <a name="creating-an-xelement-with-a-child-element"></a>创建具有子元素的 XElement  
 如果传递 <xref:System.Xml.Linq.XElement> 类的一个实例作为内容参数，则构造函数将创建一个具有子元素的元素：  
  
```csharp  
XElement shippingUnit = new XElement("ShippingUnit",  
    new XElement("Cost", 324.50)  
);  
Console.WriteLine(shippingUnit);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<ShippingUnit>  
  <Cost>324.5</Cost>  
</ShippingUnit>  
```  
  
### <a name="creating-an-xelement-with-multiple-child-elements"></a>创建具有多个子元素的 XElement  
 可以传递多个 <xref:System.Xml.Linq.XElement> 对象作为内容。 每个 <xref:System.Xml.Linq.XElement> 对象都作为子元素包含进来。  
  
```csharp  
XElement address = new XElement("Address",  
    new XElement("Street1", "123 Main St"),  
    new XElement("City", "Mercer Island"),  
    new XElement("State", "WA"),  
    new XElement("Postal", "68042")  
);  
Console.WriteLine(address);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Address>  
  <Street1>123 Main St</Street1>  
  <City>Mercer Island</City>  
  <State>WA</State>  
  <Postal>68042</Postal>  
</Address>  
```  
  
 将上面的示例进行扩展，可以创建整个 XML 树，如下所示：  
  
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
Console.WriteLine(contacts);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Contacts>  
  <Contact>  
    <Name>Patrick Hines</Name>  
    <Phone>206-555-0144</Phone>  
    <Address>  
      <Street1>123 Main St</Street1>  
      <City>Mercer Island</City>  
      <State>WA</State>  
      <Postal>68042</Postal>  
    </Address>  
  </Contact>  
</Contacts>  
```  
  
### <a name="creating-an-empty-element"></a>创建空元素  
 若要创建空 <xref:System.Xml.Linq.XElement>，请不要将任何内容传递给构造函数。 下面的示例创建一个空元素：  
  
```csharp  
XElement n = new XElement("Customer");  
Console.WriteLine(n);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Customer />  
```  
  
### <a name="attaching-vs-cloning"></a>附加与克隆  
 前面提到，在添加 <xref:System.Xml.Linq.XNode>（包括 <xref:System.Xml.Linq.XElement>）或 <xref:System.Xml.Linq.XAttribute> 对象时，如果新内容没有父级，则直接将这些对象附加到 XML 树。 如果新内容已经有父级，并且是另一 XML 树的一部分，则克隆新内容，并将新克隆的内容附加到 XML 树。  
  
```csharp  
// Create a tree with a child element.  
XElement xmlTree1 = new XElement("Root",  
    new XElement("Child1", 1)  
);  
  
// Create an element that is not parented.  
XElement child2 = new XElement("Child2", 2);  
  
// Create a tree and add Child1 and Child2 to it.  
XElement xmlTree2 = new XElement("Root",  
    xmlTree1.Element("Child1"),  
    child2  
);  
  
// Compare Child1 identity.  
Console.WriteLine("Child1 was {0}",  
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?  
    "attached" : "cloned");  
  
// Compare Child2 identity.  
Console.WriteLine("Child2 was {0}",  
    child2 == xmlTree2.Element("Child2") ?  
    "attached" : "cloned");  
```  
  
 该示例产生下面的输出：  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)

