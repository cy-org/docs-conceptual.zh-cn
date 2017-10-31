---
title: "标准查询运算符概述 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 302bd39e-2ec1-495b-94bf-37d370d6f05f
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
ms.openlocfilehash: eb28988ef49e0583fb7e9197c4e13c84665074ac
ms.lasthandoff: 03/13/2017

---
# <a name="standard-query-operators-overview-visual-basic"></a>标准查询运算符概述 (Visual Basic)
*标准查询运算符*是窗体中的 LINQ 模式的方法。 这些方法中的大多数作用于序列，其中的序列是其类型实现的对象<xref:System.Collections.Generic.IEnumerable%601>接口或<xref:System.Linq.IQueryable%601>接口。</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601> 标准查询运算符提供了查询功能包括筛选、 投影、 聚合、 排序和的详细信息。  
  
 有两套 LINQ 标准查询运算符，一种类型<xref:System.Collections.Generic.IEnumerable%601>，另一个操作类型<xref:System.Linq.IQueryable%601>。</xref:System.Linq.IQueryable%601>的对象</xref:System.Collections.Generic.IEnumerable%601>的对象上运行 构成每个集合的方法是静态成员<xref:System.Linq.Enumerable>和<xref:System.Linq.Queryable>类，分别。</xref:System.Linq.Queryable> </xref:System.Linq.Enumerable> 它们定义为*扩展方法*它们对操作的类型。 这意味着可以通过使用静态方法的语法或实例方法语法调用它们。  
  
 此外，多个标准查询运算符方法操作类型而不是基于<xref:System.Collections.Generic.IEnumerable%601>或<xref:System.Linq.IQueryable%601>。</xref:System.Linq.IQueryable%601></xref:System.Collections.Generic.IEnumerable%601>上 <xref:System.Linq.Enumerable>类型定义了两个此类方法的类型<xref:System.Collections.IEnumerable>。</xref:System.Collections.IEnumerable>对象上同时运行</xref:System.Linq.Enumerable> 这些方法，<xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29>和<xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29>，可让您启用要在 LINQ 模式中查询的非参数化或非泛型集合。</xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29> </xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> 他们通过创建强类型化对象的集合来执行此操作。 <xref:System.Linq.Queryable>类定义了两个类似的方法，<xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29>并且<xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>，针对对象类型<xref:System.Linq.Queryable>。</xref:System.Linq.Queryable>运行</xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29></xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29></xref:System.Linq.Queryable>  
  
 标准查询运算符在其执行，具体取决于它们返回单一实例值或一系列值的时间会有所不同。 返回单一实例值的那些方法 (例如，<xref:System.Linq.Enumerable.Average%2A>和<xref:System.Linq.Enumerable.Sum%2A>) 将会立即执行。</xref:System.Linq.Enumerable.Sum%2A> </xref:System.Linq.Enumerable.Average%2A> 延迟查询执行和返回一个可枚举对象返回一系列的方法。  
  
 在对集合执行运算内存中，即，将扩展这些方法的方法的情况下<xref:System.Collections.Generic.IEnumerable%601>，返回的可枚举对象捕获已传递到方法的参数。</xref:System.Collections.Generic.IEnumerable%601> 当枚举该对象时，使用查询运算符的逻辑，并返回查询结果。  
  
 与此相反，用于扩展的方法<xref:System.Linq.IQueryable%601>不实现任何查询行为，但创建表示要执行该查询的表达式树。</xref:System.Linq.IQueryable%601> 查询处理源<xref:System.Linq.IQueryable%601>对象。</xref:System.Linq.IQueryable%601>  
  
 对查询方法的调用可以链接在一起在一个查询中，这就使得查询变得很复杂。  
  
 下面的代码示例演示如何使用标准查询运算符来获取有关序列的信息。  
  
```vb  
Dim sentence = "the quick brown fox jumps over the lazy dog"  
' Split the string into individual words to create a collection.  
Dim words = sentence.Split(" "c)  
  
Dim query = From word In words   
            Group word.ToUpper() By word.Length Into gr = Group   
            Order By Length _  
            Select Length, GroupedWords = gr  
  
Dim output As New System.Text.StringBuilder  
For Each obj In query  
    output.AppendLine(String.Format("Words of length {0}:", obj.Length))  
    For Each word As String In obj.GroupedWords  
        output.AppendLine(word)  
    Next  
Next  
  
'Display the output  
MsgBox(output.ToString())  
  
' This code example produces the following output:  
'  
' Words of length 3:  
' THE  
' FOX  
' THE  
' DOG  
' Words of length 4:  
' OVER  
' LAZY  
' Words of length 5:  
' QUICK  
' BROWN  
' JUMPS   
```  
  
## <a name="query-expression-syntax"></a>查询表达式语法  
 一些经常使用的标准查询运算符包含专用使他们能够作为的一部分调用的 C# 和 Visual Basic 语言关键字语法*查询**表达式*。 有关具有专用的关键字和其对应的语法的标准查询运算符的详细信息，请参阅[标准查询运算符 (Visual Basic 中) 的查询表达式语法](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)。  
  
## <a name="extending-the-standard-query-operators"></a>扩展标准查询运算符  
 您可以通过创建适合于目标域或技术的特定于域的方法扩展的一套标准查询运算符。 您还可以用您自己提供其他服务，如远程评估、 查询转换和优化的实现替换标准查询运算符。 请参阅<xref:System.Linq.Enumerable.AsEnumerable%2A>以举例。</xref:System.Linq.Enumerable.AsEnumerable%2A>  
  
## <a name="related-sections"></a>相关章节  
 以下链接可转至主题提供了有关各种基于功能的标准查询运算符的其他信息。  
  
 [对数据进行排序](../../../../visual-basic/programming-guide/concepts/linq/sorting-data.md)  
  
 [Set 运算 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/set-operations.md)  
  
 [筛选数据 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/filtering-data.md)  
  
 [限定符操作 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)  
  
 [投影运算 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)  
  
 [分区数据 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/partitioning-data.md)  
  
 [联接操作 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/join-operations.md)  
  
 [对数据进行分组 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/grouping-data.md)  
  
 [生成操作 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/generation-operations.md)  
  
 [相等运算 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/equality-operations.md)  
  
 [元素操作 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/element-operations.md)  
  
 [转换数据类型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)  
  
 [串联运算 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/concatenation-operations.md)  
  
 [聚合操作 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable></xref:System.Linq.Queryable>   
 [(Visual Basic 中) 的 LINQ 简介](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-linq.md)   
 [标准查询运算符 (Visual Basic 中) 的查询表达式语法](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)   
 [标准查询运算符按执行 (Visual Basic 中) 的方式的分类](../../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)   
 [扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
