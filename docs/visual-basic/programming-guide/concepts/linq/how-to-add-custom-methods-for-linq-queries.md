---
title: "如何︰ 为 LINQ 查询 (Visual Basic 中) 添加自定义方法 |Microsoft 文档"
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
ms.assetid: 099b2e2a-83cd-45c6-aa4d-01b398b5faaf
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 166eb731d41e009c374ba55f929eed302793ecd0
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-add-custom-methods-for-linq-queries-visual-basic"></a>如何︰ 为 LINQ 查询 (Visual Basic 中) 添加自定义方法
您可以扩展，可以通过添加的扩展方法使用 LINQ 查询方法的一套<xref:System.Collections.Generic.IEnumerable%601>接口。</xref:System.Collections.Generic.IEnumerable%601> 例如，除了标准平均值或最大操作数中，可以创建自定义的聚合方法来计算单个值序列中的值。 此外可以创建一个方法，用作自定义筛选器或特定数据转换为一系列的值并返回新的序列。 此类方法的示例包括<xref:System.Linq.Enumerable.Distinct%2A>， <xref:System.Linq.Enumerable.Skip%2A>，和<xref:System.Linq.Enumerable.Reverse%2A>。</xref:System.Linq.Enumerable.Reverse%2A> </xref:System.Linq.Enumerable.Skip%2A> </xref:System.Linq.Enumerable.Distinct%2A>  
  
 在扩展<xref:System.Collections.Generic.IEnumerable%601>接口，可以将自定义方法应用于任何可枚举集合。</xref:System.Collections.Generic.IEnumerable%601> 有关详细信息，请参阅[扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)。  
  
## <a name="adding-an-aggregate-method"></a>添加聚合方法  
 聚合方法计算出单个值从一组值。 LINQ 提供了几种聚合方法，包括<xref:System.Linq.Enumerable.Average%2A>， <xref:System.Linq.Enumerable.Min%2A>，和<xref:System.Linq.Enumerable.Max%2A>。</xref:System.Linq.Enumerable.Max%2A> </xref:System.Linq.Enumerable.Min%2A> </xref:System.Linq.Enumerable.Average%2A> 可以通过添加到扩展方法来创建您自己的聚合方法<xref:System.Collections.Generic.IEnumerable%601>接口。</xref:System.Collections.Generic.IEnumerable%601>  
  
 下面的代码示例演示如何创建扩展方法调用`Median`来计算的类型的数字序列中的中间值`double`。  
  
```vb  
Imports System.Runtime.CompilerServices  
  
Module LINQExtension  
  
    ' Extension method for the IEnumerable(of T) interface.   
    ' The method accepts only values of the Double type.  
    <Extension()>   
    Function Median(ByVal source As IEnumerable(Of Double)) As Double  
        If source.Count = 0 Then  
            Throw New InvalidOperationException("Cannot compute median for an empty set.")  
        End If  
  
        Dim sortedSource = From number In source   
                           Order By number  
  
        Dim itemIndex = sortedSource.Count \ 2  
  
        If sortedSource.Count Mod 2 = 0 Then  
            ' Even number of items in list.  
            Return (sortedSource(itemIndex) + sortedSource(itemIndex - 1)) / 2  
        Else  
            ' Odd number of items in list.  
            Return sortedSource(itemIndex)  
        End If  
    End Function  
End Module  
```  
  
 与调用从其他聚合方法相同的方式，为任何可枚举集合调用此扩展方法<xref:System.Collections.Generic.IEnumerable%601>接口。</xref:System.Collections.Generic.IEnumerable%601>  
  
> [!NOTE]
>  在 Visual Basic 中，您可以使用方法调用或标准的查询语法`Aggregate`或`Group By`子句。 有关详细信息，请参阅[Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)和[组 By 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。  
  
 下面的代码示例演示如何使用`Median`类型的数组的方法`double`。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
### <a name="overloading-an-aggregate-method-to-accept-various-types"></a>重载以接受各种类型的聚合方法  
 您可以重载聚合方法，以便它接受各种类型的序列。 标准的方法是创建每种类型的重载。 另一种方法是创建一个重载，它将采用泛型类型，并将其转换为特定类型使用委托。 此外可以结合这两种方法。  
  
#### <a name="to-create-an-overload-for-each-type"></a>若要创建每种类型的重载  
 您可以创建您想要支持每种类型的特定重载。 下面的代码示例演示的重载`Median`方法`integer`类型。  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 现在，您可以调用`Median`两个重载`integer`和`double`类型，如下面的代码中所示︰  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
#### <a name="to-create-a-generic-overload"></a>若要创建的泛型重载  
 此外可以创建一个重载，它接受泛型对象的序列。 此重载采用委托作为参数，并使用它来将泛型类型的对象的序列转换为特定类型。  
  
 下面的代码演示的重载`Median`采用的方法<xref:System.Func%602>委托作为参数。</xref:System.Func%602> 此委托采用泛型类型 T 的对象，并返回类型的对象`double`。  
  
```vb  
' Generic overload.  
  
<Extension()>   
Function Median(Of T)(ByVal source As IEnumerable(Of T),   
                      ByVal selector As Func(Of T, Double)) As Double  
    Return Aggregate num In source Select selector(num) Into med = Median()  
End Function  
```  
  
 现在，您可以调用`Median`为一系列的任何类型的对象的方法。 如果类型不具有其自己的方法重载，您必须将传递委托参数。 在 Visual Basic 中，您可以实现此目的使用 lambda 表达式。 此外，如果您使用`Aggregate`或`Group By`子句而不是方法调用中的，您可以传递任何值或处于范围内，此子句的表达式。  
  
 下面的代码示例演示如何调用`Median`为整数的数组和一个字符串数组的方法。 对于字符串，字符串长度的数组中的中值被计算。 该示例演示如何将传递<xref:System.Func%602>委托到的参数`Median`每个用例的方法。</xref:System.Func%602>  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
## <a name="adding-a-method-that-returns-a-collection"></a>添加返回的集合的方法  
 您可以扩展<xref:System.Collections.Generic.IEnumerable%601>与返回一系列值的自定义查询方法的接口。</xref:System.Collections.Generic.IEnumerable%601> 在这种情况下，该方法必须返回类型<xref:System.Collections.Generic.IEnumerable%601>。</xref:System.Collections.Generic.IEnumerable%601>的集合 这种方法可以用于将筛选器或数据转换应用于一系列值。  
  
 下面的示例演示如何创建名为的扩展方法`AlternateElements`返回每个其他元素在集合中，从第一个元素开始。  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 可以为任何可枚举集合调用此扩展方法，就像将调用其他方法从<xref:System.Collections.Generic.IEnumerable%601>接口，如下面的代码中所示︰</xref:System.Collections.Generic.IEnumerable%601>  
  
```vb  
Dim strings() As String = {"a", "b", "c", "d", "e"}  
  
Dim query = strings.AlternateElements()  
  
For Each element In query  
    Console.WriteLine(element)  
Next  
  
' This code produces the following output:  
'  
' a  
' c  
' e  
```  
  
## <a name="see-also"></a>请参见  
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 [扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
