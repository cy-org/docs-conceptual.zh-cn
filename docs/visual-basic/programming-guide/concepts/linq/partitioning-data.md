---
title: "分区数据 (Visual Basic) |Microsoft 文档"
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
ms.assetid: 69c59379-b66e-422c-b324-5b5c07760ef7
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
ms.openlocfilehash: a746ce3e24812d1df6b6e221cca0364bf2cc7f1c
ms.lasthandoff: 03/13/2017

---
# <a name="partitioning-data-visual-basic"></a>分区数据 (Visual Basic)
在 LINQ 中分区是指将输入的序列划分为两个部分，而无需重新排列元素，并返回的部分之一的操作。  
  
 下图显示三个不同分区的操作序列的字符的结果。 第一次操作返回序列中的前三个元素。 第二个操作跳过前三个元素，并返回剩余元素。 第三个操作跳过序列中的前两个元素，并返回接下来三个元素。  
  
 ![LINQ 分区操作](../../../../csharp/programming-guide/concepts/linq/media/linq_partition.png "LINQ_Partition")  
  
 下一节中列出分区序列的标准查询运算符方法。  
  
## <a name="operators"></a>运算符  
  
|运算符名称|描述|Visual Basic 查询表达式语法|更多信息|  
|-------------------|-----------------|------------------------------------------|----------------------|  
|Skip|跳过序列中的指定位置之前的元素。|`Skip`|<xref:System.Linq.Enumerable.Skip%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Skip%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Skip%2A?displayProperty=fullName></xref:System.Linq.Queryable.Skip%2A?displayProperty=fullName>|  
|SkipWhile|跳过基于谓词的函数，直到某元素不满足条件的元素。|`Skip While`|<xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=fullName></xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=fullName></xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=fullName>|  
|Take|序列中的指定位置之前提取元素。|`Take`|<xref:System.Linq.Enumerable.Take%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Take%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Take%2A?displayProperty=fullName></xref:System.Linq.Queryable.Take%2A?displayProperty=fullName>|  
|TakeWhile|采用基于谓词的函数，直到元素不满足条件的元素。|`Take While`|<xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=fullName></xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=fullName></xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>查询表达式语法示例  
  
### <a name="skip"></a>Skip  
 下面的代码示例使用`Skip`中的子句[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]前要跳过过的字符串数组中的前四个字符串数组中返回剩余的字符串。  
  
 [!code-vb[CsLINQPartitioning #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_1.vb)]  
  
### <a name="skipwhile"></a>SkipWhile  
 下面的代码示例使用`Skip While`中的子句[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]来跳过该字符串的第一个字母时数组中的字符串为"a"。 返回数组中的剩余的字符串。  
  
 [!code-vb[CsLINQPartitioning #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_2.vb)]  
  
### <a name="take"></a>Take  
 下面的代码示例使用`Take`中的子句[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可返回的字符串数组中的前两个字符串。  
  
 [!code-vb[CsLINQPartitioning #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_3.vb)]  
  
### <a name="takewhile"></a>TakeWhile  
 下面的代码示例使用`Take While`中的子句[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符串的长度小于或等于&5; 时从数组中返回的字符串。  
  
 [!code-vb[CsLINQPartitioning #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Skip 子句](../../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Skip While 子句](../../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Take 子句](../../../../visual-basic/language-reference/queries/take-clause.md)   
 [Take While 子句](../../../../visual-basic/language-reference/queries/take-while-clause.md)
