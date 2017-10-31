---
title: "&amp; 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.&"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "& 运算符"
  - "“and”运算符 (&amp;)"
  - "And (&amp;) 运算符"
  - "串联运算符, 语法"
  - "字符串 [Visual Basic], 串联"
ms.assetid: fefc3d00-cbf1-475c-8c5e-6fb213b3f85a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &amp; 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

生成两个表达式的字符串连接。  
  
## 语法  
  
```  
  
result = expression1 & expression2  
```  
  
## 部件  
 `result`  
 必选。  任何 `String` 或 `Object` 变量。  
  
 `expression1`  
 必选。  数据类型扩展到 `String` 的任何表达式。  
  
 `expression2`  
 必选。  数据类型扩展到 `String` 的任何表达式。  
  
## 备注  
 如果 `expression1` 或 `expression2` 的数据类型不是 `String`，而是扩大为 `String`，则会将其转换为 `String`。  如果其中一个数据类型没有扩大为 `String`，编译器将产生错误。  
  
 `result` 的数据类型为 `String`。  如果一个或两个表达式的计算结果等于 [Nothing](../../../visual-basic/language-reference/nothing.md) 或者具有值 <xref:System.DBNull.Value?displayProperty=fullName>，则将其视为带有 "" 值的字符串。  
  
> [!NOTE]
>  `&` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
> [!NOTE]
>  符号 \(&\) 也可用于将变量标识为类型 `Long`。  有关更多信息，请参见 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)。  
  
## 示例  
 本示例使用 `&` 运算符来强制字符串连接。  结果是表示两个字符串操作数连接的字符串值。  
  
 [!code-vb[VbVbalrOperators#2](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/concatenation-operator_1.vb)]  
  
## 请参阅  
 [&\= 运算符](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [串联运算符](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [串联运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)