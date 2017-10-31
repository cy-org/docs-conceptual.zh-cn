---
title: "SELECT (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
ms.assetid: 9a33bd0d-ded1-41e7-ba3c-305502755e3b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# SELECT (Entity SQL)
指定查询所返回的元素。  
  
## 语法  
  
```  
  
SELECT [ ALL | DISTINCT ] [ topSubclause ] aliasedExpr   
      [{ , aliasedExpr }] FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause ]  
or  
SELECT VALUE [ ALL | DISTINCT ] [ topSubclause ] expr FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause  
```  
  
## 参数  
 ALL  
 指定结果集中可以出现重复项。 ALL 为默认值。  
  
 DISTINCT  
 指定结果集中只能出现唯一的结果。  
  
 VALUE  
 仅允许指定一个项，且不添加到行包装上。  
  
 `topSubclause`  
 任何指示从查询返回的首批结果数的有效表达式（形式为 `top (``expr``)`）。  
  
 使用 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 运算符的 LIMIT 参数也可以选择结果集中的前 n 个项。  
  
 `aliasedExpr`  
 形式如下的表达式：  
  
 `expr` 作为 `identifier` &#124; `expr`  
  
 `expr`  
 文本或表达式。  
  
## 备注  
 SELECT 子句在计算 [FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)、[GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md) 和 [HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md) 子句之后进行计算。 SELECT 子句只能引用当前处于范围内的项（FROM 子句指定的范围或外部范围）。 如果指定了 GROUP BY 子句，则仅允许 SELECT 子句引用 GROUP BY 键的别名。 仅允许在聚合函数中引用 FROM 子句项。  
  
 跟在 SELECT 关键字之后的一个或多个查询表达式的列表称为“选择列表”，更加正式的名称为“投影”。 最普通的投影形式为单个查询表达式。 如果从集合 `member1`  选择一个成员 `collection1`，则会生成 `member1`  中每个对象的所有 `collection1`值的新集合（如下面的示例所示）。  
  
```  
SELECT collection1.member1 FROM collection1  
```  
  
 例如，如果 `customers` 是类型为 `Customer` 的集合，且该类型有类型为  `Name`  的属性`string`，则从 `Name` 选择 `customers` 将生成一个字符串集合（如下面的示例所示）。  
  
```  
SELECT customers.Name FROM customers AS c  
```  
  
 也可以使用 JOIN 语法（FULL、INNER、LEFT、OUTER、ON 和 RIGHT）。 ON 是内部联接的必需语法，但不允许用于交叉联接。  
  
## 行和值选择子句  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持 SELECT 子句的两种变体。 第一种变体是行选择，由 SELECT 关键字标识，可以用于指定应提取出的一个或多个值。 由于返回值的两侧会隐式添加行包装，因此查询表达式的结果始终为行的多集。  
  
 行选择中的每个查询表达式都必须指定一个别名。 如果不指定别名，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 会尝试使用别名生成规则生成别名。  
  
 SELECT 子句的另一种变体为值选择，由 SELECT VALUE 关键字标识。 该变体仅允许指定一个值，且不添加行包装。  
  
 行选择总是可通过 VALUE SELECT 进行表示（如下面的示例所示）。  
  
```  
SELECT 1 AS a, "abc" AS b FROM C  
SELECT VALUE ROW(1 AS a, "abc" AS b) FROM C   
```  
  
## All 和 Distinct 修饰符  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中的两种 SELECT 变体都允许指定 ALL 或 DISTINCT 修饰符。 如果指定 DISTINCT 修饰符，则将从查询表达式（直到并包括 SELECT 子句）生成的集合中消除重复项。 如果指定 ALL 修饰符，则不消除重复项；ALL 为默认值。  
  
## 与 Transact\-SQL 的区别  
 与 Transact\-SQL 不同，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 不支持在 SELECT 子句中使用 \* 参数。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 允许查询通过从 FROM 子句引用集合别名来提取出完整的记录（如下面的示例所示）。  
  
```  
SELECT * FROM T1, T2  
```  
  
 上面的 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 查询表达式在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中表示如下。  
  
```  
SELECT a1, a2 FROM T1 AS a1, T2 AS a2  
```  
  
## 示例  
 下面的 Entity SQL 查询使用 SELECT 运算符指定查询要返回的元素。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1.  执行 [如何：执行返回 StructuralType 结果的查询](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md) 中的过程。  
  
2.  将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#LESS](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#less)]  
  
## 请参阅  
 [查询表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)   
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)