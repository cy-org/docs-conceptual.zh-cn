---
title: "限定符操作 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: ae1a2b73-503c-4f4b-a3fd-31b5adbee67c
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
ms.openlocfilehash: 7f69aed2e0e6791ca7f17c3420ff75a1ba220187
ms.lasthandoff: 03/13/2017

---
# <a name="quantifier-operations-visual-basic"></a>限定符操作 (Visual Basic)
限定符操作返回<xref:System.Boolean>值，该值指示是否在序列中元素的部分或全部都满足条件。</xref:System.Boolean>  
  
 下图描绘了对两个不同的源序列的两个不同的限定符操作。 第一次操作询问是否有一个或多个元素都字符 A，结果是`true`。 第二个操作询问是否所有元素都是字符 A，则结果为`true`。  
  
 ![LINQ 限定符操作](../../../../csharp/programming-guide/concepts/linq/media/linq_quantifier.png "LINQ_Quantifier")  
  
 下一节中列出执行限定符操作的标准查询运算符方法。  
  
## <a name="methods"></a>方法  
  
|方法名|描述|Visual Basic 查询表达式语法|更多信息|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|全部|确定是否在序列中的所有元素都满足条件。|`Aggregate … In … Into All(…)`|<xref:System.Linq.Enumerable.All%2A?displayProperty=fullName></xref:System.Linq.Enumerable.All%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=fullName></xref:System.Linq.Queryable.All%2A?displayProperty=fullName>|  
|任意|确定是否在序列中的任何元素都满足条件。|`Aggregate … In … Into Any()`|<xref:System.Linq.Enumerable.Any%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Any%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=fullName></xref:System.Linq.Queryable.Any%2A?displayProperty=fullName>|  
|包含|确定序列是否包含指定的元素。|不适用。|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Contains%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=fullName></xref:System.Linq.Queryable.Contains%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>查询表达式语法示例  
 这些示例使用`Aggregate`子句在 Visual Basic 中为 LINQ 查询中的筛选条件的一部分。  
  
 下面的示例使用`Aggregate`子句和<xref:System.Linq.Enumerable.All%2A>扩展方法，以从集合中返回这些人其宠物是所有早于指定的期限。</xref:System.Linq.Enumerable.All%2A>  
  
 [!code-vb[CsLINQAnyAll #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_1.vb)]  
  
 下面的示例使用`Aggregate`子句和<xref:System.Linq.Enumerable.Any%2A>扩展方法以返回集合中至少有一个人们只宠物的是早于指定的期限。</xref:System.Linq.Enumerable.Any%2A>  
  
 [!code-vb[CsLINQAnyAll #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [如何︰ 查询包含一组指定的字数 (LINQ) (Visual Basic 中) 的句子](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)
