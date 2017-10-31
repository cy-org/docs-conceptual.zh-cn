---
title: "未能从委托中推理类型参数 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36564"
  - "vbc36564"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36564"
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 未能从委托中推理类型参数
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

赋值语句使用 `AddressOf` 将泛型过程的地址赋给委托，但它不会为泛型过程提供任何类型参数。  
  
 通常，在调用某个泛型类型时，您将为该泛型类型定义的每个类型参数提供一个类型变量。  如果未提供任何类型变量，编译器将尝试推导要传递给类型参数的类型。  如果上下文未提供足够的信息供编译器推导类型，将产生错误。  
  
 **错误 ID：**BC36564  
  
### 更正此错误  
  
-   为 `AddressOf` 表达式中的泛型过程指定类型参数。  
  
## 请参阅  
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Visual Basic 中的泛型过程](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)   
 [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)