---
title: "比较 XPath 和 LINQ to XML1 |Microsoft 文档"
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
ms.assetid: c3fd07c1-6761-4e4b-8eb1-ddd780ed8d44
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e9601c51468fdf5adab8e521f8f89ee7f2e12869
ms.lasthandoff: 03/13/2017


---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>XPath 和 LINQ to XML 的比较
XPath 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 提供一些类似的功能。 二者都可用于查询 XML 树，返回诸如元素集合、属性集合、节点集合或者元素或属性的值等这样的结果。 但也有一些差异。  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a>XPath 和 LINQ to XML 之间的差异  
 XPath 不允许新类型的投影。 它只能从树中返回节点集合，而 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 可以执行查询并将对象图或 XML 树投影为新形状。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询包含更多功能并且比 XPath 表达式的功能强大得多。  
  
 XPath 表达式在字符串中孤立存在。 Visual Basic 编译器不能帮助分析 XPath 表达式在编译时。 与此相反，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]分析和可视设计基本编译器通过编译查询。 编译器能够捕捉许多查询错误。  
  
 XPath 结果不是强类型。 在许多情况下，XPath 表达式的计算结果是一个对象，并且该对象需要由开发人员确定属性类型并根据需要强制转换结果。 相比之下，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询生成的投影是强类型。  
  
## <a name="result-ordering"></a>结果排序  
 XPath 1.0 建议规定，作为 XPath 表达式计算结果的集合是无序的。  
  
 但在循环访问由 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] XPath 轴方法返回的集合时，集合中的节点将按文档顺序返回。 即使是在访问按反向文档顺序表示谓词的 XPath 轴（如 `preceding` 和 `preceding-sibling`）时，情况也如此。  
  
 与之相反，大部分[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]轴按文档顺序排列，但其中，两个返回集合<xref:System.Xml.Linq.XNode.Ancestors%2A>和<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>，按反向文档顺序返回集合。</xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> </xref:System.Xml.Linq.XNode.Ancestors%2A> 下表枚举各个轴并指示每个轴的集合顺序：  
  
|LINQ to XML 轴|订购|  
|----------------------|--------------|  
|XContainer.DescendantNodes|文档顺序|  
|XContainer.Descendants|文档顺序|  
|XContainer.Elements|文档顺序|  
|XContainer.Nodes|文档顺序|  
|XContainer.NodesAfterSelf|文档顺序|  
|XContainer.NodesBeforeSelf|文档顺序|  
|XElement.AncestorsAndSelf|反向文档顺序|  
|XElement.Attributes|文档顺序|  
|XElement.DescendantNodesAndSelf|文档顺序|  
|XElement.DescendantsAndSelf|文档顺序|  
|XNode.Ancestors|反向文档顺序|  
|XNode.ElementsAfterSelf|文档顺序|  
|XNode.ElementsBeforeSelf|文档顺序|  
|XNode.NodesAfterSelf|文档顺序|  
|XNode.NodesBeforeSelf|文档顺序|  
  
## <a name="positional-predicates"></a>位置谓词  
 在 XPath 表达式中，很多轴的位置谓词都按文档顺序表示，但是反向轴 `preceding`、`preceding-sibling`、`ancestor` 和 `ancestor-or-self` 则按反向文档顺序表示。 例如，XPath 表达式 `preceding-sibling::*[1]` 返回前面紧邻的同级。 即使最终结果集按文档顺序表示，情况也是这样。  
  
 相比之下，LINQ to XML 中的所有位置谓词始终按轴顺序表示。 例如，`anElement.ElementsBeforeSelf().ToList()[0]` 返回所查询元素的父级的第一个子元素，而不是前面紧邻的同级。 再例如：`anElement.Ancestors().ToList()[0]` 返回父元素。  
  
 请注意，上面的方法具体化整个集合。 这不是编写该查询的最有效方法。 以这种方式编写查询是为了演示位置谓词的行为。 更恰当的方式来编写相同的查询是使用<xref:System.Linq.Enumerable.First%2A>方法，如下所示︰ `anElement.ElementsBeforeSelf().First()`。</xref:System.Linq.Enumerable.First%2A>  
  
 如果要查找 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中的前面紧邻元素，则应编写下面的表达式：  
  
 `ElementsBeforeSelf().Last()`  
  
## <a name="performance-differences"></a>性能差异  
 使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中 XPath 功能的 XPath 查询的执行性能比 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询低。  
  
## <a name="comparison-of-composition"></a>撰写方式的比较  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询的撰写在某种程度上类似于 XPath 表达式的撰写，但其语法大不相同。  
  
 例如，如果名为 `customers` 的变量中有一个元素，并且您想在所有名为 `CompanyName` 的子级元素下查找名为 `Customer` 的孙级元素，则应编写如下所示的 XPath 表达式：  
  
```vb  
customers.XPathSelectElements("./Customer/CompanyName")  
```  
  
 等效的 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 查询是：  
  
```vb  
customers.Element("Customer").Elements("CompanyName")  
```  
  
 每个 XPath 轴都有一些相似处。  
  
|XPath 轴|LINQ to XML 轴|  
|----------------|----------------------|  
|子级（默认轴）|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>|  
|父级 (..)|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName></xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName>|  
|属性轴 (@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName>|  
|上级轴|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName>|  
|上级或自身轴|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName>|  
|后代轴 (//)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName>|  
|后代或自身|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName>|  
|后面同级|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName>|  
|前面同级|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName>|  
|后面|无直接等效项。|  
|前面|无直接等效项。|  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 针对 XPath 用户 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
