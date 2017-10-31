---
title: "+ 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.+"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "+ 运算符"
  - "算术运算符, 加法"
  - "串联运算符, 语法"
  - "字符串 [Visual Basic], 串联"
  - "求和运算符"
ms.assetid: 5694778f-0a2c-4539-8009-f66f318fb46d
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# + 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个数字相加，或返回数值表达式的正值。  还可用于连接两个字符串表达式。  
  
## 语法  
  
```  
  
      expression1 + expression2  
- or -  
+ expression1  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`expression1`|必选。  任何数值或字符串表达式。|  
|`expression2`|必选（除非 `+` 运算符正在计算负值）。  任何数值或字符串表达式。|  
  
## 结果  
 如果 `expression1` 和 `expression2` 均为数值，结果将为它们的算术和。  
  
 如果缺少 `expression2`，`+` 运算符为表达式的不变值的“一元”恒等运算符。  在此情况下，该运算将保留 `expression1` 的符号，因此当 `expression1` 为负值时，结果也为负值。  
  
 如果 `expression1` 和 `expression2` 均为字符串，将把它们的值连接起来作为结果。  
  
 如果 `expression1` 和 `expression2` 的类型不同，执行的操作将取决于它们的类型、内容及 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md) 的设置。  有关更多信息，请参见“备注”中的表。  
  
## 支持的类型  
 所有数值类型，包括无符号和浮点类型以及 `Decimal`、`String` 类型。  
  
## 备注  
 通常，`+` 运算符尽可能执行算术加法运算，只有当两个表达式均为字符串时，才执行连接操作。  
  
 如果两个表达式都不是 `Object`，Visual Basic 将执行以下操作。  
  
|||  
|-|-|  
|表达式的数据类型|编译器操作|  
|两个表达式均为数值数据类型（`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single` 或 `Double`）|相加。  结果数据类型是适用于 `expression1` 和 `expression2` 的数据类型的数值类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的“整数算法”表。|  
|两个表达式均为 `String` 类型|连接。|  
|一个表达式为数值数据类型而另一个表达式是字符串|如果 `Option Strict` 为 `On`，则产生编译器错误。<br /><br /> 如果 `Option Strict` 为 `Off`，则将 `String` 隐式转换为 `Double` 并执行加法运算。<br /><br /> 如果 `String` 不能转换为 `Double`，将引发 <xref:System.InvalidCastException> 异常。|  
|一个表达式为数值数据类型而另一个表达式为 [Nothing](../../../visual-basic/language-reference/nothing.md)|相加，此时 `Nothing` 的值为零。|  
|一个表达式为字符串而另一个表达式为 `Nothing`|连接，此时 `Nothing` \= ""。|  
  
 如果一个表达式为 `Object` 表达式，Visual Basic 将执行下列操作。  
  
|||  
|-|-|  
|表达式的数据类型|编译器操作|  
|`Object` 表达式保存数值而另一个表达式为数值数据类型|如果 `Option Strict` 为 `On`，则产生编译器错误。<br /><br /> 如果 `Option Strict` 为 `Off`，则执行加法运算。|  
|`Object` 表达式保存数值而另一个表达式的类型为 `String`|如果 `Option Strict` 为 `On`，则产生编译器错误。<br /><br /> 如果 `Option Strict` 为 `Off`，则将 `String` 隐式转换为 `Double` 并执行加法运算。<br /><br /> 如果 `String` 不能转换为 `Double`，将引发 <xref:System.InvalidCastException> 异常。|  
|`Object` 表达式保存字符串而另一个表达式为数值数据类型|如果 `Option Strict` 为 `On`，则产生编译器错误。<br /><br /> 如果 `Option Strict` 为 `Off`，则将字符串 `Object` 隐式转换为 `Double` 并执行加法运算。<br /><br /> 如果字符串 `Object` 不能转换为 `Double`，将引发 <xref:System.InvalidCastException> 异常。|  
|`Object` 表达式保存字符串而另一个表达式的类型为 `String`|如果 `Option Strict` 为 `On`，则产生编译器错误。<br /><br /> 如果 `Option Strict` 为 `Off`，则将 `Object` 隐式转换为 `String` 并执行连接操作。|  
  
 如果两个表达式均为 `Object` 表达式，Visual Basic 将执行下列操作（仅限于 `Option Strict Off` 情况下）。  
  
|||  
|-|-|  
|表达式的数据类型|编译器操作|  
|两个 `Object` 表达式均保存数值|相加。|  
|两个 `Object` 表达式均为 `String` 类型|连接。|  
|一个 `Object` 表达式保存数值而另一个表达式保存字符串|将字符串 `Object` 隐式转换为 `Double` 并执行加法运算。<br /><br /> 如果字符串 `Object` 不能转换为数值，将引发 <xref:System.InvalidCastException> 异常。|  
  
 如果其中一个 `Object` 表达式计算值为 [Nothing](../../../visual-basic/language-reference/nothing.md) 或 <xref:System.DBNull>，则 `+` 运算符将其视为 `String`，其值为 ""。  
  
> [!NOTE]
>  使用 `+` 运算符时，可能无法确定应该执行加法运算还是执行字符串连接运算。  所以应使用 `&` 运算符执行连接操作，以消除多义性并提供自我说明代码。  
  
## 重载  
 `+` 运算符可以被“重载”，这意味着当操作数的类型为类或结构时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `+` 运算符将数字相加。  如果操作数均为数值，Visual Basic 将计算算术结果。  算术结果为两个操作数的和。  
  
 [!code-vb[VbVbalrOperators#6](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_1.vb)]  
  
 还可以使用 `+` 运算符连接字符串。  如果操作数均为字符串，Visual Basic 将把它们连接起来。  连接结果为一个字符串，它由两个操作数的内容依次排列而成。  
  
 如果操作数的类型不同，则结果将取决于 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md) 的设置。  下面的示例演示当 `Option Strict` 为 `On` 时的结果。  
  
 [!code-vb[VbVbalrOperators#53](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_2.vb)]  
  
 [!code-vb[VbVbalrOperators#50](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_3.vb)]  
[!code-vb[VbVbalrOperators#51](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_4.vb)]  
  
 下面的示例演示当 `Option Strict` 为 `Off` 时的结果。  
  
 [!code-vb[VbVbalrOperators#54](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_5.vb)]  
  
 [!code-vb[VbVbalrOperators#50](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_3.vb)]  
[!code-vb[VbVbalrOperators#52](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_6.vb)]  
  
 若要消除多义性，应用 `&` 运算符代替 `+` 运算符执行连接操作。  
  
## 请参阅  
 [& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md)   
 [串联运算符](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)