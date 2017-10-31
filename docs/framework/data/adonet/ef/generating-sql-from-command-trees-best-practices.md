---
title: "从命令目录树生成 SQL - 最佳做法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 71ef6a24-4c4f-4254-af3a-ffc0d855b0a8
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 从命令目录树生成 SQL - 最佳做法
输出查询命令目录树高度模拟可使用 SQL 表示的查询。  但是，对于提供程序编写者而言，从输出命令目录树生成 SQL 还是存在一些常见的难题。  本主题讨论这些难题。  在下一主题中，示例提供程序将演示如何解决这些难题。  
  
## 对 SQL SELECT 语句中的 DbExpression Nodes 进行分组  
 典型的 SQL 语句具有以下形式的嵌套结构：  
  
```  
SELECT …  
FROM …  
WHERE …  
GROUP BY …  
ORDER BY …  
```  
  
 一个或多个子句可能为空。  在任何行中都可能会出现嵌套的 SELECT 语句。  
  
 查询命令目录树到 SQL SELECT 语句可能的转换会针对每个关系运算符产生一个子查询。  然而，这会导致一些难于读取的不必要的子查询。  对于某些数据存储，查询的性能可能会很差。  
  
 例如，考虑下面的查询命令目录树  
  
```  
Project (  
a.x,  
   a = Filter(  
      b.y = 5,   
      b = Scan("TableA")  
   )  
)  
```  
  
 低效率的转换会产生：  
  
```  
SELECT a.x  
FROM (   SELECT *  
         FROM TableA as b  
         WHERE b.y = 5) as a  
```  
  
 请注意，每个关系表达式节点都成为一个新的 SQL SELECT 语句。  
  
 因此，在保持正确的同时，一定要将尽可能多的表达式节点聚合到单个 SQL SELECT 语句中。  
  
 上面的示例的此类聚合的结果为：  
  
```  
SELECT b.x   
FROM TableA as b  
WHERE b.y = 5  
```  
  
## 平展 SQL SELECT 语句中的联接  
 将多个节点聚合成单个 SQL SELECT 语句的一种情况是将多个联接表达式聚合成单个 SQL SELECT 语句。  DbJoinExpression 表示两个输入之间的单一联接。  但是，作为单个 SQL SELECT 语句的一部分，可以指定多个联接。  在这种情况下，将按指定的顺序执行这些联接。  
  
 左侧刺联接（显示为另一个联接的左侧子级的联接）可以更加轻松地平展成单个 SQL SELECT 语句。  例如，考虑以下查询命令目录树：  
  
```  
InnerJoin(  
   a = LeftOuterJoin(  
   b = Extent("TableA")  
   c = Extent("TableB")  
   ON b.y = c.x ),  
   d = Extent("TableC")   
   ON a.b.y = d.z  
)  
```  
  
 这可以正确地转换成：  
  
```  
SELECT *  
FROM TableA as b  
LEFT OUTER JOIN TableB as c ON b.y = c.x  
INNER JOIN TableC as d ON b.y = d.z  
```  
  
 但是，非左侧刺联接无法轻松地平展，而且您也不应尝试去平展它们。  例如，以下查询命令目录树中的联接：  
  
```  
InnerJoin(  
   a = Extent("TableA")   
   b = LeftOuterJoin(  
   c = Extent("TableB")  
   d = Extent("TableC")  
   ON c.y = d.x),  
   ON a.z = b.c.y  
)  
```  
  
 将转换成一个包含子查询的 SQL SELECT 语句。  
  
```  
SELECT *  
FROM TableA as a  
INNER JOIN (SELECT *   
   FROM TableB as c   
   LEFT OUTER JOIN TableC as d  
   ON c.y = d.x) as b  
ON b.y = d.z  
```  
  
## 输入别名重定向  
 为了解释输入别名重定向，请先考虑关系表达式的结构，如 DbFilterExpression、DbProjectExpression、DbCrossJoinExpression、DbJoinExpression、DbSortExpression、DbGroupByExpression、DbApplyExpression 和 DbSkipExpression。  
  
 上述每种类型都具有一个或多个用于描述输入集合的 Input 属性，并且每个输入都对应一个绑定变量，用于在集合遍历期间表示该输入的每个元素。  当引用输入元素时（例如在 DbFilterExpression 的 Predicate 属性中或者在 DbProjectExpression 的 Projection 属性中），将使用相应的绑定变量。  
  
 在将更多的关系表达式节点聚合成单个 SQL SELECT 语句，并在计算一个作为关系表达式的一部分的表达式（例如 DbProjectExpression 的 Projection 属性的一部分）时，它所使用的绑定变量可能与输入的别名不相同，这是因为多个表达式绑定必须重定向到一个范围。  这个问题称作“别名重命名”。  
  
 考虑本主题中的第一个示例。  如果进行自然转换并转换 Projection a.x \(DbPropertyExpression\(a, x\)\)，正确做法是将其转换为 `a.x`，因为我们已为输入提供别名“a”来匹配绑定变量。  但是，在将两个节点聚合成单个 SQL SELECT 语句时，需要将相同的 DbPropertyExpression 转换为 `b.x`，因为输入的别名已改为“b”。  
  
## 联接别名平展  
 与输出命令目录树中的任何其他关系表达式不同，DbJoinExpression 输出一个结果类型，该结果类型是一个由两列组成的行，每一列都对应一个输入。  当生成 DbPropertyExpresssion 以访问源自某个联接的标量属性时，它位于另一个 DbPropertyExpresssion 之上。  
  
 示例包括示例 2 中的“a.b.y”和示例 3 中的“b.c.y”。  但是，在对应的 SQL 语句中这些内容称为“b.y”。  这一重新设定别名问题称为“联接别名平展”。  
  
## 列名和范围别名重命名  
 如果必须使用预测完成具有一个联接的 SQL SELECT 查询，则当枚举输入中的所有参与列时，可能会发生名称冲突，因为多个输入可能具有相同的列名。  为同名列使用不同的名称可避免名称冲突。  
  
 此外，当平展联接时，参与的表（或子查询）可能存在互相冲突的别名，这种情况下需要进行重命名。  
  
## 避免 SELECT \*  
 不要使用 `SELECT *` 从基表中进行选择。  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]应用程序中的存储模型只能包含数据库表中的列的子集。  在这种情况下，`SELECT *` 可能产生不正确的结果。  替代方法是，应通过使用参与的表达式的结果类型中的列名，指定所有参与的列。  
  
## 重用表达式  
 在由 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 传递的查询命树中可以重用表达式。不要假定每个表达式在查询命令树中仅出现一次。  
  
## 映射基元类型  
 在将概念 \(EDM\) 类型映射到提供程序类型时，应映射到最宽的类型 \(Int32\)，以便适合所有可能的值。  此外，避免映射到无法用于许多操作的类型，如 BLOB 类型（例如，[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 中的 `ntext`）。  
  
## 请参阅  
 [SQL 生成](../../../../../docs/framework/data/adonet/ef/sql-generation.md)