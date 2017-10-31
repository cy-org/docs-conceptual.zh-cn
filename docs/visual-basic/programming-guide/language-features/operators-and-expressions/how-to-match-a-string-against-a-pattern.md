---
title: "如何：将字符串与模式相匹配 (Visual Basic) | Microsoft Docs"
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
  - "比较运算符, 比较字符串"
  - "Like 运算符 [Visual Basic], 模式匹配"
  - "运算符 [Visual Basic], 比较"
  - "模式匹配"
  - "模式匹配, 空字符串"
  - "模式匹配, 字符串比较"
  - "字符串比较 [Visual Basic]"
  - "字符串比较 [Visual Basic], 运算符"
  - "字符串 [Visual Basic], 比较"
  - "Visual Basic 代码, 运算符"
ms.assetid: 19a83804-b5af-4739-928b-ac93e64e457f
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 如何：将字符串与模式相匹配 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果要确定 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md) 的表达式是否与模式相符，则可使用 [Like 运算符](../../../../visual-basic/language-reference/operators/like-operator.md)。  
  
 `Like` 使用两个操作数。  左侧操作数为字符串表达式，右侧操作数为包含匹配所用模式的字符串。  `Like` 返回 `Boolean` 值，该值指示字符串表达式是否满足模式的要求。  
  
 您可以将字符串表达式中的每个字符与具体字符、通配符、字符列表或字符范围进行匹配。  模式字符串中规范的位置与字符串表达式中要进行匹配的字符位置对应。  
  
### 将字符串表达式中的字符与具体的字符进行匹配  
  
-   将具体的字符直接放在模式字符串中。  某些特殊字符必须用括号 \(`[ ]`\) 括起来。  有关更多信息，请参见 [Like 运算符](../../../../visual-basic/language-reference/operators/like-operator.md)。  
  
     下面的示例测试 `myString` 是否只包含 `H` 这一字符。  
  
     [!code-vb[VbVbalrOperators#70](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_1.vb)]  
  
### 将字符串表达式中的字符与通配符进行匹配  
  
-   将问号 \(`?`\) 放在模式字符串中。  此位置的任何有效字符都被视为与模式成功匹配。  
  
     下面的示例测试 `myString` 是否由单一字符 `W` 及其后面的两个为任意值的字符组成。  
  
     [!code-vb[VbVbalrOperators#71](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_2.vb)]  
  
### 将字符串表达式中的字符与字符列表进行匹配  
  
-   将括号 \(`[ ]`\) 放在模式字符串中，并将字符列表放在括号中。  不要在字符之间使用逗号或任何其他分隔符。  字符串表达式的对应位置只要存在列表中的任何单个字符，即可视为与模式成功匹配。  
  
     下面的示例测试 `myString` 是否包含任何有效字符，并且该有效字符后面正好是字符 `A`、`C` 或 `E` 之一。  
  
     [!code-vb[VbVbalrOperators#72](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_3.vb)]  
  
     请注意，该匹配区分大小写。  
  
### 将字符串表达式中的字符与字符范围进行匹配  
  
-   将括号 \(`[ ]`\) 放在模式字符串中，并在括号内放置此字符范围的最大字符和最小字符，它们之间由连字符 \(`–`\) 隔开。  字符串表达式的对应位置只要存在该范围中的任何单个字符，即可视为与模式成功匹配。  
  
     下面的示例测试 `myString` 是否包含字符 `num`，并且其后正好是字符 `i`、`j`、`k`、`l`、`m` 或 `n` 之一。  
  
     [!code-vb[VbVbalrOperators#73](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_4.vb)]  
  
     请注意，该匹配区分大小写。  
  
## 匹配空字符串  
 `Like` 将序列 `[]` 视为零长度字符串 \(`""`\)。  使用 `[]` 可测试整个字符串表达式是否为空，但不能用它测试字符串表达式中的特定位置是否为空。  如果需要测试空位置，则可多次使用 `Like`。  
  
#### 将字符串表达式中的字符与字符列表或空列表进行匹配  
  
1.  在同一个字符串表达式上调用两次 `Like` 运算符，然后用 [Or 运算符](../../../../visual-basic/language-reference/operators/or-operator.md) 或 [OrElse 运算符](../../../../visual-basic/language-reference/operators/orelse-operator.md) 将两次调用连接在一起。  
  
2.  在第一个 `Like` 子句的模式字符串中包含字符列表，并将该列表用括号 \(`[ ]`\) 括起来。  
  
3.  在第二个 `Like` 子句的模式字符串中，不在相关位置放置任何字符。  
  
     下面的示例测试 7 位电话号码 `phoneNum` 中是否首先是 3 个数字，接着是一个空格、一个连字符 \(`–`\)、一个句点 \(`.`\) 或无任何字符，再接着是 4 个数字。  
  
     [!code-vb[VbVbalrOperators#74](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_5.vb)]  
  
## 请参阅  
 [比较运算符](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [运算符和表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Like 运算符](../../../../visual-basic/language-reference/operators/like-operator.md)   
 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)