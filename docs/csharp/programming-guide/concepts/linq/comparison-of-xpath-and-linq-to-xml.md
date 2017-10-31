---
title: "XPath 和 LINQ to XML 的比较 2"
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
ms.assetid: 87d361b1-daa9-4fd4-a53a-cbfa40111ad3
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a0b24eeeb79651f69178fa4e9c2e4a3359434556
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>XPath 和 LINQ to XML 的比较
XPath 和 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 提供一些类似的功能。 二者都可用于查询 XML 树，返回诸如元素集合、属性集合、节点集合或者元素或属性的值等这样的结果。 但也有一些差异。  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a>XPath 和 LINQ to XML 之间的差异  
 XPath 不允许新类型的投影。 它只能从树中返回节点集合，而 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 可以执行查询并将对象图或 XML 树投影为新形状。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询包含更多功能并且比 XPath 表达式的功能强大得多。  
  
 XPath 表达式在字符串中孤立存在。 C# 编译器无法在编译时帮助分析 XPath 表达式。 相反，C# 编译器可以分析和编译 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询。 编译器能够捕捉许多查询错误。  
  
 XPath 结果不是强类型。 在许多情况下，XPath 表达式的计算结果是一个对象，并且该对象需要由开发人员确定属性类型并根据需要强制转换结果。 相比之下，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询生成的投影是强类型。  
  
## <a name="result-ordering"></a>结果排序  
 XPath 1.0 建议规定，作为 XPath 表达式计算结果的集合是无序的。  
  
 但在循环访问由 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] XPath 轴方法返回的集合时，集合中的节点将按文档顺序返回。 即使是在访问按反向文档顺序表示谓词的 XPath 轴（如 `preceding` 和 `preceding-sibling`）时，情况也如此。  
  
 相比之下，多数 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 轴都按文档顺序返回集合，但其中 <xref:System.Xml.Linq.XNode.Ancestors%2A> 和 <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> 两个轴按反向文档顺序返回集合。 下表枚举各个轴并指示每个轴的集合顺序：  
  
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
  
 请注意，上面的方法具体化整个集合。 这不是编写该查询的最有效方法。 以这种方式编写查询是为了演示位置谓词的行为。 编写同一查询的更恰当的方式是使用 <xref:System.Linq.Enumerable.First%2A> 方法，如下所示：`anElement.ElementsBeforeSelf().First()`。  
  
 如果要查找 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的前面紧邻元素，则应编写下面的表达式：  
  
 `ElementsBeforeSelf().Last()`  
  
## <a name="performance-differences"></a>性能差异  
 使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中 XPath 功能的 XPath 查询的执行性能比 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询低。  
  
## <a name="comparison-of-composition"></a>撰写方式的比较  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询的撰写在某种程度上类似于 XPath 表达式的撰写，但其语法大不相同。  
  
 例如，如果名为 `customers` 的变量中有一个元素，并且您想在所有名为 `CompanyName` 的子级元素下查找名为 `Customer` 的孙级元素，则应编写如下所示的 XPath 表达式：  
  
```csharp  
customers.XPathSelectElements("./Customer/CompanyName");  
```  
  
 等效的 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询是：  
  
```csharp  
customers.Element("Customer").Elements("CompanyName");  
```  
  
 每个 XPath 轴都有一些相似处。  
  
|XPath 轴|LINQ to XML 轴|  
|----------------|----------------------|  
|子级（默认轴）|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|  
|父级 (..)|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=nameWithType>|  
|属性轴 (@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|  
|上级轴|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|  
|上级或自身轴|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|  
|后代轴 (//)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=nameWithType>|  
|后代或自身|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=nameWithType>|  
|后面同级|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=nameWithType>|  
|前面同级|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType><br /><br /> 或<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=nameWithType>|  
|后面|无直接等效项。|  
|前面|无直接等效项。|  
  
## <a name="see-also"></a>另请参阅  
 [针对 XPath 用户的 LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)

