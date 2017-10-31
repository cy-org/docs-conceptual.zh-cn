---
title: "&lt;&lt; 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<<"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "&lt;&lt; 运算符 [Visual Basic]"
  - "移位运算符"
  - "运算符 &lt;&lt;, Visual Basic left shift 运算符"
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# &lt;&lt; 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对位模式执行数学左移位。  
  
## 语法  
  
```  
  
result = pattern << amount  
```  
  
## 部件  
 `result`  
 必选。  整型数值。  对该位模式进行移位的结果。  数据类型与 `pattern` 的数据类型相同。  
  
 `pattern`  
 必选。  整型数值表达式。  要进行移位的位模式。  数据类型必须为整型（`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 或 `ULong`）。  
  
 `amount`  
 必选。  数值表达式。  要将该位模式移位的位数。  数据类型必须为 `Integer` 或扩展到 `Integer`。  
  
## 备注  
 数学移位不是循环的，即不会将在结果的一端移出的数位从另一端重新移入。  在数学左移位运算中，丢弃移出结果数据类型范围的数位，而将右端空出的数位位置设置为零。  
  
 为防止移位的结果超出它所支持的位数，Visual Basic 使用与 `pattern` 的数据类型相对应的大小掩码来屏蔽 `amount` 的值。  可使用这些值的二进制与运算结果作为移位量。  大小掩码如下所示：  
  
|`pattern` 的数据类型。|大小掩码（十进制）|大小掩码（十六进制）|  
|----------------------|---------------|----------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 如果 `amount` 为零，则 `result` 的值与 `pattern` 的值相同。  如果 `amount` 为负值，则将把它作为无符号的值，并使用相应的大小掩码进行屏蔽。  
  
 数学移位绝不会产生溢出异常。  
  
> [!NOTE]
>  `<<` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码对这样的类或结构使用此运算符，请确保您了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `<<` 运算符对整数值执行数学左移位。  结果的数据类型始终与被移位的表达式相同。  
  
 [!code-vb[VbVbalrOperators#12](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/left-shift-operator_1.vb)]  
  
 上面示例的结果如下：  
  
-   `result1` 为 192 \(0000 0000 1100 0000\)。  
  
-   `result2` 为 3072 \(0000 1100 0000 0000\)。  
  
-   `result3` 为 \-32768 \(1000 0000 0000 0000\)。  
  
-   `result4` 为 384 \(0000 0001 1000 0000\)。  
  
-   `result5` 为 0（向左移动 15 位）。  
  
 `result4` 的移位量以 17 AND 15 计算，结果等于 1。  
  
## 请参阅  
 [移位运算符](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [\<\<\= 运算符](../../../visual-basic/language-reference/operators/left-shift-assignment-operator.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)