---
title: "用作可选参数类型的泛型参数必须受类约束 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32124"
  - "bc32124"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32124"
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 用作可选参数类型的泛型参数必须受类约束
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

通过某个可选参数声明了过程，该参数使用未约束为引用类型的类型参数。  
  
 必须始终为每个可选参数提供默认值。  如果参数采用引用类型，则可选值必须为 `Nothing`，该值对于任何引用类型均为有效值。  但是，如果参数采用值类型，则该类型必须为 Visual Basic 预定义的基本数据类型。  这是因为复合值类型（如用户定义的结构）没有有效的默认值。  
  
 在为可选参数使用类型参数时，必须保证它采用引用类型，以避免值类型没有有效默认值的可能性。  这意味着，您必须使用 `Class` 关键字或某个具体类的名称来约束类型参数。  
  
 **错误 ID：**BC32124  
  
### 更正此错误  
  
-   约束类型参数以便只接受引用类型，或者，不要为可选参数使用它。  
  
## 请参阅  
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [可选参数](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Nothing](../../../visual-basic/language-reference/nothing.md)