---
title: "&gt;&gt; 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.>>"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - ">> 运算符 [Visual Basic]"
  - "移位运算符"
  - "运算符 >>"
  - "运算符 >>"
  - "右移位运算符"
ms.assetid: 054dc6a6-47d9-47ef-82da-cfa2b59fbf8f
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# &gt;&gt; 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对位模式执行数学右移位。  
  
## 语法  
  
```  
  
result = pattern >> amount  
```  
  
## 部件  
 `result`  
 必选。  整型数值。  对该位模式进行移位的结果。  数据类型与 `pattern` 的数据类型相同。  
  
 `pattern`  
 必选。  整型数值表达式。  要进行移位的位模式。  数据类型必须为整型（`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 或 `ULong`）。  
  
 `amount`  
 必选。  数值表达式。  要将该位模式移位的位数。  数据类型必须为 `Integer` 或扩展到 `Integer`。  
  
## 备注  
 数学移位不是循环的，即不会将在结果的一端移出的数位从另一端重新移入。  在数学右移位运算中，将丢弃移出最右侧数位位置的数位，并将最左侧的（符号）数位传播到左端空出的数位位置。  这意味着如果 `pattern` 为负值，空出的位置将设置为一；否则，将设置为零。  
  
 请注意，数据类型 `Byte`、`UShort`、`UInteger` 和 `ULong` 是无符号的，所以没有符号位需要传递。  如果 `pattern` 的类型是任一种无符号类型，空出的位置将始终设置为零。  
  
 为防止移位的结果超出它所支持的位数，Visual Basic 使用与 `pattern` 的数据类型相对应的大小掩码来屏蔽 `amount` 的值。  可使用这些值的二进制与运算结果作为移位量。  大小掩码如下所示：  
  
|`pattern` 的数据类型。|大小掩码（十进制）|大小掩码（十六进制）|  
|----------------------|---------------|----------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 如果 `amount` 为零，则 `result` 的值与 `pattern` 的值相同。  如果 `amount` 为负值，则将把它作为无符号的值，并使用相应的大小掩码进行屏蔽。  
  
 数学移位绝不会产生溢出异常。  
  
## 重载  
 `>>` 运算符可以被重载，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `>>` 运算符对整数值执行算术右移位。  结果的数据类型始终与被移位的表达式相同。  
  
 [!code-vb[VbVbalrOperators#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/right-shift-operator_1.vb)]  
  
 上面的示例的结果如下：  
  
-   `result1` 为 2560 \(0000 1010 0000 0000\)。  
  
-   `result2` 为 160 \(0000 0000 1010 0000\)。  
  
-   `result3` 为 2 \(0000 0000 0000 0010\)。  
  
-   `result4` 为 640 \(0000 0010 1000 0000\)。  
  
-   `result5` 为 0（向右移了 15 位）。  
  
 `result4` 的移位量按 18 AND 15 计算，结果等于 2。  
  
 下面的示例演示对负值进行算术移位。  
  
 [!code-vb[VbVbalrOperators#55](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/right-shift-operator_2.vb)]  
  
 上面的示例的结果如下：  
  
-   `negresult1` 为 \-512 \(1111 1110 0000 0000\)。  
  
-   `negresult2` 为 \-1（传递了符号位）。  
  
## 请参阅  
 [移位运算符](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [\>\>\= 运算符](../../../visual-basic/language-reference/operators/right-shift-assignment-operator.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)