---
title: "Order By 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryOrderBy"
  - "vb.QueryAscending"
  - "vb.QueryDescending"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Order By 子句"
  - "Order By 语句"
  - "查询 [Visual Basic], Order By"
ms.assetid: fa911282-6b81-44c7-acfa-46b5bb93df75
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Order By 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定查询结果的排序顺序。  
  
## 语法  
  
```  
Order By orderExp1 [ Ascending | Descending ] [, orderExp2 [...] ]  
```  
  
## 部件  
 `orderExp1`  
 必选。  当前查询结果中的一个或多个字段，用于标识对返回值进行排序的方式。  字段名称必须以逗号 \(,\) 分隔。  使用 `Ascending` 或 `Descending` 关键字可以指定对每个字段进行升序或降序排序。  如果未指定 `Ascending` 和 `Descending` 关键字，则默认排序顺序为升序。  排序顺序字段的优先级从左到右依次降低。  
  
## 备注  
 使用 `Order By` 子句可以对查询结果进行排序。  `Order By` 子句只能根据当前范围的范围变量对结果进行排序。  例如，`Select` 子句会在查询表达式中引入新范围以及用于该范围的新迭代变量。  在查询中的 `Select` 子句之前定义的范围变量不能在 `Select` 子句之后使用。  因此，如果要按照不可用于 `Select` 子句的字段对结果进行排序，则必须将 `Order By` 子句放在 `Select` 子句之前。  例如，当您希望按照没有在结果中返回的字段对查询结果进行排序时，必须这样做。  
  
 字段的升序和降序顺序由该字段的数据类型的 <xref:System.IComparable> 接口实现确定。  如果数据类型未实现 <xref:System.IComparable> 接口，则会忽略排序顺序。  
  
## 示例  
 下面的查询表达式使用 `From` 子句为 `books` 集合声明了范围变量 `book`。  `Order By` 子句按照价格以升序（默认值）对查询结果进行排序。  价格相同的书籍按书名进行升序排序。  `Select` 子句选择 `Title` 和 `Price` 属性作为查询返的回值。  
  
 [!code-vb[VbSimpleQuerySamples#24](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/order-by-clause_1.vb)]  
  
## 示例  
 下面的查询表达式使用 `Order By` 子句按照价格以降序对查询结果进行排序。  价格相同的书籍按书名进行升序排序。  
  
 [!code-vb[VbSimpleQuerySamples#25](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/order-by-clause_2.vb)]  
  
## 示例  
 下面的查询表达式使用 `Select` 子句选择书名、价格、出版日期和作者。  然后，该表达式填充新范围的范围变量的 `Title`、`Price`、`PublishDate` 和 `Author` 字段。  `Order By` 子句依次按照作者姓名、书名和价格对新的范围变量进行排序。  每个列以默认顺序（升序）进行排序。  
  
 [!code-vb[VbSimpleQuerySamples#26](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/order-by-clause_3.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)