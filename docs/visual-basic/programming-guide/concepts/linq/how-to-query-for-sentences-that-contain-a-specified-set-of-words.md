---
title: "如何︰ 查询包含一组指定的字数 (LINQ) (Visual Basic 中) 的句子 |Microsoft 文档"
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
ms.assetid: a5ae8ced-61fe-4c10-bb8a-95630e50f603
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
ms.openlocfilehash: 31561d586c9c05f502002efdfc455acb55159fed
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq-visual-basic"></a>如何：查询包含一组指定词语的句子 (LINQ) (Visual Basic)
此示例演示如何在文本文件中包含的一组指定词语的每个匹配项中找到的句子。 尽管搜索词的数组是硬编码在此示例中，它可能也将是动态填充在运行时。 在此示例中，查询返回的句子上，"过去"包含单词"数据"和"集成"。  
  
## <a name="example"></a>示例  
  
```vb  
Class FindSentences  
  
    Shared Sub Main()  
        Dim text As String = "Historically, the world of data and the world of objects " &   
        "have not been well integrated. Programmers work in C# or Visual Basic " &   
        "and also in SQL or XQuery. On the one side are concepts such as classes, " &   
        "objects, fields, inheritance, and .NET Framework APIs. On the other side " &   
        "are tables, columns, rows, nodes, and separate languages for dealing with " &   
        "them. Data types often require translation between the two worlds; there are " &   
        "different standard functions. Because the object world has no notion of query, a " &   
        "query can only be represented as a string without compile-time type checking or " &   
        "IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to " &   
        "objects in memory is often tedious and error-prone."  
  
        ' Split the text block into an array of sentences.  
        Dim sentences As String() = text.Split(New Char() {".", "?", "!"})  
  
        ' Define the search terms. This list could also be dynamically populated at runtime  
        Dim wordsToMatch As String() = {"Historically", "data", "integrated"}  
  
        ' Find sentences that contain all the terms in the wordsToMatch array  
        ' Note that the number of terms to match is not specified at compile time  
        Dim sentenceQuery = From sentence In sentences   
                            Let w = sentence.Split(New Char() {" ", ",", ".", ";", ":"},   
                                                   StringSplitOptions.RemoveEmptyEntries)   
                            Where w.Distinct().Intersect(wordsToMatch).Count = wordsToMatch.Count()   
                            Select sentence  
  
        ' Execute the query  
        For Each str As String In sentenceQuery  
            Console.WriteLine(str)  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
End Class  
' Output:  
' Historically, the world of data and the world of objects have not been well integrated  
```  
  
 查询将起作用，首先将文本拆分成的句子，然后将句子拆分为一个包含每个单词的字符串数组。 为每个这些阵列<xref:System.Linq.Enumerable.Distinct%2A>方法中删除所有重复的单词，然后查询执行<xref:System.Linq.Enumerable.Intersect%2A>word 阵列上的操作和`wordsToMatch`数组。</xref:System.Linq.Enumerable.Intersect%2A> </xref:System.Linq.Enumerable.Distinct%2A> 交集 count 是否的计数相同`wordsToMatch`数组，字中找到所有单词，且返回原始句子。  
  
 在调用<xref:System.String.Split%2A>，标点符号使用作为分隔符，以便从字符串中移除。</xref:System.String.Split%2A> 如果您没有不这样做，例如"过去"您可以使用一个字符串，程序将不匹配"过去"在`wordsToMatch`数组。 您可能需要使用其他分隔符，具体取决于标点的源文本中找到的类型。  
  
## <a name="compiling-the-code"></a>编译代码  
 创建一个面向.NET Framework 版本 3.5 或更高版本对 System.Core.dll 的引用与项目和一个`Imports`System.Linq 命名空间的语句。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ 和字符串 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
