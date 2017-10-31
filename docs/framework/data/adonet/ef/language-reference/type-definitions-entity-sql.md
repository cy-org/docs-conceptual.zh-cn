---
title: "类型定义 (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 类型定义 (Entity SQL)
类型定义用在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 内联函数的声明语句中。  
  
## 备注  
 内联函数的声明语句的组成为：[FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) 关键字，后跟表示函数名称的标识符（例如，“MyAvg”），接着是放在括号中的参数定义列表（例如，“dues Collection\(Decimal\)”）。  
  
 参数定义列表由零个或多个参数定义组成。  每个参数定义均由一个标识符（该函数的参数的名称，例如“dues”）后跟类型定义（例如，“Collection\(Decimal\)”）组成。  
  
 类型定义可以为以下任一情况：  
  
-   标识符的类型（例如，“Int32”或“AdventureWorks.Order”）。  
  
-   关键字 `COLLECTION` 后跟放在括号中的另一个类型定义（例如，“Collection\(AdventureWorks.Order\)”）。  
  
-   关键字 ROW 后跟放在括号中的属性定义列表（例如，“Row\(x AdventureWorks.Order\)”）。  属性定义具有格式，例如“`identifier type_definition`, `identifier type_definition`, ...”。  
  
-   关键字 REF 后跟放在括号中的标识符类型（例如，“Ref\(AdventureWorks.Order\)”）。  REF 类型定义运算符要求将实体类型作为参数。  您不能指定基元类型作为参数。  
  
 还可以嵌套类型定义（例如，“Collection\(Row\(x Ref\(AdventureWorks.Order\)\)\)”）。  
  
 类型定义选项为：  
  
-   `IdentifierName supported_type` 或  
  
-   `IdentifierName` COLLECTION\(`type_definition`\) 或  
  
-   `IdentifierName` ROW\(`property_definition`\) 或  
  
-   `IdentifierName` REF\(`supported_entity_type`\)  
  
 属性定义选项为 `IdentifierName type_definition`。  
  
 支持的类型为当前命名空间中的任何类型。  它们包括基元类型和实体类型。  
  
 支持的实体类型仅仅是当前命名空间中的实体类型。  而不包括基元类型。  
  
## 示例  
 下面是一个简单类型定义的示例。  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 下面是 COLLECTION 类型定义的示例。  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 下面是 ROW 类型定义的示例。  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 下面是 REF 类型定义的示例。  
  
```  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)