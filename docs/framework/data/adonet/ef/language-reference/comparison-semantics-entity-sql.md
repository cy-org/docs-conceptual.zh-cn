---
title: "比较语义 (Entity SQL) | Microsoft Docs"
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
ms.assetid: b36ce28a-2fe4-4236-b782-e5f7c054deae
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 比较语义 (Entity SQL)
执行下列任一 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 运算符时都涉及类型实例的比较：  
  
## 显式比较  
 相等运算：  
  
-   \=  
  
-   \!\=  
  
 排序运算：  
  
-   \<  
  
-   \<\=  
  
-   \>  
  
-   \>\=  
  
 判断是否可为 Null 的运算：  
  
-   IS NULL  
  
-   IS NOT NULL  
  
## 显式区别  
 相等区别：  
  
-   DISTINCT  
  
-   GROUP BY  
  
 排序区别：  
  
-   ORDER BY  
  
## 隐式区别  
 集运算和谓词（相等）：  
  
-   UNION  
  
-   INTERSECT  
  
-   EXCEPT  
  
-   SET  
  
-   OVERLAPS  
  
 项谓词（相等）：  
  
-   IN  
  
## 支持的组合  
 下表说明了每种类型的比较运算符的所有受支持的组合：  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**类型**|**\=**<br /><br /> **\!\=**|**GROUP BY**<br /><br /> **DISTINCT**|**UNION**<br /><br /> **INTERSECT**<br /><br /> **EXCEPT**<br /><br /> **SET**<br /><br /> **OVERLAPS**|**IN**|**\<   \<\=**<br /><br /> **\>   \>\=**|**ORDER BY**|**IS NULL**<br /><br /> **IS NOT NULL**|  
|实体类型|引用<sup>1</sup>|所有属性<sup>2</sup>|所有属性<sup>2</sup>|所有属性<sup>2</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引用<sup>1</sup>|  
|复杂类型|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|  
|行|所有属性<sup>4</sup>|所有属性<sup>4</sup>|所有属性<sup>4</sup>|引发<sup>3</sup>|引发<sup>3</sup>|所有属性<sup>4</sup>|引发<sup>3</sup>|  
|基元类型|特定于提供程序|特定于提供程序|特定于提供程序|特定于提供程序|特定于提供程序|特定于提供程序|特定于提供程序|  
|多集|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|  
|引用|是 <sup>5</sup>|是 <sup>5</sup>|是 <sup>5</sup>|是 <sup>5</sup>|引发|引发|是 <sup>5</sup>|  
|关联<br /><br /> 类型|引发<sup>3</sup>|引发|引发|引发|引发<sup>3</sup>|引发<sup>3</sup>|引发<sup>3</sup>|  
  
 <sup>1</sup>给定实体类型实例的引用被隐式比较，如下面的示例所示：  
  
```  
SELECT p1, p2   
FROM AdventureWorksEntities.Product AS p1   
     JOIN AdventureWorksEntities.Product AS p2   
WHERE p1 != p2 OR p1 IS NULL  
```  
  
 不能将实体实例与显式引用进行比较。  如果试图这么做，则会引发异常。  例如，以下查询将引发异常：  
  
```  
SELECT p1, p2   
FROM AdventureWorksEntities.Product AS p1   
     JOIN AdventureWorksEntities.Product AS p2   
WHERE p1 != REF(p2)  
```  
  
 <sup>2</sup>复杂类型的属性在发送到存储之前被转换为扁平类型，因此它们变得可比较（前提是它们的所有属性可比较）。  另请参见 <sup>4</sup>。  
  
 <sup>3</sup>实体框架运行库检测到不受支持的情况，并在不牵扯提供程序\/存储的情况下引发有意义的异常。  
  
 <sup>4</sup>试图比较所有属性。  如果某个属性的类型不可比较，例如 text、ntext 或 image，则可能引发服务器异常。  
  
 <sup>5</sup>比较引用的所有单个元素（这包括实体集名称和该实体类型的所有键属性）。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)