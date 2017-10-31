---
title: "如何：在一个变量中保存多个值 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数组 [Visual Basic], 编译错误"
  - "数组 [Visual Basic], 复合数据类型"
  - "类 [Visual Basic], 复合数据类型"
  - "复合数据类型"
  - "复合类型"
  - "数据类型 [Visual Basic], 复合"
  - "结构, 复合数据类型"
  - "类型 [Visual Basic], 复合"
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：在一个变量中保存多个值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果将某个变量声明为*“复合数据类型”*，则该变量可保存多个值。  
  
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md) 包括结构、数组和类。  复合数据类型的变量可保存基本数据类型和其他复合类型的组合。  结构和类可保存代码和数据。  
  
### 在变量中保存多个值  
  
1.  确定变量要使用何种复合数据类型。  
  
2.  如果该复合数据类型尚未定义，则定义此数据类型，以供变量使用。  
  
    -   使用 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md) 定义结构。  
  
    -   使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 定义数组。  
  
    -   使用 [Class 语句](../../../../visual-basic/language-reference/statements/class-statement.md) 定义类。  
  
3.  使用 `Dim` 语句声明变量。  
  
4.  变量名后接 `As` 子句。  
  
5.  `As` 关键字后接适当的复合数据类型的名称。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)