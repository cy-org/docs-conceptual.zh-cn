---
title: "LINQ to XML 轴 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: ecd3bd00-28e5-4517-a59f-53bff39fd478
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
ms.openlocfilehash: 4d6466a78c3a8e9d21e30f2d3cf8a49ed89dafbf
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-axes-visual-basic"></a>LINQ to XML 轴 (Visual Basic)
创建 XML 树或将 XML 文档加载到 XML 树之后，可以进行查询，从而查找元素和属性并检索它们的值。  
  
 在编写查询之前，必须了解 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 轴。 有两类轴方法︰ 第一类，是调用单个方法<xref:System.Xml.Linq.XElement>对象，<xref:System.Xml.Linq.XDocument>对象，或<xref:System.Xml.Linq.XNode>对象。</xref:System.Xml.Linq.XNode> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 这些方法对单个对象操作，返回的集合<xref:System.Xml.Linq.XElement>， <xref:System.Xml.Linq.XAttribute>，或<xref:System.Xml.Linq.XNode>对象。</xref:System.Xml.Linq.XNode> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> 第二类，是对集合操作并返回集合的扩展方法。 这些扩展方法可以：枚举源集合，在集合的每一项上调用适当的轴方法，将结果串联起来。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[LINQ to XML 轴概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|介绍轴的定义，并说明如何在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询的上下文中使用轴。|  
|[如何︰ 检索元素 (LINQ to XML) 的集合 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|引入了<xref:System.Xml.Linq.XContainer.Elements%2A>方法。</xref:System.Xml.Linq.XContainer.Elements%2A> 此方法检索元素的子元素集合。|  
|[如何︰ 检索元素 (LINQ to XML) 的值 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|演示如何获取元素的值。|  
|[如何︰ 筛选元素名称 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|演示如何在使用轴时筛选元素名称。|  
|[如何︰ 链接轴方法调用 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|演示如何将调用链接到轴方法。|  
|[如何︰ 检索单个子元素 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|演示在给定子元素标记名的情况下，如何检索元素的单个子元素。|  
|[如何︰ 检索特性 (LINQ to XML) 的集合 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|引入了<xref:System.Xml.Linq.XElement.Attributes%2A>方法。</xref:System.Xml.Linq.XElement.Attributes%2A> 此方法检索元素的属性。|  
|[如何︰ 检索单个特性 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|演示在给定属性名称的情况下，如何检索元素的单个属性。|  
|[如何︰ 检索特性 (LINQ to XML) 的值 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|演示如何获取属性的值。|  
|[如何︰ 检索浅值的元素 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|演示如何检索元素的浅值。|  
|[在 Visual Basic (LINQ to XML) 中语言集成的轴](../../../../visual-basic/programming-guide/concepts/linq/language-integrated-axes.md)|总结了[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]集成轴。|  
  
## <a name="see-also"></a>另请参阅  
 [编程指南 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
