---
title: "用户定义的函数 (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f9e6bbd-8e5a-43e1-809f-f8a61338e522
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 用户定义的函数 (Entity SQL)
Entity SQL 支持在查询中调用用户定义函数。  可以将这些函数定义为与查询内联（请参见[How to: Call a User\-Defined Function](http://msdn.microsoft.com/zh-cn/ad131b86-8b4e-4747-8605-d4fc64fb9d02)）或将它们定义为概念模型的一部分（请参见[How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/zh-cn/0dad7b8b-58f6-4271-b238-f34810d68e5f)）。  概念模型函数定义为概念模型中 [Function](http://msdn.microsoft.com/zh-cn/dc3beca7-55cf-4977-8db0-5064cdbab134) 元素的 [DefiningExpression](http://msdn.microsoft.com/zh-cn/d3da8d8b-a048-47ee-8d81-0c2ea3acdd3e) 元素中的 Entity SQL 命令。  
  
 通过 Entity SQL，您可以在查询命令自身中定义函数。  [FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) 运算符定义内联函数。  您可以在单个命令中定义多个函数，这些函数可以具有相同的函数名称，只要函数签名是唯一的。  有关详细信息，请参阅[函数重载解析](../../../../../../docs/framework/data/adonet/ef/language-reference/function-overload-resolution-entity-sql.md)。  
  
## 请参阅  
 [函数](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)