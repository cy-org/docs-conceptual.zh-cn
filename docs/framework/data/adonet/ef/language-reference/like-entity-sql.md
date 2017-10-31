---
title: "LIKE (Entity SQL) | Microsoft Docs"
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
ms.assetid: 8300e6d2-875b-481e-9ef4-e1e7c12d46fa
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# LIKE (Entity SQL)
确定特定字符 `String` 是否与指定模式相匹配。  
  
## 语法  
  
```  
  
match [NOT] LIKE pattern [ESCAPE escape]  
```  
  
## 参数  
 `match`  
 计算结果为 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 的 `String` 表达式。  
  
 `pattern`  
 要与指定 `String` 匹配的模式。  
  
 `escape`  
 一个转义符。  
  
 NOT  
 指定对 LIKE 的结果取反。  
  
## 返回值  
 如果 `true` 与模式相匹配，则为 `string`；否则为 `false`。  
  
## 备注  
 使用 LIKE 运算符的 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 表达式的计算方式十分类似于将相等性用作筛选条件的表达式。 但是，使用 LIKE 运算符的 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 表达式可以包含文本和通配符。  
  
 下表说明模式 `string` 的语法。  
  
|通配符|描述|示例|  
|---------|--------|--------|  
|%|包含零个或零个以上字符的任何 `string`。|`title like '%computer%'` 查找标题中任何位置包含单词 `"computer"` 的所有标题。|  
|\_（下划线）|任意单个字符。|`firstname like '_ean'` 查找所有以 `"ean`" 结尾的四个字母的名字（如 Dean 或 Sean）。|  
|\[ \]|指定范围 \(\[a\-f\]\) 或集合 \(\[abcdef\]\) 中的任意单个字符。|`lastname like '[C-P]arsen'` 查找以“arsen”结尾且以介于 C 与 P 之间的任意单个字符开头的姓氏（如 Carsen 或 Larsen）。|  
|\[^\]|不在指定范围 \(\[^a\-f\]\) 或集合 \(\[^abcdef\]\) 中的任意单个字符。|`lastname like 'de[^l]%'` 查找所有以“de”开头且第三个字母不为“l”的姓氏。|  
  
> [!NOTE]
>  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] LIKE 运算符和 ESCAPE 子句不适用于 `System.DateTime` 或 `System.Guid` 值。  
  
 LIKE 支持 ASCII 模式匹配和 Unicode 模式匹配。 当所有参数都为 ASCII 字符时，将执行 ASCII 模式匹配。 如果一个或多个参数为 Unicode，则所有参数都会转换为 Unicode，并执行 Unicode 模式匹配。 在将 Unicode 与 LIKE 一起使用时，尾随空格有意义；但对非 Unicode，尾随空格则没有意义。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 的模式字符串语法与 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 的模式字符串语法相同。  
  
 模式可以包含常规字符和通配符。 模式匹配过程中，常规字符必须与在字符 `string` 中指定的字符完全匹配。 但是，通配符可以与字符串的任意部分相匹配。 在与通配符一起使用时，LIKE 运算符比 \= 和 \!\= 字符串比较运算符更为灵活。  
  
> [!NOTE]
>  如果是针对特定的提供程序，则可以使用特定于提供程序的扩展。 但是，其他提供程序可能以不同方式对待这类构造。 SqlServer 支持 \[first\-last\] 和 \[^first\-last\] 模式，前一个模式与介于“first”和“last”之间的一个字符完全匹配，而后一个模式与不在“first”和“last”之间的一个字符完全匹配。  
  
### Esc 键  
 使用 ESCAPE 子句可以搜索包含一个或多个特殊通配符（在上一部分的表中进行了介绍）的字符串。 例如，假定有几个文档在标题中包含文本“100%”，而您希望搜索所有这些文档。 由于百分号 \(%\) 字符是通配符，因此若要成功执行搜索，必须使用 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ESCAPE 子句对百分号字符进行转义。 下面是一个此筛选的示例。  
  
```  
"title like '%100!%%' escape '!'"  
```  
  
 在此搜索表达式中，紧跟在惊叹号字符 \(\!\) 之后的百分号通配符 \(%\) 除了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 通配符和方括号 \(`[ ]`\) 字符之外，可以使用任何字符作为转义符。 在前一个示例中，惊叹号 \(\!\) 字符是转义字符。  
  
## 示例  
 下面两个 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询使用 LIKE 和 ESCAPE 运算符确定特定字符串是否与指定模式匹配。 第一个查询搜索以字符 `Name` 开头的 `Down_`。 此查询使用了 ESCAPE 选项，因为下划线 \(`_`\) 为通配符。 如果不指定 ESCAPE 选项，则该查询将搜索所有以单词 `Down` 开头、后跟任意单个字符（下划线字符除外）的 `Name` 值。 这些查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1.  执行 [如何：执行返回 PrimitiveType 结果的查询](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md) 中的过程。  
  
2.  将以下查询作为参数传递给 `ExecutePrimitiveTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#LIKE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#like)]  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)