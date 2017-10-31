---
title: "使用 Visual Basic 运算符执行的常规任务 | Microsoft Docs"
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
  - "运算符 [Visual Basic], 算法"
  - "运算符 [Visual Basic], 移位"
  - "运算符 [Visual Basic], 按位"
  - "运算符 [Visual Basic], 比较"
  - "运算符 [Visual Basic], 串联"
  - "运算符 [Visual Basic], 逻辑"
  - "运算符 [Visual Basic], 短路逻辑"
  - "运算符 [Visual Basic], 字符串比较"
  - "运算符 [Visual Basic], 字符串串联"
  - "Visual Basic 代码, 运算符"
ms.assetid: d181afe5-fafa-460f-a13b-81203f6f4587
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 使用 Visual Basic 运算符执行的常规任务
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

运算符执行的许多常规任务都涉及到一个或多个表达式（称为“操作数”）。  
  
## 算术和移位任务  
 下表概括了可用的算术和移位运算。  
  
|||  
|-|-|  
|若要|请参见|  
|将一个数值与另一个数值相加|[\+ 运算符](../../../../visual-basic/language-reference/operators/addition-operator.md)|  
|从一个数值中减去另一个数值|[\- 运算符](../../../../visual-basic/language-reference/operators/subtraction-operator.md)|  
|反转数值的符号|[\- 运算符](../../../../visual-basic/language-reference/operators/subtraction-operator.md)|  
|将一个数值与另一个数值相乘|[\* 运算符](../../../../visual-basic/language-reference/operators/multiplication-operator.md)|  
|将一个数值除以另一个数值|[\/ 运算符](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md)|  
|查找一个数值被另一个数值相除所得的商（不包括余数）|[\\ 运算符](../../../../visual-basic/language-reference/operators/integer-division-operator.md)|  
|查找一个数值被另一个数值相除所得的余数（不包括商）|[Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md)|  
|将一个数值自乘另一个数值的幂|[^ 运算符](../../../../visual-basic/language-reference/operators/exponentiation-operator.md)|  
|将某个数值的位模式向左移|[\<\< 运算符](../../../../visual-basic/language-reference/operators/left-shift-operator.md)|  
|将某个数值的位模式向右移|[\>\> 运算符](../../../../visual-basic/language-reference/operators/right-shift-operator.md)|  
  
## 比较任务  
 下表概括了可用的比较运算。  
  
|||  
|-|-|  
|若要|请参见|  
|确定两个值是否相等|`=` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定两个值是否不相等|`<>` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定一个值是否小于另一个值|`<` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定一个值是否大于另一个值|`>` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定一个值是否小于或等于另一个值|`<=` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定一个值是否大于或等于另一个值|`>=` 运算符 \([比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)\)|  
|确定两个对象变量是否引用同一对象实例|[Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)|  
|确定两个对象变量是否引用不同对象实例|[IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)|  
|确定对象是否为某个特定类型|[TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md)|  
  
## 串联任务  
 下表概括了可用的串联运算。  
  
|||  
|-|-|  
|若要|请参见|  
|将多个字符串联接为一个字符串|`&` 运算符 \([串联运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)\)|  
|联接数值与字符串值|`+` 运算符 \([串联运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)\)|  
  
## 逻辑和按位任务  
 下表概括了可用的逻辑和按位运算。  
  
|||  
|-|-|  
|若要|请参见|  
|对 Boolean 值执行逻辑求反|[Not 运算符](../../../../visual-basic/language-reference/operators/not-operator.md)|  
|对两个 Boolean 值执行逻辑合取|[And 运算符](../../../../visual-basic/language-reference/operators/and-operator.md)|  
|对两个 Boolean 值执行包容性逻辑析取|[Or 运算符](../../../../visual-basic/language-reference/operators/or-operator.md)|  
|对两个 Boolean 值执行排它性逻辑析取|[异或运算符](../../../../visual-basic/language-reference/operators/xor-operator.md)|  
|对两个 Boolean 值执行短路逻辑合取|[AndAlso 运算符](../../../../visual-basic/language-reference/operators/andalso-operator.md)|  
|对两个 Boolean 值执行短路包容性逻辑析取|[OrElse 运算符](../../../../visual-basic/language-reference/operators/orelse-operator.md)|  
|对两个整数值执行按位逻辑合取|[And 运算符](../../../../visual-basic/language-reference/operators/and-operator.md)|  
|对两个整数值执行按位包容性逻辑析取|[Or 运算符](../../../../visual-basic/language-reference/operators/or-operator.md)|  
|对两个整数值执行按位排它性逻辑析取|[异或运算符](../../../../visual-basic/language-reference/operators/xor-operator.md)|  
|对整数值执行按位逻辑求反|[Not 运算符](../../../../visual-basic/language-reference/operators/not-operator.md)|  
  
## 请参阅  
 [运算符和表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [按功能列出的运算符](../../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)