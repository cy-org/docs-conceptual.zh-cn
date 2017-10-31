---
title: "Entity SQL 参考 | Microsoft Docs"
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
ms.assetid: 61ce7ee1-ffe2-477d-8a9f-835b0a11d900
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Entity SQL 参考
本节包含 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 参考主题。本主题汇总了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 运算符并按类别对其分组。  
  
## 算术运算符  
 算术运算符对两个表达式执行数学运算，这两个表达式可以是一个或多个数值数据类型。  下表列出了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 算术运算符。  
  
|运算符|使用|  
|---------|--------|  
|[\+（添加）](../../../../../../docs/framework/data/adonet/ef/language-reference/add.md)|加法。|  
|[\/（除）](../../../../../../docs/framework/data/adonet/ef/language-reference/divide-entity-sql.md)|除法。|  
|[%（取模）](../../../../../../docs/framework/data/adonet/ef/language-reference/modulo-entity-sql.md)|返回除法运算的余数。|  
|[\*（乘）](../../../../../../docs/framework/data/adonet/ef/language-reference/multiply-entity-sql.md)|乘法。|  
|[\-（负号）](../../../../../../docs/framework/data/adonet/ef/language-reference/negative-entity-sql.md)|求反。|  
|[\-（减）](../../../../../../docs/framework/data/adonet/ef/language-reference/subtract-entity-sql.md)|减法。|  
  
## 规范函数  
 所有数据提供程序都支持规范函数，并且所有查询技术都可以使用规范函数。  下表列出了规范函数。  
  
|函数|类型|  
|--------|--------|  
|[聚合 Entity SQL 规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)|讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 聚合规范函数。|  
|[数学规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/math-canonical-functions.md)|讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 数学规范函数。|  
|[字符串规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/string-canonical-functions.md)|讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 字符串规范函数。|  
|[日期和时间规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/date-and-time-canonical-functions.md)|讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 日期和时间规范函数。|  
|[按位规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/bitwise-canonical-functions.md)|讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 按位规范函数。|  
|[其他规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/other-canonical-functions.md)|讨论未分类为按位、日期\/时间、字符串、数字或聚合函数的函数。|  
  
## 比较运算符  
 比较运算符适用于下列类型：`Byte`、`Int16`、`Int32`、`Int64`、`Double`、`Single`、`Decimal`、`String`、`DateTime`、`Date`、`Time`、`DateTimeOffset`。  应用比较运算符之前将对操作数进行隐性类型升级。  比较运算符总是生成布尔值。  如果操作数中至少有一个 `null`，则结果为 `null`。  
  
 相等和不相等适用于有标识的所有对象类型，如 `Boolean` 类型。  拥有相同标识的非基元对象被视为相等。  下表列出了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 比较运算符。  
  
|运算符|描述|  
|---------|--------|  
|[\=（等于）](../../../../../../docs/framework/data/adonet/ef/language-reference/equals-entity-sql.md)|比较两个表达式是否相等。|  
|[\> （大于）](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-entity-sql.md)|比较两个表达式以确定左侧表达式的值是否大于右侧表达式的值。|  
|[\>\=（大于或等于）](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-or-equal-to-entity-sql.md)|比较两个表达式以确定左侧表达式的值是否大于或等于右侧表达式的值。|  
|[IS &#91;NOT&#93; NULL](../../../../../../docs/framework/data/adonet/ef/language-reference/isnull-entity-sql.md)|确定查询表达式是否为 null。|  
|[\< （小于）](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-entity-sql.md)|比较两个表达式以确定左侧表达式的值是否小于右侧表达式的值。|  
|[\<\=（小于或等于）](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-or-equal-to-entity-sql.md)|比较两个表达式以确定左侧表达式的值是否小于或等于右侧表达式的值。|  
|[&#91;NOT&#93; BETWEEN](../../../../../../docs/framework/data/adonet/ef/language-reference/between-entity-sql.md)|确定表达式的结果值是否在指定范围内。|  
|[\!\=（不等于）](../../../../../../docs/framework/data/adonet/ef/language-reference/not-equal-to-entity-sql.md)|比较两个表达式以确定左侧表达式是否不等于右侧表达式。|  
|[&#91;NOT&#93; LIKE](../../../../../../docs/framework/data/adonet/ef/language-reference/like-entity-sql.md)|确定特定字符串是否与指定模式相匹配。|  
  
## 逻辑和 Case 表达式运算符  
 逻辑运算符测试条件的真实性。  CASE 表达式计算一组布尔表达式的值以确定结果。  下表列出了逻辑和 Case 表达式运算符。  
  
|运算符|描述|  
|---------|--------|  
|[&&（逻辑与）](../../../../../../docs/framework/data/adonet/ef/language-reference/and-entity-sql.md)|逻辑“与”。|  
|[\!  （逻辑非）](../../../../../../docs/framework/data/adonet/ef/language-reference/not-entity-sql.md)|逻辑非。|  
|[&#124;&#124;（逻辑或）](../../../../../../docs/framework/data/adonet/ef/language-reference/or-entity-sql.md)|逻辑“或”。|  
|[CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md)|求出一组布尔表达式的值以确定结果。|  
|[THEN](../../../../../../docs/framework/data/adonet/ef/language-reference/then-entity-sql.md)|当 [WHEN](http://msdn.microsoft.com/zh-cn/6233fe9f-00b0-460e-8372-64e138a5f998) 子句取值为 true 时的结果。|  
  
## 查询运算符  
 查询运算符用于定义返回实体数据的查询表达式。  下表列出了查询运算符。  
  
|运算符|使用|  
|---------|--------|  
|[FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)|指定 [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md) 语句中使用的集合。|  
|[GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md)|指定由查询 \([SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)\) 表达式返回的对象要分入的组。|  
|[GroupPartition](../../../../../../docs/framework/data/adonet/ef/language-reference/grouppartition-entity-sql.md)|返回从聚合与之相关的组分区提取的参数值集合。|  
|[HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md)|指定组或聚合的搜索条件。|  
|[LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)|与 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 子句一起使用，以执行物理分页。|  
|[ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)|指定用于 [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md) 语句所返回的对象的排序顺序。|  
|[SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)|指定投影中由查询返回的元素。|  
|[SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)|与 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 子句一起使用，以执行物理分页。|  
|[TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)|指定查询结果中将只返回第一组行。|  
|[WHERE](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md)|按条件筛选由查询返回的数据。|  
  
## 引用运算符  
 引用是指向特定实体集中的特定实体的逻辑指针（外键）。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持使用以下运算符对引用进行构造、解构和导航：  
  
|运算符|使用|  
|---------|--------|  
|[CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)|创建对实体集中的实体的引用。|  
|[DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)|取消引用一个引用值，并生成该取消引用的结果。|  
|[KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)|提取引用或实体表达式的键。|  
|[NAVIGATE](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)|使您可以从一个实体类型到另一个实体类型对关系进行导航|  
|[REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)|返回对实体实例的引用。|  
  
## 集运算符  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供了各种功能强大的集运算符。  这包括与 Transact\-SQL 运算符类似的集运算符，例如 UNION、INTERSECT、EXCEPT 和 EXISTS。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 还支持用于清除重复项 \(SET\)、成员身份测试 \(IN\) 和联接 \(JOIN\) 的运算符。  下表列出了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 集运算符。  
  
|运算符|使用|  
|---------|--------|  
|[ANYELEMENT](../../../../../../docs/framework/data/adonet/ef/language-reference/anyelement-entity-sql.md)|从多值集合中提取元素。|  
|[EXCEPT](../../../../../../docs/framework/data/adonet/ef/language-reference/except-entity-sql.md)|返回由 EXCEPT 操作数左侧的查询表达式返回而不由 EXCEPT 操作数右侧的查询表达式返回的任何非重复值的集合。|  
|[&#91;NOT&#93; EXISTS](../../../../../../docs/framework/data/adonet/ef/language-reference/exists-entity-sql.md)|确定集合是否为空。|  
|[FLATTEN](../../../../../../docs/framework/data/adonet/ef/language-reference/flatten-entity-sql.md)|将一个由多个集合组成的集合转换为一个平展集合。|  
|[&#91;NOT&#93; IN](../../../../../../docs/framework/data/adonet/ef/language-reference/in-entity-sql.md)|确定某个值是否与某个集合中的任何值匹配。|  
|[INTERSECT](../../../../../../docs/framework/data/adonet/ef/language-reference/intersect-entity-sql.md)|返回 INTERSECT 操作数左右两边的两个查询表达式均返回的所有非重复值的集合。|  
|[OVERLAPS](../../../../../../docs/framework/data/adonet/ef/language-reference/overlaps-entity-sql.md)|确定两个集合是否具有公共元素。|  
|[SET](../../../../../../docs/framework/data/adonet/ef/language-reference/set-entity-sql.md)|用于通过生成一个新集合（其中移除了所有重复元素）将对象集合转换为一个集。|  
|[UNION](../../../../../../docs/framework/data/adonet/ef/language-reference/union-entity-sql.md)|将两个或更多查询的结果组合成单个集合。|  
  
## 类型运算符  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供了用于构造、查询和操作表达式（值）的类型的运算。  下表列出了用于处理类型的运算符。  
  
|运算符|使用|  
|---------|--------|  
|[CAST](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md)|将一种数据类型的表达式转换为另一种数据类型的表达式。|  
|[COLLECTION](../../../../../../docs/framework/data/adonet/ef/language-reference/collection-entity-sql.md)|用于 [FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) 操作中，以声明实体类型或复杂类型的集合。|  
|[IS &#91;NOT&#93; OF](../../../../../../docs/framework/data/adonet/ef/language-reference/isof-entity-sql.md)|确定表达式的类型是否为指定类型或指定类型的某个子类型。|  
|[OFTYPE](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md)|从查询表达式返回特定类型的对象集合。|  
|[命名类型构造函数](../../../../../../docs/framework/data/adonet/ef/language-reference/named-type-constructor-entity-sql.md)|用于创建实体类型或复杂类型的实例。|  
|[MULTISET](../../../../../../docs/framework/data/adonet/ef/language-reference/multiset-entity-sql.md)|根据值列表创建多集的实例。|  
|[ROW](../../../../../../docs/framework/data/adonet/ef/language-reference/row-entity-sql.md)|从一个或多个值构造结构上类型化的匿名记录。|  
|[TREAT](../../../../../../docs/framework/data/adonet/ef/language-reference/treat-entity-sql.md)|将特定基类型的对象视为指定派生类型的对象。|  
  
## 其他运算符  
 下表列出了其他 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 运算符。  
  
|运算符|使用|  
|---------|--------|  
|[\+（字符串串联）](../../../../../../docs/framework/data/adonet/ef/language-reference/string-concatenation-entity-sql.md)|用于在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中串联字符串。|  
|[.  （成员访问）](../../../../../../docs/framework/data/adonet/ef/language-reference/member-access-entity-sql.md)|用于访问结构化概念模型类型实例的属性或字段的值。|  
|[\-\-（注释）](../../../../../../docs/framework/data/adonet/ef/language-reference/comment-entity-sql.md)|包括 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 注释。|  
|[FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md)|定义可在 Entity SQL 查询中执行的内联函数。|  
  
## 请参阅  
 [Entity SQL 语言](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)