---
title: LINQ to Objects (C#)
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c5c2c178-3529-4f6c-b3df-2d5267af7f22
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 565b506a2b01c9d32fbd339d700e663527ee3b6e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-objects-c"></a>LINQ to Objects (C#)
术语“LINQ to Objects”指直接将 LINQ 查询与任何 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601> 集合一起使用，而不使用中间 LINQ 提供程序或 API，例如 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976) 或 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)。 可以使用 LINQ 来查询任何可枚举的集合，例如 <xref:System.Collections.Generic.List%601>、<xref:System.Array> 或 <xref:System.Collections.Generic.Dictionary%602>。 该集合可以是用户定义的集合，也可以是由 .NET Framework API 返回的集合。  
  
 从根本上说，“LINQ to Objects”表示一种新的处理集合的方法。 采用旧方法，必须编写指定如何从集合检索数据的复杂的 `foreach` 循环。 而采用 LINQ 方法，只需编写描述要检索的内容的声明性代码。  
  
 此外，LINQ 查询与传统 `foreach` 循环相比具有三大优势：  
  
1.  它们更简明、更易读，尤其在筛选多个条件时。  
  
2.  它们使用最少的应用程序代码提供强大的筛选、排序和分组功能。  
  
3.  无需修改或只需做很小的修改即可将它们移植到其他数据源。  
  
 通常，对数据执行的操作越复杂，就越能体会到 LINQ 相较于传统迭代技术的优势。  
  
 本节的目的是使用一些精选示例来演示 LINQ 方法。 并不打算详尽说明。  
  
## <a name="in-this-section"></a>本节内容  
 [LINQ 和字符串 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)  
 阐释如何使用 LINQ 来查询和转换字符串和字符串集合。 还包括指向演示这些原则的主题的链接。  
  
 [LINQ 和反射 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-reflection.md)  
 指向演示 LINQ 如何使用反射的示例的链接。  
  
 [LINQ 和文件目录 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)  
 阐释如何使用 LINQ 来与文件系统进行交互。 还包括指向演示这些概念的主题的链接。  
  
 [如何：使用 LINQ 查询 ArrayList (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 演示如何使用 C# 查询 ArrayList。  
  
 [如何：为 LINQ 查询添加自定义方法 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 阐释如何通过向 <xref:System.Collections.Generic.IEnumerable%601> 接口中添加扩展方法来扩展可用于 LINQ 查询的方法集。  
  
 [语言集成查询 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)  
 提供指向阐释 LINQ 并提供执行查询的代码示例的主题的链接。

