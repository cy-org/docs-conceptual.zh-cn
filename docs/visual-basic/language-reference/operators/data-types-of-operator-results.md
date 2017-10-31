---
title: "运算符结果 (Visual Basic 中) 的数据类型 |Microsoft 文档"
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
- data types [Visual Basic], operator result data types
- result data types
- operator result data types
- operators [Visual Basic], data types
- data types [Visual Basic], ranges
- operators [Visual Basic], result data types
ms.assetid: 9d524533-e1a1-4aa8-b1b8-622068173d06
caps.latest.revision: 27
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
ms.openlocfilehash: 577be6330cb76da436470c383841a717dd6e3200
ms.lasthandoff: 03/13/2017

---
# <a name="data-types-of-operator-results-visual-basic"></a>运算符结果的数据类型 (Visual Basic)
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]确定基于操作数的数据类型的操作的结果数据类型。 在某些情况下，这可能是更大的范围比两个操作数的数据类型。  
  
## <a name="data-type-ranges"></a>数据类型范围  
 范围相关的数据类型，从最小到最大值的顺序如下所示︰  
  
-   [布尔](../../../visual-basic/language-reference/data-types/boolean-data-type.md)— 两个可能值  
  
-   [SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)，[字节](../../../visual-basic/language-reference/data-types/byte-data-type.md)-256 个可能的整数值  
  
-   [短](../../../visual-basic/language-reference/data-types/short-data-type.md)， [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md) — 65536 (6.5 … E + 4) 不可或缺的可能值  
  
-   [整数](../../../visual-basic/language-reference/data-types/integer-data-type.md)， [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md) -4294967296 (4.2 … E + 9) 不可或缺的可能值  
  
-   [长](../../../visual-basic/language-reference/data-types/long-data-type.md)， [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md) -18446744073709551615 (1.8 … E + 19) 不可或缺的可能值  
  
-   [十进制](../../../visual-basic/language-reference/data-types/decimal-data-type.md)-1.5 … E + 29 可能整数值，最大的范围是 7.9 … E + 28 （绝对值）  
  
-   [单个](../../../visual-basic/language-reference/data-types/single-data-type.md)—...最大范围 3.4 E + 38 （绝对值）  
  
-   [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) —...最大范围 1.7 E + 308 （绝对值）  
  
 有关详细信息[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]数据类型，请参阅[数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
 如果操作数的计算结果为[Nothing](../../../visual-basic/language-reference/nothing.md)、[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]算术运算符将其视为零。  
  
## <a name="decimal-arithmetic"></a>十进制算术运算  
 请注意，[十进制](../../../visual-basic/language-reference/data-types/decimal-data-type.md)数据类型既不是浮点和整型。  
  
 如果其中一个操作数的`+`， `–`， `*`， `/`，或`Mod`操作`Decimal`和另一个则不`Single`或`Double`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]扩大到另一个操作数`Decimal`。 它将执行中的操作`Decimal`，并且结果数据类型为`Decimal`。  
  
## <a name="floating-point-arithmetic"></a>浮点运算  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]执行中的大多数浮点算术[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)，这是最有效的数据类型执行之类的操作。 但是，如果一个操作数为[单个](../../../visual-basic/language-reference/data-types/single-data-type.md)和另一个则不`Double`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]执行中的操作`Single`。 它将根据需要适当的数据类型在执行操作前向每个操作数的扩展，则结果也为该数据类型。  
  
### <a name="-and--operators"></a>/ 和 ^ 运算符  
 `/`仅为定义运算符[十进制](../../../visual-basic/language-reference/data-types/decimal-data-type.md)，[单个](../../../visual-basic/language-reference/data-types/single-data-type.md)，和[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)数据类型。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将根据需要向适当的数据类型的每个操作数扩展之前此操作，以及结果也为该数据类型。  
  
 下表显示结果数据类型为`/`运算符。 请注意，此表是对称;操作数数据类型的给定组合，结果数据类型是无论操作数的顺序相同。  
  
||||||  
|---|---|---|---|---|  
||`Decimal`|`Single`|`Double`|任何整数类型|  
|`Decimal`|Decimal|Single|Double|Decimal|  
|`Single`|单倍行距|Single|Double|单倍行距|  
|`Double`|Double|Double|Double|Double|  
|任何整数类型|Decimal|Single|Double|Double|  
  
 `^`仅为定义运算符`Double`数据类型。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将根据需要向每个操作数扩展`Double`之前此操作，以及结果数据类型始终是`Double`。  
  
## <a name="integer-arithmetic"></a>整数算术运算  
 整数运算的结果数据类型取决于操作数的数据类型。 一般情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使用以下策略确定的结果数据类型︰  
  
-   如果二元运算符的两个操作数具有相同的数据类型，则结果也为该数据类型。 一个例外是`Boolean`，这将其强制转换为`Short`。  
  
-   如果无符号的操作数与签名操作数加入，该结果的有符号的类型至少尽可能大范围与具有其中一个操作数。  
  
-   否则，结果通常具有较大的两个操作数数据类型。  
  
 请注意结果数据类型不可能任一操作数数据类型。  
  
> [!NOTE]
>  结果数据类型不是始终足以容纳所有可能的值的运算所生成的。 <xref:System.OverflowException>如果值太大的结果数据类型，可能会发生异常。</xref:System.OverflowException>  
  
### <a name="unary--and--operators"></a>一元 + 和-运算符  
 下表显示结果数据类型的两个一元运算符`+`和`–`。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|一元`+`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|一元`–`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
  
### <a name="-and--operators"></a><\<和 >> 运算符  
 下表显示结果数据类型的两个移位运算符，`<<`和`>>`。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将每个移位运算符视为其左操作数 （要移动的位模式） 的一元运算符。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`<<`, `>>`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 如果左的操作数是`Decimal`， `Single`， `Double`，或`String`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将其转换为`Long`之前此操作，并且结果数据类型为`Long`。 右操作数 （要位移的位位置数） 必须`Integer`或类型加宽到`Integer`。  
  
### <a name="binary----and-mod-operators"></a>二进制 +、-、 *，和 Mod 运算符  
 下表显示结果数据类型为二进制文件`+`和`–`运算符和`*`和`Mod`运算符。 请注意，此表是对称;操作数数据类型的给定组合，结果数据类型是无论操作数的顺序相同。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|简短|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`Byte`|简短|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|简短|Short|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Decimal|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Decimal|  
|`ULong`|Decimal|Decimal|ULong|Decimal|ULong|Decimal|ULong|Decimal|ULong|  
  
### <a name="-operator"></a>\ 运算符  
 下表显示结果数据类型为`\`运算符。 请注意，此表是对称;操作数数据类型的给定组合，结果数据类型是无论操作数的顺序相同。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|简短|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|简短|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|简短|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 如果其中一个操作数的`\`运算符是[十进制](../../../visual-basic/language-reference/data-types/decimal-data-type.md)，[单个](../../../visual-basic/language-reference/data-types/single-data-type.md)，或[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将其转换为[长](../../../visual-basic/language-reference/data-types/long-data-type.md)之前此操作，并且结果数据类型为`Long`。  
  
## <a name="relational-and-bitwise-comparisons"></a>关系和按位比较  
 关系的操作的结果数据类型 (`=`， `<>`， `<`， `>`， `<=`， `>=`) 始终是`Boolean`[布尔数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)。 同样适用于逻辑运算 (`And`， `AndAlso`， `Not`， `Or`， `OrElse`， `Xor`) 上`Boolean`操作数。  
  
 按位逻辑运算的结果数据类型取决于操作数的数据类型。 请注意，`AndAlso`和`OrElse`仅为定义`Boolean`，和[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将根据需要向每个操作数转换`Boolean`之前执行该操作。  
  
### <a name="-----and--operators"></a>=, <>, \<, >, \<=, and >= Operators  
 如果这两个操作数都是`Boolean`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]认为`True`要小于`False`。 如果数值类型进行比较与`String`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将转换`String`到`Double`操作之前。 一个`Char`或`Date`操作数可以只与相同的数据类型的另一个操作数进行比较。 结果数据类型始终是`Boolean`。  
  
### <a name="bitwise-not-operator"></a>位 Not 运算符  
 下表显示结果数据类型的按位`Not`运算符。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Not`|Boolean|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 如果操作数为`Decimal`， `Single`， `Double`，或`String`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将其转换为`Long`之前此操作，并且结果数据类型为`Long`。  
  
### <a name="bitwise-and-or-and-xor-operators"></a>按位，或者，和 Xor 运算符  
 下表显示结果数据类型的按位`And`， `Or`，和`Xor`运算符。 请注意，此表是对称;操作数数据类型的给定组合，结果数据类型是无论操作数的顺序相同。  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Boolean|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|简短|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|简短|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 如果一个操作数为`Decimal`， `Single`， `Double`，或`String`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将其转换为`Long`前该操作和结果数据类型是否相同如果已经过该操作数的`Long`。  
  
## <a name="miscellaneous-operators"></a>其他运算符  
 `&`仅定义的串联运算符`String`操作数。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将根据需要向每个操作数转换`String`之前此操作，以及结果数据类型始终是`String`。 为了进行`&`运算符、 所有转换到`String`视为会扩大，即使`Option Strict`是`On`。  
  
 `Is`和`IsNot`运算符要求两个操作数均为引用类型。 The `TypeOf`...`Is`表达式要求第一个操作数是引用类型，第二个操作数是一种数据类型的名称。 在所有这些情况下结果数据类型是`Boolean`。  
  
 `Like`仅针对的模式匹配定义运算符`String`操作数。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]尝试将根据需要向每个操作数转换`String`操作之前。 结果数据类型始终是`Boolean`。  
  
## <a name="see-also"></a>请参见  
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [在 Visual Basic 中的算术运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [在 Visual Basic 中的比较运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [运算符](../../../visual-basic/language-reference/operators/index.md)   
 [在 Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)
