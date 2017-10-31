---
title: "数值数据类型 (Visual Basic 中) |Microsoft 文档"
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
- integral types, Visual Basic
- Short data type, numeric data types
- Double data type, numeric data types
- Long data type, Visual Basic numeric data types
- numbers, whole
- fractions
- numbers
- whole numbers
- integer numbers
- numbers, integer
- fractional data types
- mantissas, of fractional numbers
- mantissas
- data types [Visual Basic], numeric
- Integer data type, numeric data types
- exponent, of fractional numbers
- integers
- numeric data types, Visual Basic
- Single data type, numeric types
- Decimal data type, numeric data types
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
caps.latest.revision: 25
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
ms.openlocfilehash: 3c3098370b8d9dcb6aafcb06dcfb8f4e144b899a
ms.lasthandoff: 03/13/2017

---
# <a name="numeric-data-types-visual-basic"></a>数值型数据类型 (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供几个*数值数据类型*来处理各种表示形式之间的数字。 *整型*类型只表示整数 （正数、 负数和零），和*nonintegral*类型带有整数和小数部分表示的数字。  
  
 显示通过并行进行比较的表为[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]数据类型，请参阅[数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## <a name="integral-numeric-types"></a>整型数值类型  
 *整数数据类型*是指那些表示没有小数部分的唯一数字。  
  
 *签名*整数数据类型是[SByte 数据类型](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)（8 位）、 [Short 数据类型](../../../../visual-basic/language-reference/data-types/short-data-type.md)（16 位）、[整数数据类型](../../../../visual-basic/language-reference/data-types/integer-data-type.md)（32-位） 和[Long 数据类型](../../../../visual-basic/language-reference/data-types/long-data-type.md)（64 位）。 如果某个变量总是存储整数而不是小数数字，将其声明为这些类型之一。  
  
 *无符号*整型[Byte 数据类型](../../../../visual-basic/language-reference/data-types/byte-data-type.md)（8 位）、 [UShort 数据类型](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)（16 位）、 [UInteger 数据类型](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)（32-位） 和[ULong 数据类型](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)（64 位）。 如果某个变量包含二进制数据或未知种类的数据，将其声明为这些类型之一。  
  
### <a name="performance"></a>性能  
 算术运算是更快速度和整数类型，而不与其他数据类型。 它们是使用最快`Integer`和`UInteger`中的类型[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
### <a name="large-integers"></a>大整数  
 如果您需要存储的整数大于`Integer`可以容纳的数据类型，则可以使用`Long`改为数据类型。 `Long`变量可以存储从-9223372036854775808 到 9223372036854775807 的数字。 使用操作`Long`速度稍慢于具有`Integer`。  
  
 如果您需要更大的值，则可以使用[Decimal 数据类型](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)。 您可以存储从-79228162514264337593543950335 到 79228162514264337593543950335 的数字`Decimal`如果不使用任何小数位数的变量。 但是，操作与`Decimal`数字是远远慢于速度与任何其他数值数据类型。  
  
### <a name="small-integers"></a>小整数  
 如果您不需要的全部`Integer`数据类型，则可以使用`Short`数据类型，它包含从-32768 到 32767 的整数。 对于最小的整数范围，`SByte`数据类型都包含从-128 到 127 的整数。 如果您有大量的变量包含小整数，公共语言运行时可以有时将存储您`Short`和`SByte`变量更高效地，以节省内存消耗。 但是，操作与`Short`和`SByte`会稍微慢一些比与`Integer`。  
  
### <a name="unsigned-integers"></a>无符号的整数  
 如果您知道您的变量永远不需要保存为负数，则可以使用*无符号类型*`Byte`， `UShort`， `UInteger`，和`ULong`。 上述每种数据类型可以容纳一个正整数值大小的两倍作为其相应的有符号类型 (`SByte`， `Short`， `Integer`，和`Long`)。 就性能来说，每个无符号的类型是效率及其对应的有符号类型一样。 具体而言，`UInteger`与共享`Integer`都被认为最有效的所有基本数值数据类型。  
  
## <a name="nonintegral-numeric-types"></a>非整型数值类型  
 *非整数数据类型*是指那些表示带有整数和小数部分的数字。  
  
 非整型数值数据类型为`Decimal`（128 位定点）[单一数据类型](../../../../visual-basic/language-reference/data-types/single-data-type.md)（32 位浮点） 和[Double 数据类型](../../../../visual-basic/language-reference/data-types/double-data-type.md)（64 位浮点数）。 它们是已全部签名的类型。 如果一个变量可以包含一小部分，将其声明为这些类型之一。  
  
 `Decimal`不是浮点数据类型。 `Decimal`数字具有二进制整数值和一个指定的值的哪一部分是小数部分的整数比例因子。  
  
 您可以使用`Decimal`货币值的变量。 优点是值的精度。 `Double`数据类型是速度更快，并且需要更少的内存，但它可能会发生舍入误差。 `Decimal`数据类型可保持完整精度为 28 位小数。  
  
 浮点 (`Single`和`Double`) 数字具有更大范围比`Decimal`数字，但可能会导致舍入误差。 浮点类型都支持有效位比`Decimal`，但可以表示更大的值。  
  
 非整型数值可以用来表示为 mmmEeee，mmm 即*尾数*（有效位） 和 eee 是*指数*（10 的幂）。 非整型的最高的正值将为 7.9228162514264337593543950335 e + 28 `Decimal`，3.4028235 e + 38 个`Single`，1.79769313486231570 e + 308 `Double`。  
  
### <a name="performance"></a>性能  
 `Double`因为当前平台上的处理器执行以双精度浮点运算，则是最有效的小数数据类型。 但是，操作与`Double`与整数类型，如速度快`Integer`。  
  
### <a name="small-magnitudes"></a>小量值  
 对于具有最小可能的数值 （接近 0），数字`Double`变量可以存储数字越小越-4.94065645841246544 e-324 的负值，4.94065645841246544 e-324 的正值。  
  
### <a name="small-fractional-numbers"></a>小小数位的数字  
 如果您不需要的全部`Double`数据类型，则可以使用`Single`数据类型，它可以存储从-3.4028235 e + 38 到 3.4028235 e + 38 之间的浮点数。 最小最小量值为`Single`变量为-1.401298 e-45 对于负值，范围为 1.401298 e-45, 正值 45。 如果您有大量的变量包含小浮点数，公共语言运行时可以有时将存储您`Single`变量更高效地，以节省内存消耗。  
  
## <a name="see-also"></a>另请参阅  
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [字符数据类型](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [其他数据类型](../../../../visual-basic/programming-guide/language-features/data-types/miscellaneous-data-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
