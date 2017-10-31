---
title: ". （成员访问）(Entity SQL) | Microsoft Docs"
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
ms.assetid: 4733e3b2-3efa-4b96-b591-ac31350e96ad
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# . （成员访问）(Entity SQL)
点运算符 \(.\) 是 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 成员访问运算符。  使用成员访问运算符可生成结构化概念模型类型实例的属性或字段的值。  
  
## 语法  
  
```  
expression.identifier  
```  
  
## 参数  
 `expression`  
 结构化概念模型类型的实例。  
  
 `identifier`  
 属于对象实例的属性或字段。  
  
## 备注  
 点 \(.\) 运算符可以用于从记录中提取字段，类似于提取复杂类型或实体类型的属性。  例如，如果类型 Name 的 n 是类型 Person 的成员，而 p 是类型 Person 的实例，则提取 p。  n 是一个产生类型为 Name 的值的有效成员访问表达式。  
  
 `select p.Name.FirstName from LOB.Person as p`  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)