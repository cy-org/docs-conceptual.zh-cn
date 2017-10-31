---
title: "如何：通过 LINQ 使用联接合并数据 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Group Join 子句 [Visual Basic]"
  - "Join 子句 [Visual Basic 中的 LINQ]"
  - "联接 [Visual Basic 中的 LINQ]"
  - "联接 [Visual Basic 中的 LINQ]"
  - "查询 [Visual Basic 中的 LINQ], 帮助主题"
  - "查询 [Visual Basic 中的 LINQ], 联接"
ms.assetid: 5b00a478-035b-41c6-8918-be1a97728396
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：通过 LINQ 使用联接合并数据 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 提供 `Join` 和 `Group Join` 查询子句，使您可以基于集合之间的公共值将多个集合的内容合并在一起。  这些值称为键值。  熟悉关系数据库概念的开发人员会发现，实际上 `Join` 子句相当于 INNER JOIN，`Group Join` 子句相当于 LEFT OUTER JOIN。  
  
 本主题中的示例演示一些使用 `Join` 和 `Group Join` 查询子句组合数据的方式。  
  
## 创建项目和添加示例数据  
  
#### 创建包含示例数据和类型的项目  
  
1.  若要运行本主题中的示例，请打开 Visual Studio，添加一个新的 Visual Basic 控制台应用程序项目。  双击 Visual Basic 创建的 Module1.vb 文件。  
  
2.  本主题中的示例使用 `Person` 和 `Pet` 类型以及下面的代码示例中的数据。  将这段代码复制到 Visual Basic 所创建的默认 `Module1` 模块中。  
  
     [!code-vb[VbLINQHowTos#1](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_1.vb)]  
    [!code-vb[VbLINQHowTos#2](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_2.vb)]  
  
## 使用 Join 子句执行内部联接  
 INNER JOIN 将两个集合的数据合并在一起。  指定的键值相匹配的项包括在内。  在另一集合中没有匹配项的所有集合项都排除在外。  
  
 在 Visual Basic 中，LINQ 提供两个选项来执行 INNER JOIN：隐式联接和显式联接。  
  
 隐式联接在 `From` 子句中指定要联接的集合，在 `Where` 子句中指定匹配键字段。  Visual Basic 根据指定的键字段隐式联接两个集合。  
  
 如果要明确指出联接所用的键字段，可以使用 `Join` 子句指定显式联接。  这种情况下，`Where` 子句仍可用于筛选查询结果。  
  
#### 使用 Join 子句执行内部联接  
  
1.  将下面的代码添加到项目中的 `Module1` 模块，查看隐式和显式内部联接的示例。  
  
     [!code-vb[VbLINQHowTos#4](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_3.vb)]  
  
## 使用 Group Join 子句执行左外部联接  
 LEFT OUTER JOIN 包括联接左侧集合中的所有项，而对于联接的右侧集合，它仅包含其中的匹配值。  联接的右侧集合中的项如果在联接的左侧集合中没有匹配项，则会排除在查询结果之外。  
  
 `Group Join` 子句实际上执行 LEFT OUTER JOIN。  通常所称的 LEFT OUTER JOIN 与 `Group Join` 子句的返回结果之间的差异在于，`Group Join` 子句对联接的右侧集合的结果按左侧集合中的每一项进行分组。  在关系数据库中，LEFT OUTER JOIN 返回未分组的结果，在该结果中，查询结果中的每一项都包含来自联接的两个集合的匹配项。  这种情况下，对于联接的右侧集合中的每个匹配项，对应的左侧集合中的项都是重复的。  完成下面的过程后，就可以看到这种情况。  
  
 通过扩展查询，为每个分组查询结果返回一个项，可以按照不分组结果的形式检索 `Group Join` 查询的结果。  为此，必须确保在分组集合的 `DefaultIfEmpty` 方法上进行查询。  这样可确保联接的左侧集合中的项包括在查询结果中，即使在右侧集合中没有匹配结果也是如此。  可以向查询添加代码，以便提供一个默认值，作为联接的右侧集合中不存在匹配值时的结果。  
  
#### 使用 Group Join 子句执行左外部联接  
  
1.  将下面的代码添加到项目的 `Module1` 模块中，查看分组左外部联接和不分组左外部联接的示例。  
  
     [!code-vb[VbLINQHowTos#3](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_4.vb)]  
  
## 使用复合键执行联接  
 在 `Join` 或 `Group Join` 子句中，可以使用 `And` 关键字来标识在对联接的集合中的值进行匹配时要使用的多个键字段。  `And` 关键字指定所有指定的键字段都必须匹配要联接的项。  
  
#### 使用复合键执行联接  
  
1.  将下面的代码添加到项目的 `Module1` 模块，查看使用复合键的联接示例。  
  
     [!code-vb[VbLINQHowTos#5](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_5.vb)]  
  
## 运行代码  
  
#### 添加代码以运行示例  
  
1.  用下面的代码替换项目中的 `Module1` 模块的 `Sub Main`，运行本主题中的示例。  
  
     [!code-vb[VbLINQHowTos#6](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-combine-data-with-linq-by-using-joins_6.vb)]  
  
2.  按 F5 键运行示例。  
  
## 请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)   
 [Group Join 子句](../../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [使用 LINQ 进行数据转换 \(C\#\)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)