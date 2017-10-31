---
title: "Set 运算 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 2b06e822-e030-438f-9db7-ee402bd3a706
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
ms.openlocfilehash: e835737b388427445a15b6658c7d148801f29b79
ms.lasthandoff: 03/13/2017

---
# <a name="set-operations-visual-basic"></a>Set 运算 (Visual Basic)
LINQ 中的集运算是指生成基于存在相同或不同集合 （或集） 中的等效元素的结果集的查询操作。  
  
 下一节中列出了执行集合操作的标准查询运算符方法。  
  
## <a name="methods"></a>方法  
  
|方法名|描述|Visual Basic 查询表达式语法|更多信息|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Distinct|中删除重复的集合中的值。|`Distinct`|<xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName></xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName>|  
|不包括|返回的差集，这意味着第二个集合中不会出现一个集合中的元素。|不适用。|<xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Except%2A?displayProperty=fullName></xref:System.Linq.Queryable.Except%2A?displayProperty=fullName>|  
|相交|返回组重叠，这意味着每两个集合中显示的元素。|不适用。|<xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName></xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName>|  
|联合|返回并集，这意味着显示在上述两个集合的唯一元素。|不适用。|<xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Union%2A?displayProperty=fullName></xref:System.Linq.Queryable.Union%2A?displayProperty=fullName>|  
  
## <a name="comparison-of-set-operations"></a>集运算的比较  
  
### <a name="distinct"></a>Distinct  
 下图描绘了的行为<xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName>方法上的字符序列。</xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName> 返回的序列包含输入序列中的唯一元素。  
  
 ![显示 distinct （） 的行为的图。](../../../../csharp/programming-guide/concepts/linq/media/distinct.png "不同")  
  
### <a name="except"></a>不包括  
 下图描绘了<xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName>。</xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName>的行为 返回的序列仅包含元素的第一个输入序列中不在第二个输入序列中。  
  
 ![图形显示操作的图。](../../../../csharp/programming-guide/concepts/linq/media/except.png "Except")  
  
### <a name="intersect"></a>相交  
 下图描绘了<xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName>。</xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName>的行为 返回的序列包含的元素所共有的这两个输入序列。  
  
 ![显示两个序列的交集的图。](../../../../csharp/programming-guide/concepts/linq/media/intersect.png "相交")  
  
### <a name="union"></a>联合  
 下图描绘了 union 运算对两个序列的字符。 返回的序列中不包含这两个输入序列中的唯一元素。  
  
 ![显示两个序列的联合的图。](../../../../csharp/programming-guide/concepts/linq/media/union.png "Union")  
  
## <a name="query-expression-syntax-example"></a>查询表达式语法示例  
 下面的示例使用`Distinct`LINQ 查询以返回唯一的编号从整数列表中的子句。  
  
 [!code-vb[CsLINQSetOps #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/set-operations_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Distinct 子句](../../../../visual-basic/language-reference/queries/distinct-clause.md)   
 [如何︰ 组合和比较字符串集合 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md)   
 [如何︰ 查找两个列表 (LINQ) (Visual Basic 中) 之间的差集](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md)
