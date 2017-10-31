---
title: "XAttribute 类概述 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 7781580a-9583-4a1b-ae1e-91c5936eb0b1
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
ms.openlocfilehash: 1ce5f4be6006908b35057854f89432471fd9f06b
ms.lasthandoff: 03/13/2017

---
# <a name="xattribute-class-overview-visual-basic"></a>XAttribute 类概述 (Visual Basic)
属性是与元素关联的名称/值对。 <xref:System.Xml.Linq.XAttribute>类表示 XML 属性。</xref:System.Xml.Linq.XAttribute>  
  
## <a name="overview"></a>概述  
 使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中的属性，与使用元素非常相似。 它们的构造函数相似。 用于检索它们的集合的方法相似。 属性集合的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询表达式与元素集合的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询表达式看起来非常相似。  
  
 将属性添加到元素中的顺序会保留下来。 也就是说，当循环访问属性时，所见到的属性顺序与它们的添加顺序相同。  
  
## <a name="the-xattribute-constructor"></a>XAttribute 构造函数  
 下面的构造函数的<xref:System.Xml.Linq.XAttribute>类是将最常使用的一个︰</xref:System.Xml.Linq.XAttribute>  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`XAttribute(XName name, object content)`|创建<xref:System.Xml.Linq.XAttribute>对象。</xref:System.Xml.Linq.XAttribute> `name` 参数指定属性的名称；`content` 指定属性的内容。|  
  
### <a name="creating-an-element-with-an-attribute"></a>创建具有属性的元素  
 下面的代码演示一个包含属性在 Visual Basic 中使用 XML 文本的元素︰  
  
```vb  
Dim phone As XElement = <Phone Type="Home">555-555-5555</Phone>  
Console.WriteLine(phone)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>  
```  
  
### <a name="functional-construction-of-attributes"></a>属性的函数构造  
 您可以构造<xref:System.Xml.Linq.XAttribute>对象行的构造一致的<xref:System.Xml.Linq.XElement>对象，如下︰</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute>  
  
```vb  
Dim c As XElement = _  
    <Customers>  
        <Customer>  
            <Name>John Doe</Name>  
            <PhoneNumbers>  
                <Phone type="home">555-555-5555</Phone>  
                <Phone type="work">666-666-6666</Phone>  
            </PhoneNumbers>  
        </Customer>  
    </Customers>  
Console.WriteLine(c)  
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
 属性与元素之间有些区别。 <xref:System.Xml.Linq.XAttribute>对象不是 XML 树中的节点。</xref:System.Xml.Linq.XAttribute> 它们是与 XML 元素关联的名称/值对。 与文档对象模型 (DOM) 相比，这更加贴切地反映了 XML 结构。 尽管<xref:System.Xml.Linq.XAttribute>对象实际上不是节点在 XML 树中，使用<xref:System.Xml.Linq.XAttribute>对象是非常类似于使用<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XAttribute>  
  
 这一区别仅对编写在节点级使用 XML 树的代码的开发人员特别重要。 许多开发人员不会关心这种区别。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 编程概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
