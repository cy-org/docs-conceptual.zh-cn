---
title: "LINQ to Objects (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: dd4c30bc-1c9b-4781-a482-b5eada38deb2
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
ms.openlocfilehash: d2bc048fea9affd4998430783d20b978317f3897
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-objects-visual-basic"></a>LINQ to Objects (Visual Basic)
术语"LINQ 到对象"指使用 LINQ 查询与任何<xref:System.Collections.IEnumerable>或<xref:System.Collections.Generic.IEnumerable%601>集合直接，无需使用中间的 LINQ 提供程序或 API，例如[LINQ to SQL](https://msdn.microsoft.com/library/bb386976)或[LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable> 您可以使用 LINQ 来查询任何可枚举集合，如<xref:System.Collections.Generic.List%601>， <xref:System.Array>，或<xref:System.Collections.Generic.Dictionary%602>.</xref:System.Collections.Generic.Dictionary%602> </xref:System.Array> </xref:System.Collections.Generic.List%601> 此集合可以是用户定义，或者可能由.NET Framework API 返回。  
  
 在基本的意义上讲，LINQ to Objects 表示集合的新方法。 采用旧方法，你必须编写指定如何从集合检索数据的复杂的 `For Each` 循环。 在 LINQ 方法中，您编写描述要检索的声明性代码。  
  
 此外，LINQ 查询具有三大优势于传统`For Each`循环︰  
  
1.  它们更简明、更易读，尤其在筛选多个条件时。  
  
2.  它们使用最少的应用程序代码提供强大的筛选、排序和分组功能。  
  
3.  无需修改或只需做很小的修改即可将它们移植到其他数据源。  
  
 在常规、 变得更加复杂你想要对数据执行该操作，而不是传统迭代技术使用 LINQ，您将认识的益处越多。  
  
 本节的目的是演示使用一些精选示例的 LINQ 方法。 并不打算详尽说明。  
  
## <a name="in-this-section"></a>本节内容  
 [LINQ 和字符串 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)  
 说明如何使用 LINQ 来查询和转换字符串和字符串集合。 还包括指向演示这些原则的主题的链接。  
  
 [LINQ 和反射 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-reflection.md)  
 链接到演示 LINQ 如何使用反射的示例。  
  
 [LINQ 和文件目录 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)  
 说明如何使用 LINQ 与文件系统进行交互。 还包括指向演示这些概念的主题的链接。  
  
 [如何︰ 使用 (Visual Basic 中) 的 LINQ 查询 ArrayList](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 演示如何查询在 C# 中的 ArrayList。  
  
 [如何︰ 为 LINQ 查询 (Visual Basic 中) 添加自定义方法](../../../../visual-basic/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 说明如何扩展，可以通过添加的扩展方法使用 LINQ 查询方法的一套<xref:System.Collections.Generic.IEnumerable%601>接口。</xref:System.Collections.Generic.IEnumerable%601>  
  
 [语言集成查询 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 提供指向介绍了 LINQ，并提供执行查询的代码示例的主题的链接。
