---
title: "LINQ to XML 轴概述 (C#)"
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
ms.assetid: 516792fb-461d-40a8-8a50-9993a51258fc
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: fdd4e6ffc17bc2c39d0dbeadbba955aacfe02dd9
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-xml-axes-overview-c"></a>LINQ to XML 轴概述 (C#)
创建 XML 树或将 XML 文档加载到 XML 树之后，可以进行查询，从而查找元素和属性并检索它们的值。 通过*轴方法*（也叫做*轴*）来检索集合。 一些轴就是 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 类中返回 <xref:System.Collections.Generic.IEnumerable%601> 集合的方法。 另一些轴是 <xref:System.Xml.Linq.Extensions> 类中的扩展方法。 实现为扩展方法的轴对集合进行操作，然后返回集合。  
  
 如同 [XElement 类概述](http://msdn.microsoft.com/library/d35180fe-7016-4895-9bfc-ba1e3f7875ec)中所述，<xref:System.Xml.Linq.XElement> 对象表示单个元素节点。 元素的内容可以是复杂的（有时称为结构化内容），也可以是简单元素。 简单元素可以是空的，也可以包含值。 如果节点包含结构化内容，则可以使用各种轴方法来检索子代元素的枚举。 最常使用的轴方法是 <xref:System.Xml.Linq.XContainer.Elements%2A> 和 <xref:System.Xml.Linq.XContainer.Descendants%2A>。  
  
 除了返回集合的轴方法之外，还有两个方法会在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询中经常用到。 <xref:System.Xml.Linq.XContainer.Element%2A> 方法返回单个 <xref:System.Xml.Linq.XElement>。 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法返回单个 <xref:System.Xml.Linq.XAttribute>。  
  
 对于很多应用来说，[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询提供了检查树、从树中提取数据以及转换树的最有效的方法。 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询对实现 <xref:System.Collections.Generic.IEnumerable%601> 的对象进行操作，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 轴返回 <xref:System.Xml.Linq.XElement> 集合的 <xref:System.Collections.Generic.IEnumerable%601>，以及 <xref:System.Xml.Linq.XAttribute> 集合的 <xref:System.Collections.Generic.IEnumerable%601>。 需要使用这些集合来执行查询。  
  
 除了检索元素和属性集合的轴方法之外，还有一些轴方法可以十分详尽地循环访问树。 例如，可以处理树的节点，而不是处理元素和属性。 节点比元素和属性有更细的粒度。 处理节点时，可以检查 XML 注释、文本节点、处理指令以及其他方面。 该功能很重要，例如对正在编写字处理器并希望将文档保存为 XML 的用户非常有用。 但是，大部分 XML 程序员主要关心的是元素、属性和它们的值。  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>用于检索元素集合的方法  
 下面是 <xref:System.Xml.Linq.XElement> 类（或其基类）的方法汇总，您可以对 <xref:System.Xml.Linq.XElement> 调用这些方法以返回元素集合。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|返回此元素的上级的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回上级的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，这些上级具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>|返回此元素的子代的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回子代的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，这些子代具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|返回此元素的子元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回子元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，这些子元素具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType>|返回此元素之后的元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回此元素之后的元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，此元素之后的这些元素具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType>|返回此元素之前的元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回此元素之前的元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，此元素之前的这些元素具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|返回此元素及其上级的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，这些元素具有指定的 <xref:System.Xml.Linq.XName>。|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType>|返回此元素及其子代的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>。 重载方法返回元素的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，这些元素具有指定的 <xref:System.Xml.Linq.XName>。|  
  
## <a name="method-for-retrieving-a-single-element"></a>用于检索单个元素的方法  
 下面的方法从 <xref:System.Xml.Linq.XElement> 对象中检索单个子级。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=nameWithType>|返回具有指定 <xref:System.Xml.Linq.XElement> 的第一个子 <xref:System.Xml.Linq.XName> 对象。|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>用于检索属性集合的方法  
 下面的方法从 <xref:System.Xml.Linq.XElement> 对象中检索属性。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|返回所有属性的 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XAttribute>。|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>用于检索单个属性的方法  
 下面的方法从 <xref:System.Xml.Linq.XElement> 对象中检索单个属性。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType>|返回具有指定 <xref:System.Xml.Linq.XAttribute> 的 <xref:System.Xml.Linq.XName>。|  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 轴 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)

