---
title: "Group By 子句 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.QueryGroupByInto
- vb.QueryGroupBy
- vb.QueryGroupRef
- vb.QueryGroupInto
- vb.QueryGroup
dev_langs:
- VB
helpviewer_keywords:
- queries [Visual Basic], Group By
- Group By statement
- Group By clause
ms.assetid: b1b5dcea-6654-473b-a2db-01f7e4c265d7
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a40074c4602d6c0164c784d497fbfb134402bf62
ms.lasthandoff: 03/13/2017

---
# <a name="group-by-clause-visual-basic"></a>Group By 子句 (Visual Basic)
对查询结果的元素进行分组。 也可用于将聚合函数应用于每个组。 分组运算基于一个或多个键。  
  
## <a name="syntax"></a>语法  
  
```  
Group [ listField1 [, listField2 [...] ] By keyExp1 [, keyExp2 [...] ]  
  Into aggregateList  
```  
  
## <a name="parts"></a>部件  
  
-   `listField1`, `listField2`  
  
     可选。 分组结果中将包括一个或多个显式标识字段的查询变量的一个或多个字段。 如果未指定字段，则分组结果中将包括一个或多个查询变量的所有字段。  
  
-   `keyExp1`  
  
     必需。 标识键以用于确定元素所在的组的表达式。 可以指定多个键以形成组合键。  
  
-   `keyExp2`  
  
     可选。 与 `keyExp1` 结合以形成组合键的一个或多个其他键。  
  
-   `aggregateList`  
  
     必需。 标识如何对组进行聚合的一个或多个表达式。 若要标识分组结果的成员名称，请使用 `Group` 关键字，它可以采用以下任意一种形式：  
  
    ```  
    Into Group  
    ```  
  
     - 或 -  
  
    ```  
    Into <alias> = Group  
    ```  
  
     还可以包含聚合函数以将其应用于该组。  
  
## <a name="remarks"></a>备注  
 可以使用 `Group By` 子句来将查询的结果分解为组。 分组基于某个键或包含多个键的组合键。 与匹配的键值相关联的元素包括在同一组中。  
  
 使用 `aggregateList` 子句的 `Into` 参数和 `Group` 关键字来标识用于引用该组的成员名称。 还可以将聚合函数包括在 `Into` 子句中，以计算分组元素的值。 标准聚合函数的列表，请参阅[Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例根据客户所在的位置（国家/地区）对客户列表进行分组，并提供了每个组中的客户计数。 按国家/地区名称对结果进行排序。 按城市名称对分组结果进行排序。  
  
 [!code-vb[VbSimpleQuerySamples #&11;](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/group-by-clause_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Group Join 子句](../../../visual-basic/language-reference/queries/group-join-clause.md)
