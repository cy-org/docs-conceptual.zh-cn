---
title: "如何︰ 使用 (Visual Basic 中) 的 LINQ 查询 ArrayList |Microsoft 文档"
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
ms.assetid: 176358a9-d765-4b57-9557-7feb4428138d
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f48b06c23b1e28fccb953638954a8d9afefe574e
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-an-arraylist-with-linq-visual-basic"></a>如何︰ 使用 (Visual Basic 中) 的 LINQ 查询 ArrayList
当使用 LINQ 来查询非泛型<xref:System.Collections.IEnumerable>这类的集合<xref:System.Collections.ArrayList>，所以必须显式声明的范围变量，以反映在集合中的对象的特定类型的类型。</xref:System.Collections.ArrayList> </xref:System.Collections.IEnumerable> 例如，如果您有<xref:System.Collections.ArrayList>的`Student`对象，您[From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)应如下所示︰</xref:System.Collections.ArrayList>  
  
```  
Dim query = From student As Student In arrList   
...  
```  
  
 通过指定的范围变量的类型，您要强制转换中的每项<xref:System.Collections.ArrayList>到`Student`。</xref:System.Collections.ArrayList>  
  
 使用显式类型化的范围变量在查询表达式等效于调用<xref:System.Linq.Enumerable.Cast%2A>方法。</xref:System.Linq.Enumerable.Cast%2A> <xref:System.Linq.Enumerable.Cast%2A>如果无法执行指定的强制转换，将引发异常。</xref:System.Linq.Enumerable.Cast%2A> <xref:System.Linq.Enumerable.Cast%2A>和<xref:System.Linq.Enumerable.OfType%2A>是对非泛型操作的两个标准查询运算符方法<xref:System.Collections.IEnumerable>类型。</xref:System.Collections.IEnumerable> </xref:System.Linq.Enumerable.OfType%2A></xref:System.Linq.Enumerable.Cast%2A> 在 Visual Basic 中，您必须显式调用<xref:System.Linq.Enumerable.Cast%2A>方法要确保特定范围的变量类型的数据源。</xref:System.Linq.Enumerable.Cast%2A> 有关详细信息，请参阅[查询操作 (Visual Basic 中) 中的类型关系](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示一个简单的查询对<xref:System.Collections.ArrayList>。</xref:System.Collections.ArrayList> 请注意，本示例使用对象初始值设定项，当代码调用<xref:System.Collections.ArrayList.Add%2A>方法，但这并不是必需。</xref:System.Collections.ArrayList.Add%2A>  
  
```vb  
Imports System.Collections  
Imports System.Linq  
  
Module Module1  
  
    Public Class Student  
        Public Property FirstName As String  
        Public Property LastName As String  
        Public Property Scores As Integer()  
    End Class  
  
    Sub Main()  
  
        Dim student1 As New Student With {.FirstName = "Svetlana",   
                                     .LastName = "Omelchenko",   
                                     .Scores = New Integer() {98, 92, 81, 60}}  
        Dim student2 As New Student With {.FirstName = "Claire",   
                                    .LastName = "O'Donnell",   
                                    .Scores = New Integer() {75, 84, 91, 39}}  
        Dim student3 As New Student With {.FirstName = "Cesar",   
                                    .LastName = "Garcia",   
                                    .Scores = New Integer() {97, 89, 85, 82}}  
        Dim student4 As New Student With {.FirstName = "Sven",   
                                    .LastName = "Mortensen",   
                                    .Scores = New Integer() {88, 94, 65, 91}}  
  
        Dim arrList As New ArrayList()  
        arrList.Add(student1)  
        arrList.Add(student2)  
        arrList.Add(student3)  
        arrList.Add(student4)  
  
        ' Use an explicit type for non-generic collections  
        Dim query = From student As Student In arrList   
                    Where student.Scores(0) > 95   
                    Select student  
  
        For Each student As Student In query  
            Console.WriteLine(student.LastName & ": " & student.Scores(0))  
        Next  
        ' Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
End Module  
' Output:  
'   Omelchenko: 98  
'   Garcia: 97  
```  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)

