---
title: "LINQ to XML 针对 XPath 用户 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 0e64911c-a7cc-4c20-b927-ca99078b5656
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 376e7d67edf1719dc1a020974b38e3600831d660
ms.lasthandoff: 03/13/2017


---
# <a name="linq-to-xml-for-xpath-users-visual-basic"></a>LINQ to XML 针对 XPath 用户 (Visual Basic)
这组主题演示很多 XPath 表达式及其 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 等效表达式。  
  
 所有示例都使用中的 XPath 功能[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]，可供<xref:System.Xml.XPath.Extensions?displayProperty=fullName>。</xref:System.Xml.XPath.Extensions?displayProperty=fullName>中的扩展方法 这些示例既执行 XPath 表达式也执行 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 表达式。 然后，每个示例都对这两种查询的结果进行比较，验证 XPath 表达式与 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询的功能等效性。 由于这两种类型的查询都从相同的 XML 树返回节点，因此查询结果的比较是使用引用标识进行的。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[XPath 和 LINQ to XML 的比较](../../../../visual-basic/programming-guide/concepts/linq/comparison-of-xpath-and-linq-to-xml.md)|概述 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的异同。|  
|[如何︰ 查找子元素 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-child-element-xpath-linq-to-xml.md)|比较 XPath 子元素轴与[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]<xref:System.Xml.Linq.XContainer.Element%2A>方法。</xref:System.Xml.Linq.XContainer.Element%2A><br /><br /> 关联的 XPath 表达式为：`"DeliveryNotes"`。|  
|[如何︰ 查找子元素 (XPATH-LINQ to XML) 的列表 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-list-of-child-elements-xpath-linq-to-xml.md)|比较 XPath 子元素轴与[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]<xref:System.Xml.Linq.XContainer.Elements%2A>轴。</xref:System.Xml.Linq.XContainer.Elements%2A><br /><br /> 关联的 XPath 表达式为：`"./*"`|  
|[如何︰ 查找根元素 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-root-element-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 获取根元素。<br /><br /> 关联的 XPath 表达式为：`"/PurchaseOrders"`|  
|[如何︰ 查找子代元素 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-descendant-elements-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 获取具有特定名称的子代元素。<br /><br /> 关联的 XPath 表达式为：`"//Name"`|  
|[如何︰ 筛选特性 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-an-attribute-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 获取子代元素，这些子代元素具有指定的名称，并具有一个带指定值的属性。<br /><br /> 关联的 XPath 表达式为：`".//Address[@Type='Shipping']"`|  
|[如何︰ 查找相关的元素 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-related-elements-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 在由其他元素的值所引用的属性上获取元素选择。<br /><br /> 关联的 XPath 表达式为：`".//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]"`|  
|[如何︰ 查找 Namespace (XPATH-LINQ to XML) 中的元素 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-elements-in-a-namespace.md)|比较 XPath 使用<xref:System.Xml.XmlNamespaceManager>类[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]<xref:System.Xml.Linq.XName.Namespace%2A>属性<xref:System.Xml.Linq.XName>类中的用于处理 XML 命名空间。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XName.Namespace%2A> </xref:System.Xml.XmlNamespaceManager><br /><br /> 关联的 XPath 表达式为：`"./aw:*"`|  
|[如何︰ 查找前面的同级 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-preceding-siblings-xpath-linq-to-xml.md)|比较 XPath`preceding-sibling`轴与[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]子<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>轴。</xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName><br /><br /> 关联的 XPath 表达式为：`"preceding-sibling::*"`|  
|[如何︰ 查找子元素 (XPATH-LINQ to XML) 的子代 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-descendants-of-a-child-element-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 获取具有特定名称的子元素的子代元素。<br /><br /> 关联的 XPath 表达式为：`"./Paragraph//Text/text()"`|  
|[如何︰ 查找两个位置路径 (XPATH-LINQ to XML) 的并集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-a-union-of-two-location-paths-xpath.md)|比较使用 union 运算符， `&#124;`，与 XPath 中<xref:System.Linq.Enumerable.Concat%2A>中的标准查询运算符[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]。</xref:System.Linq.Enumerable.Concat%2A><br /><br /> 关联的 XPath 表达式为：`"//Category&#124;//Price"`|  
|[如何︰ 查找同级节点 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-sibling-nodes-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查找所有具有特定名称的节点同级。<br /><br /> 关联的 XPath 表达式为：`"../Book"`|  
|[如何︰ 查找父级 (XPATH-LINQ to XML) 的属性 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-an-attribute-of-the-parent-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 定位到父元素并查找关联的属性。<br /><br /> 关联的 XPath 表达式为：`"../@id"`|  
|[如何︰ 查找具有特定名称 (XPATH-LINQ to XML) 的同级的特性 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-attributes-of-siblings-with-a-specific-name.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查找上下文节点的同级的特定属性。<br /><br /> 关联的 XPath 表达式为：`"``../Book/@id``"`|  
|[如何︰ 查找具有特定特性 (XPATH-LINQ to XML) 的元素 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-elements-with-a-specific-attribute.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查找所有包含特定属性的元素。<br /><br /> 关联的 XPath 表达式为：`"./*[@Select]"`|  
|[如何︰ 查找子元素 (XPATH-LINQ to XML) 的位置对基于 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-child-elements-based-on-position.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 根据元素的相对位置查找元素。<br /><br /> 关联的 XPath 表达式为：`"Test[position() >= 2 and position() <= 4]"`|  
|[如何︰ 查找前面紧邻的同级 (XPATH-LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml.md)|比较如何使用 XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查找节点前面紧邻的同级。<br /><br /> 关联的 XPath 表达式为：`"preceding-sibling::*[1]"`|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.XPath?displayProperty=fullName></xref:System.Xml.XPath?displayProperty=fullName>   
 [查询 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/querying-xml-trees.md)   
 [使用 XPath 数据模型处理 XML 数据](http://msdn.microsoft.com/library/536c6fce-1453-4654-9c72-bca54d47e081)
