---
title: "转换数据类型 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 9b0cf1ab-de48-4c6e-9f00-05b40fade46e
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
ms.openlocfilehash: 53d8ad292891a567e13ec8a5396bcc114b379351
ms.lasthandoff: 03/13/2017

---
# <a name="converting-data-types-visual-basic"></a>转换数据类型 (Visual Basic)
转换方法更改输入对象的类型。  
  
 LINQ 查询中的转换运算可在各种应用程序中。 以下是一些示例︰  
  
-   <xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>方法可用来隐藏控件的标准查询运算符的类型的自定义实现。</xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>  
  
-   <xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName>方法可以用于启用非参数化以进行 LINQ 查询的集合。</xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName>  
  
-   <xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>， <xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>， <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>，和<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName>方法可用于强制立即执行查询而不是推迟到枚举该查询。</xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>  
  
## <a name="methods"></a>方法  
 下表列出了执行数据类型转换的标准查询运算符方法。  
  
 此名称以"As"开头的表中的转换方法更改源集合的静态类型，但不是枚举。 键入名称以开头"来枚举源集合，以及将项目放入相应的集合"的方法。  
  
|方法名|说明|Visual Basic 查询表达式语法|更多信息|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|AsEnumerable|返回类型化为<xref:System.Collections.Generic.IEnumerable%601>。</xref:System.Collections.Generic.IEnumerable%601>输入|不适用。|<xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName></xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>|  
|AsQueryable|将转换 （泛型）<xref:System.Collections.IEnumerable>到 （泛型） <xref:System.Linq.IQueryable>。</xref:System.Linq.IQueryable> </xref:System.Collections.IEnumerable>|不适用。|<xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName></xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName>|  
|Cast|将强制转换为指定的类型集合中的元素。|`From … As …`|<xref:System.Linq.Enumerable.Cast%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Cast%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Cast%2A?displayProperty=fullName></xref:System.Linq.Queryable.Cast%2A?displayProperty=fullName>|  
|OfType|筛选值，具体取决于他们可强制转换为指定类型的能力。|不适用。|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName></xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName></xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName>|  
|ToArray|将集合转换为数组。 此方法强制执行查询。|不适用。|<xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>|  
|ToDictionary|将元素放入<xref:System.Collections.Generic.Dictionary%602>根据键选择器函数。</xref:System.Collections.Generic.Dictionary%602> 此方法强制执行查询。|不适用。|<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>|  
|ToList|将集合转换为一种<xref:System.Collections.Generic.List%601>。</xref:System.Collections.Generic.List%601> 此方法强制执行查询。|不适用。|<xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>|  
|ToLookup|将元素放入<xref:System.Linq.Lookup%602>（一多字典） 根据键选择器函数。</xref:System.Linq.Lookup%602> 此方法强制执行查询。|不适用。|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-example"></a>查询表达式语法示例  
 下面的代码示例使用`From As`子句，以访问仅适用于子类型的成员之前转换为子类型。  
  
```vb  
Class Plant  
    Public Property Name As String  
End Class  
  
Class CarnivorousPlant  
    Inherits Plant  
    Public Property TrapType As String  
End Class  
  
Sub Cast()  
  
    Dim plants() As Plant = {   
        New CarnivorousPlant With {.Name = "Venus Fly Trap", .TrapType = "Snap Trap"},   
        New CarnivorousPlant With {.Name = "Pitcher Plant", .TrapType = "Pitfall Trap"},   
        New CarnivorousPlant With {.Name = "Sundew", .TrapType = "Flypaper Trap"},   
        New CarnivorousPlant With {.Name = "Waterwheel Plant", .TrapType = "Snap Trap"}}  
  
    Dim query = From plant As CarnivorousPlant In plants   
                Where plant.TrapType = "Snap Trap"   
                Select plant  
  
    Dim sb As New System.Text.StringBuilder()  
    For Each plant In query  
        sb.AppendLine(plant.Name)  
    Next  
  
    ' Display the results.  
    MsgBox(sb.ToString())  
  
    ' This code produces the following output:  
  
    ' Venus Fly Trap  
    ' Waterwheel Plant  
  
End Sub  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq></xref:System.Linq>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)   
 [如何︰ 使用 (Visual Basic 中) 的 LINQ 查询 ArrayList](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)
