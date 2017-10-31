---
title: "常量必须是内部类型或者枚举类型，不能是类、结构、类型参数或数组类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30424"
  - "bc30424"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30424"
ms.assetid: 2d402c2f-27ad-428b-b699-d45cd62f7196
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 常量必须是内部类型或者枚举类型，不能是类、结构、类型参数或数组类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试将常数声明为类、结构或数组类型，或声明为由包含的泛型类型定义的类型参数。  
  
 常数必须是内部类型（`Boolean`、`Byte`、`Date`、`Decimal`、`Double`、`Integer`、`Long`、`Object`、`SByte`、`Short`、`Single`、`String`、`UInteger`、`ULong` 或 `UShort`），或者是基于整型之一的 `Enum` 类型。  
  
 **错误 ID：**BC30424  
  
### 更正此错误  
  
1.  将常数声明为内部类型或 `Enum` 类型。  
  
2.  常数也可能是某个特定值，例如，`True`、`False` 或 `Nothing`。  编译器将这些预定义的值视为适当的内部类型。  
  
## 请参阅  
 [常量和枚举](../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [数据类型](../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)