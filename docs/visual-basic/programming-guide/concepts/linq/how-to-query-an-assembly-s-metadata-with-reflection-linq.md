---
title: "如何︰ 查询使用反射 (LINQ) (Visual Basic 中) 的程序集的元数据 |Microsoft 文档"
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
ms.assetid: 53caa336-ab83-4181-b0f6-5c87c5f9e4ee
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7c1bc26d7b23135dd45ad58ea0bd2510b7157448
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-query-an-assembly39s-metadata-with-reflection-linq-visual-basic"></a>如何︰ 查询使用反射 (LINQ) (Visual Basic 中) 的程序集的元数据
下面的示例演示 LINQ 可以与反射一起用于检索有关与指定的搜索条件匹配的方法的特定元数据。 在这种情况下，该查询将返回可枚举的类型，如数组的程序集中查找的所有方法的名称。  
  
## <a name="example"></a>示例  
  
```vb  
Imports System.Reflection  
Imports System.IO  
Imports System.Linq  
Module Module1  
  
    Sub Main()  
        Dim asmbly As Assembly =   
            Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089")  
  
        Dim pubTypesQuery = From type In asmbly.GetTypes()   
                            Where type.IsPublic   
                            From method In type.GetMethods()   
                            Where method.ReturnType.IsArray = True   
                            Let name = method.ToString()   
                            Let typeName = type.ToString()   
                            Group name By typeName Into methodNames = Group  
  
        Console.WriteLine("Getting ready to iterate")  
        For Each item In pubTypesQuery  
            Console.WriteLine(item.methodNames)  
  
            For Each type In item.methodNames  
                Console.WriteLine(" " & type)  
            Next  
        Next  
        Console.ReadKey()  
    End Sub  
  
End Module  
```  
  
 该示例使用<xref:System.Reflection.Assembly.GetTypes%2A>方法以返回类型的数组中指定的程序集。</xref:System.Reflection.Assembly.GetTypes%2A> [Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)应用筛选器以便仅将公共类型返回。 对于每个公共类型，子查询通过使用生成<xref:System.Reflection.MethodInfo>从返回的数组<xref:System.Type.GetMethods%2A>调用。</xref:System.Type.GetMethods%2A> </xref:System.Reflection.MethodInfo> 这些结果进行筛选，返回其返回类型是数组或其他类型的实现<xref:System.Collections.Generic.IEnumerable%601>。</xref:System.Collections.Generic.IEnumerable%601>这些方法 最后，这些结果进行分组所使用的类型名称作为键。  
  
## <a name="compiling-the-code"></a>编译代码  
 创建一个面向.NET Framework 版本 3.5 或更高版本对 System.Core.dll 的引用与项目和一个`Imports`System.Linq 命名空间的语句。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
