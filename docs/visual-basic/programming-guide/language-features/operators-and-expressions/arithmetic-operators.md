---
title: "在 Visual Basic 中的算术运算符 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- type safety
- operators [Visual Basic], bitwise
- operators [Visual Basic], bit-shift
- bitwise operators
- bit-shift operators
- zero, division by zero
- operators [Visual Basic], arithmetic
- division, by zero
- Visual Basic code, operators
- arithmetic operators, about arithmetic operators
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c724bf8b6794e71d49b32c7d3ce9e010f541f68f
ms.lasthandoff: 03/13/2017

---
# <a name="arithmetic-operators-in-visual-basic"></a>算术运算符 (Visual Basic)
算术运算符用于执行很多熟悉的算术运算，涉及通过文字、 变量、 其他表达式、 函数和属性调用和常量表示的数值计算。 算术运算符也属于是移位运算符，该级别的单个位进行运算的操作数执行操作和向左或向右移动其位模式。  
  
## <a name="arithmetic-operations"></a>算术运算  
 您可以添加两个值一起使用的表达式中[+ 运算符](../../../../visual-basic/language-reference/operators/addition-operator.md)，或从另一个具有中减去&1; [-运算符 (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md)，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators #&57;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_1.vb)]  
  
 求反也使用[-运算符 (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md)，但只带一个操作数，如下面的示例演示了。  
  
 [!code-vb[VbVbalrOperators #&58; 页](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_2.vb)]  
  
 乘法和除法使用[* 运算符](../../../../visual-basic/language-reference/operators/multiplication-operator.md)和[/ 运算符 (Visual Basic)](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md)分别，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators #&59;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_3.vb)]  
  
 求幂使用[^ 运算符](../../../../visual-basic/language-reference/operators/exponentiation-operator.md)，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators #&60;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_4.vb)]  
  
 整数除法利用执行[\ 运算符 (Visual Basic)](../../../../visual-basic/language-reference/operators/integer-division-operator.md)。 整数除法返回商，即表示的次数的整数除数可以除被除数而无需考虑了所有余数。 除数和被除数必须是整数类型 (`SByte`， `Byte`， `Short`， `UShort`， `Integer`， `UInteger`， `Long`，和`ULong`) 为此运算符。 必须首先将所有其他类型转换为整数类型。 下面的示例演示整数除法。  
  
 [!code-vb[VbVbalrOperators #&61;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_5.vb)]  
  
 使用执行求模算术[Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md)。 此运算符返回其余部分被除数除以除数后的次数的整数。 如果除数和被除数可以是整数类型，则返回的值是整数。 如果除数和除数都是浮点类型，则返回的值也是浮点。 下面的示例演示此行为。  
  
 [!code-vb[VbVbalrOperators #&62;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_6.vb)]  
  
 [!code-vb[VbVbalrOperators #&63;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_7.vb)]  
  
### <a name="attempted-division-by-zero"></a>尝试被零除  
 被零除具有不同的结果，具体取决于涉及的数据类型。 In integral divisions (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`), the [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] throws a <xref:System.DivideByZeroException> exception.</xref:System.DivideByZeroException> 在除法运算`Decimal`或`Single`数据类型，[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]还会抛出<xref:System.DivideByZeroException>异常。</xref:System.DivideByZeroException>  
  
 在涉及浮点部门`Double`数据类型，不会引发异常，并且结果是表示的类成员<xref:System.Double.NaN>， <xref:System.Double.PositiveInfinity>，或<xref:System.Double.NegativeInfinity>，取决于被除数。</xref:System.Double.NegativeInfinity> </xref:System.Double.PositiveInfinity> </xref:System.Double.NaN> 下表汇总了各个结果的尝试除`Double`被零除的值。  
  
|被除数的数据类型|除数数据类型|被除数的值|结果|  
|---|---|---|---|  
|`Double`|`Double`|0|<xref:System.Double.NaN>（不是数学上定义的数字）</xref:System.Double.NaN>|  
|`Double`|`Double`|> 0|<xref:System.Double.PositiveInfinity></xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity></xref:System.Double.NegativeInfinity>|  
  
 当捕获的<xref:System.DivideByZeroException>异常，您可以使用其成员可以帮助您处理它。</xref:System.DivideByZeroException> 例如，<xref:System.Exception.Message%2A>属性保留了该异常的消息文本。</xref:System.Exception.Message%2A> 有关详细信息，请参阅[重试...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## <a name="bit-shift-operations"></a>移位运算  
 移位运算对位模式执行算术移位运算。 模式包含在左侧，操作数中，而右侧操作数指定的位数移动模式。 将模式切换到右[>> 运算符](../../../../visual-basic/language-reference/operators/right-shift-operator.md)滑动到左侧则与[ <> </> ](../../../../visual-basic/language-reference/operators/left-shift-operator.md)。  
  
 模式操作数的数据类型必须是`SByte`， `Byte`， `Short`， `UShort`， `Integer`， `UInteger`， `Long`，或`ULong`。 Shift 量操作数的数据类型必须是`Integer`或者必须扩大到`Integer`。  
  
 算术移位不是循环性的这意味着从结果的一端移掉的位在另一端不重新移入。 因移位而空出的位上将设置，如下所示︰  
  
-   0 表示算术左移位运算  
  
-   0 的正数值的算术右移位  
  
-   算术右移位运算的无符号的数据类型为&0; (`Byte`， `UShort`， `UInteger`， `ULong`)  
  
-   1 表示负数的算术右移位 (`SByte`， `Short`， `Integer`，或`Long`)  
  
 以下示例将推`Integer`左侧和右侧的值。  
  
 [!code-vb[VbVbalrOperators #&64;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_8.vb)]  
  
 算术移位永远不会产生溢出异常。  
  
## <a name="bitwise-operations"></a>按位运算  
 逻辑运算符，除了`Not`， `Or`， `And`，和`Xor`还执行按位算术运算在数值中使用时。 有关详细信息，请参阅 》 的"按位操作"[逻辑和按位运算符在 Visual Basic 中](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)。  
  
## <a name="type-safety"></a>类型安全  
 操作数通常应属于同一类型。 例如，如果你正在添加`Integer`变量时，您应将其添加到另一个`Integer`变量，并且您应将结果赋给一个类型的变量`Integer`以及。  
  
 一种方法以确保良好的类型安全编码做法是使用[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)。 如果您设置`Option Strict On`，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]自动执行*类型安全*转换。 例如，如果你尝试添加`Integer`变量`Double`变量并将值赋给`Double`变量时，该操作将正常进行，因为`Integer`值可以转换为`Double`而不丢失数据。 类型不安全的转换，另一方面，导致编译器错误与`Option Strict On`。 例如，如果你尝试添加`Integer`变量`Double`变量并将值赋给`Integer`变量时，会导致编译器错误，因为`Double`变量不能隐式转换为键入`Integer`。  
  
 如果您设置`Option Strict Off`，但[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]允许隐式收缩转换完成，但是它们可能会导致意外丢失的数据或精度。 出于此原因，我们建议你使用`Option Strict On`编写生产代码时。 有关详细信息，请参阅[扩大和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [算术运算符](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [移位运算符](../../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [在 Visual Basic 中的比较运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [在 Visual Basic 中的串联运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [在 Visual Basic 中的逻辑和按位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
