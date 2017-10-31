---
title: "XAttribute 类概述 (C#)"
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
ms.assetid: 5a630f24-f9ad-400e-831e-c14ebfc9e142
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
ms.openlocfilehash: fdac066fbd467768cedcf93f6258cbde0b6dd847
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="xattribute-class-overview-c"></a>XAttribute 类概述 (C#)
属性是与元素关联的名称/值对。 <xref:System.Xml.Linq.XAttribute> 类表示 XML 属性。  
  
## <a name="overview"></a>概述  
 使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的属性，与使用元素非常相似。 它们的构造函数相似。 用于检索它们的集合的方法相似。 属性集合的 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式与元素集合的 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式看起来非常相似。  
  
 将属性添加到元素中的顺序会保留下来。 也就是说，当循环访问属性时，所见到的属性顺序与它们的添加顺序相同。  
  
## <a name="the-xattribute-constructor"></a>XAttribute 构造函数  
 下面的 <xref:System.Xml.Linq.XAttribute> 类构造函数是您将最常使用的构造函数之一：  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`XAttribute(XName name, object content)`|创建一个 <xref:System.Xml.Linq.XAttribute> 对象。 `name` 参数指定属性的名称；`content` 指定属性的内容。|  
  
### <a name="creating-an-element-with-an-attribute"></a>创建具有属性的元素  
 下面的代码演示创建包含属性的元素的常见任务：  
  
```csharp  
XElement phone = new XElement("Phone",  
    new XAttribute("Type", "Home"),  
    "555-555-5555");  
Console.WriteLine(phone);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>  
```  
  
### <a name="functional-construction-of-attributes"></a>属性的函数构造  
 可以构造与 <xref:System.Xml.Linq.XAttribute> 对象的构造一致的 <xref:System.Xml.Linq.XElement> 对象，如下所示：  
  
```csharp  
XElement c = new XElement("Customers",  
    new XElement("Customer",  
        new XElement("Name", "John Doe"),  
        new XElement("PhoneNumbers",  
            new XElement("Phone",  
                new XAttribute("type", "home"),  
                "555-555-5555"),  
            new XElement("Phone",  
                new XAttribute("type", "work"),  
                "666-666-6666")  
        )  
    )  
);  
Console.WriteLine(c);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Customers>  
  <Customer>  
    <Name>John Doe</Name>  
    <PhoneNumbers>  
      <Phone type="home">555-555-5555</Phone>  
      <Phone type="work">666-666-6666</Phone>  
    </PhoneNumbers>  
  </Customer>  
</Customers>  
```  
  
### <a name="attributes-are-not-nodes"></a>属性不是节点  
 属性与元素之间有些区别。 <xref:System.Xml.Linq.XAttribute> 对象不是 XML 树中的节点。 它们是与 XML 元素关联的名称/值对。 与文档对象模型 (DOM) 相比，这更加贴切地反映了 XML 结构。 虽然 <xref:System.Xml.Linq.XAttribute> 对象实际上不是 XML 树的节点，但使用 <xref:System.Xml.Linq.XAttribute> 对象与使用 <xref:System.Xml.Linq.XElement> 对象非常相似。  
  
 这一区别仅对编写在节点级使用 XML 树的代码的开发人员特别重要。 许多开发人员不会关心这种区别。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to XML 编程概述 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)

