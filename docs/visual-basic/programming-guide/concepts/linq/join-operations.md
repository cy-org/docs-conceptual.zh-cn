---
title: "联接操作 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 39ab4854-ac84-4738-9d0b-3cb79be84db4
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
ms.openlocfilehash: dce1adb5b918674bc8ee8fc48c8ff5b3c3814a88
ms.lasthandoff: 03/13/2017

---
# <a name="join-operations-visual-basic"></a>联接操作 (Visual Basic)
一个*联接*两个数据源就是一个数据源中的对象具有共享一个公共属性，另一个数据源中的对象相关联。  
  
 当查询所面向的数据源相互之间具有无法直接领会的关系时，联接就成为一项重要的运算。 在面向对象的编程中，这可能意味着在未建模对象之间进行关联，例如对单向关系进行反向推理。 下面是单向关系的一个示例：Customer 类有一个类型为 City 的属性，但 City 类没有作为 Customer 对象集合的属性。 如果你具有一个 City 对象列表，并且要查找每个城市中的所有客户，则可以使用联接运算完成此项查找。  
  
 LINQ 框架中提供的联接方法有<xref:System.Linq.Enumerable.Join%2A>和<xref:System.Linq.Enumerable.GroupJoin%2A>。</xref:System.Linq.Enumerable.GroupJoin%2A> </xref:System.Linq.Enumerable.Join%2A> 这些方法执行同等联接，即来匹配基于的键相等对两个数据源的联接。 （与此相较，Transact-SQL 支持除“等于”之外的联接运算符，例如“小于”运算符。）在关系数据库术语<xref:System.Linq.Enumerable.Join%2A>实现内部联接中，一种联接类型仅在另一个数据集中具有匹配项的那些对象返回。</xref:System.Linq.Enumerable.Join%2A> <xref:System.Linq.Enumerable.GroupJoin%2A>方法在关系数据库术语中，有没有直接等效项，但它实现了内部联接和左外部联接的超集。</xref:System.Linq.Enumerable.GroupJoin%2A> 左外部联接是一种联接，返回第一个 （左） 数据源，每个元素，即使它具有其他数据源中没有关联的元素。  
  
 下图显示了一个概念性视图，其中包含两个集合以及这两个集合中的包含在内部联接或左外部联接中的元素。  
  
 ![显示内部/外部的两个重叠圆圈。] (../../../../csharp/programming-guide/concepts/linq/media/joincircles.png "JoinCircles")  
  
## <a name="methods"></a>方法  
  
|方法名|描述|Visual Basic 查询表达式语法|更多信息|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|联接|根据键选择器函数联接两个序列并提取值对。|`From x In …, y In … Where x.a = y.a`<br /><br /> - 或 -<br /><br /> `Join … [As …]In … On …`|<xref:System.Linq.Enumerable.Join%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Join%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Join%2A?displayProperty=fullName></xref:System.Linq.Queryable.Join%2A?displayProperty=fullName>|  
|GroupJoin|根据键选择器函数联接两个序列，并对每个元素的结果匹配项进行分组。|`Group Join … In … On …`|<xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=fullName></xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=fullName></xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=fullName>|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [构建联接和叉积查询](http://msdn.microsoft.com/library/d8072ede-0521-4670-9bec-1778ceeb875b)   
 [Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)   
 [如何︰ 联接不同文件 (LINQ) (Visual Basic 中) 的内容](../../../../visual-basic/programming-guide/concepts/linq/how-to-join-content-from-dissimilar-files-linq.md)   
 [如何︰ 从多个源 (LINQ) (Visual Basic 中) 填充对象集合](../../../../visual-basic/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)
