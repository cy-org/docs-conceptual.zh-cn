---
title: "Select 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySelect"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Select"
  - "Select 子句"
  - "Select 语句"
ms.assetid: 27a3f61c-5960-4692-9b91-4d0c4b6178fe
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Select 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

定义查询的结果。  
  
## 语法  
  
```  
Select [ var1 = ] fieldName1 [, [ var2 = ] fieldName2 [...] ]  
```  
  
## 部件  
 `var1`  
 可选。  可用于引用列表达式的结果的别名。  
  
 `fieldName1`  
 必选。  要在查询结果中返回的字段的名称。  
  
## 备注  
 使用 `Select` 子句可以定义要从查询中返回的结果。  这使您可以定义由查询创建的新匿名类型的成员，或指定由查询返回的命名类型的成员。  `Select` 子句不是查询所必需的。  如果未指定 `Select` 子句，查询将根据为当前范围标识的范围变量的所有成员返回一个类型。  有关更多信息，请参见[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  当查询创建命名类型时，它将返回类型为 <xref:System.Collections.Generic.IEnumerable%601> 的结果，其中 `T` 为创建的类型。  
  
 `Select` 子句可以引用当前范围中的任何变量。  这包括在 `From` 子句（或 `From` 子句）中标识的范围变量。  它还包括由 `Aggregate`、`Let`、`Group By` 或 `Group Join` 子句通过别名创建的任何新变量或查询表达式中之前的 `Select` 子句创建的变量。  `Select` 子句还可以包含静态值。  例如，下面的代码示例演示查询表达式，其中，`Select` 子句将查询结果定义为具有以下四个成员的新匿名类型：`ProductName`、`Price`、`Discount` 和 `DiscountedPrice`。  `ProductName` 和 `Price` 成员值取自 `From` 子句中定义的产品范围变量。  `DiscountedPrice` 成员值是在 `Let` 子句中计算的。  `Discount` 成员是一个静态值。  
  
 [!code-vb[VbSimpleQuerySamples#27](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_1.vb)]  
  
 `Select` 子句为后续查询子句引入一组新的范围变量，而之前的范围变量不再位于范围中。  查询表达式中的最后一个 `Select` 子句确定查询的返回值。  例如，下面的查询返回总数超过 500 的每个客户订单的公司名称和订单 ID。  第一个 `Select` 子句标识了 `Where` 子句和第二个 `Select` 子句的范围变量。  第二个 `Select` 子句将查询返回的值标识为新的匿名类型。  
  
 [!code-vb[VbSimpleQuerySamples#28](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_2.vb)]  
  
 如果 `Select` 子句标识了要返回的单个项，则查询表达式将返回该项的类型集合。  如果 `Select` 子句标识了要返回的多个项，则查询表达式根据所选项返回新匿名类型的集合。  例如，下面两个查询根据 `Select` 子句返回两个不同类型的集合。  第一个查询返回字符串形式的公司名称的集合。  第二个查询返回用公司名称和地址信息填充的 `Customer` 对象的集合。  
  
 [!code-vb[VbSimpleQuerySamples#29](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_3.vb)]  
  
## 示例  
 下面的查询表达式使用 `From` 子句为 `customers` 集合声明范围变量 `cust`。  `Select` 子句选择客户名称和 ID 值，并填充新范围变量的 `CompanyName` 和 `CustomerID` 列。  `For Each` 语句循环访问返回的每个对象，并显示每条记录的 `CompanyName` 和 `CustomerID` 列。  
  
 [!code-vb[VbSimpleQuerySamples#30](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/select-clause_4.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)