---
title: "数据类型疑难解答 (Visual Basic) |Microsoft 文档"
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
- Char data type, converting
- Decimal data type, conversions
- data types [Visual Basic], troubleshooting
- literals, default types
- type characters, literal
- Mod operator [Visual Basic], in floating-point operations
- troubleshooting Visual Basic, data types
- troubleshooting data types
- floating-point numbers, precision
- Boolean data type, converting
- literal types
- literal type characters
- floating-point numbers, imprecision
- String data type, converting
- floating-point numbers, comparison
- floating-point numbers
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
caps.latest.revision: 29
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
ms.openlocfilehash: cfb8fc77d3e0d85ef795a94fc95ab61a8f68ff39
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-data-types-visual-basic"></a>数据类型疑难解答 (Visual Basic)
此页列出了对内部数据类型执行操作时可能会出现一些常见问题。  
  
## <a name="floating-point-expressions-do-not-compare-as-equal"></a>浮点表达式不相等比较  
 当您处理使用浮点数 ([单一数据类型](../../../../visual-basic/language-reference/data-types/single-data-type.md)和[Double 数据类型](../../../../visual-basic/language-reference/data-types/double-data-type.md))，请记住它们存储为二进制分数的形式。 这意味着它们不能存储不是二进制分数任何数量的准确表示形式 (窗体 k / (2 ^ n) 其中 k 和 n 为整数)。 例如，0.5 （= 1/2） 和 0.3125 （= 5/16） 可以保存为精确值，而 （= 1/5） 的 0.2 和 0.3 （= 3/10） 只能是近似值。  
  
 由于这不精确，您不能依赖精确的结果在浮点值上运行时。 特别是，理论上相等的两个值可能必须稍有不同的表示形式。  
  
| 若要将浮点数进行比较 | 
|---| 
|1.使用计算它们的差的绝对值<xref:System.Math.Abs%2A>方法<xref:System.Math>类<xref:System>命名空间。</xref:System> </xref:System.Math> </xref:System.Math.Abs%2A><br />2.确定可接受的最大差值，以便您可以考虑进行相等实用的角度而言如果它们的差不大于这两个数量。<br />3.将为可接受的差值差的绝对值的数值进行比较。|  
  
 下面的示例演示两个错误用法和正确比较`Double`值。  
  
 [!code-vb[VbVbalrDataTypes #&10;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_1.vb)]  
  
 前面的示例使用<xref:System.Double.ToString%2A>方法<xref:System.Double>结构，以便它可以指定精度优于`CStr`关键字使用。</xref:System.Double> </xref:System.Double.ToString%2A> 默认值为 15 位数字，但是"G17"格式将其扩展为 17 个数位。  
  
## <a name="mod-operator-does-not-return-accurate-result"></a>Mod 运算符不返回准确的结果  
 由于不精确的浮点存储[Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md)可以在至少其中一个操作数为浮点数时返回了意外的结果。  
  
 [Decimal 数据类型](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)不使用浮点表示形式。 在不精确的许多数字`Single`和`Double`中精确`Decimal`（例如 0.2 和 0.3）。 尽管算术中要慢`Decimal`比在浮点数，但可能值得性能的下降来实现更好的精度。  
  
|若要查找的浮点数的整数余数|  
|---|  
|1.将变量声明为`Decimal`。<br />2.使用文本类型字符`D`强制转换为`Decimal`，以防它们的值太大，`Long`数据类型。|  
  
 下面的示例演示了潜在的浮点操作数不精确性。  
  
 [!code-vb[VbVbalrDataTypes #&11;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_2.vb)]  
  
 前面的示例使用<xref:System.Double.ToString%2A>方法<xref:System.Double>结构，以便它可以指定精度优于`CStr`关键字使用。</xref:System.Double> </xref:System.Double.ToString%2A> 默认值为 15 位数字，但是"G17"格式将其扩展为 17 个数位。  
  
 因为`zeroPointTwo`是`Double`，它表示的 0.2 已存储的值是为 0.20000000000000001 的无限重复二进制小数。 此数量的值除以 2.0 将得到 9.9999999999999995，余数为 0.19999999999999991。  
  
 中的表达式`decimalRemainder`，文本类型字符`D`强制的两个操作数`Decimal`，，0.2 具有精确的表示形式。 因此`Mod`运算符产生预期的余数 0.0。  
  
 请注意，不不足，无法声明`decimalRemainder`作为`Decimal`。 您还必须强制文字到`Decimal`，或者它们使用`Double`默认情况下和`decimalRemainder`接收相同的不准确值`doubleRemainder`。  
  
## <a name="boolean-type-does-not-convert-to-numeric-type-accurately"></a>布尔值类型不会准确地转换为数值类型  
 [Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)值不会存储为数字，并且存储的值不应为等效于数字。 为了与早期版本中，兼容[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供转换关键字 ([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)， `CBool`，`CInt`等) 之间进行转换`Boolean`与数值类型。 但是，其他语言有时执行这些转换方式不同，请执行[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]方法。  
  
 绝不应编写代码，它依赖于等效数值`True`和`False`。 只要有可能，应限制使用`Boolean`变量来为其设计的逻辑值。 如果您需要混合`Boolean`和数字值，请确保您了解您选择的转换方法。  
  
### <a name="conversion-in-visual-basic"></a>在 Visual Basic 中的转换  
 当您使用`CType`或`CBool`转换关键字，若要将数值数据类型转换`Boolean`，0 会变为`False`和所有其他值会变为`True`。 转换时`Boolean`为数值类型时使用了转换的关键字值`False`变为 0 和`True`会变为-1。  
  
### <a name="conversion-in-the-framework"></a>框架中的转换  
 <xref:System.Convert.ToInt32%2A>方法<xref:System.Convert>类<xref:System>命名空间将转换`True`为 +&1;。</xref:System> </xref:System.Convert> </xref:System.Convert.ToInt32%2A>  
  
 如果必须将`Boolean`值为数值数据类型时，请小心使用转换方法。  
  
## <a name="character-literal-generates-compiler-error"></a>字符文本将生成编译器错误  
 在任何类型的字符，缺乏[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将采用默认的文本的数据类型。 默认类型为字符文本，用引号引起来 (`" "`) — 是`String`。  
  
 `String`数据类型不会扩大到[Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)。 这意味着，如果你想要分配到一个文本`Char`变量时，必须进行收缩转换，或将文本强制转换到`Char`类型。  

|若要创建字符文本以将分配给变量或常量|
|---|  
|1.声明的变量或常量作为`Char`。<br />2.将字符值括在双引号 (`" "`)。<br />3.请按照右双引号以文本类型字符`C`若要将文本强制转换到`Char`。 如果类型检查开关，则必须 ([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 是`On`，而且希望在任何情况下。|  
  
 下面的示例演示了将文本赋予的失败和成功分配`Char`变量。  
  
 [!code-vb[VbVbalrDataTypes #&12;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_3.vb)]  
  
 始终存在风险中没有使用收缩转换，因为它们可以在运行时失败。 例如，从转换`String`到`Char`如果可能会失败`String`值包含多个字符。 因此，在编程时最好使用`C`键入字符。  
  
## <a name="string-conversion-fails-at-run-time"></a>字符串转换在运行时失败  
 [字符串数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md)参与了很少的扩大转换。 `String`扩大到自身和`Object`，和仅`Char`和`Char()`(`Char`数组) 扩大到`String`。 这是因为`String`变量和常量可以包含其他数据类型不能包含的值。  
  
 类型检查开关 ([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 是`On`，编译器不允许所有隐式收缩转换。 这包括涉及`String`。 您的代码仍可以使用转换关键字如`CStr`和[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)，以指示[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]尝试进行转换。  
  
> [!NOTE]
>  收缩转换错误则会取消对转换中的元素从`For Each…Next`循环控制变量的集合。 有关详细信息和示例，请参阅中的"收缩转换"一节[为每个...下一条语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
### <a name="narrowing-conversion-protection"></a>收缩转换保护  
 收缩转换的缺点是它们可能会在运行时失败。 例如，如果`String`变量包含的任何内容而不是"True"或"False，"它不能转换为`Boolean`。 如果它包含标点字符，为任何数值类型的转换将失败。 除非您知道您`String`变量始终保存目标类型可以接受的值，否则不应尝试进行转换。  
  
 如果必须从转换`String`最安全的过程是将在尝试的转换为另一个数据类型，[重试...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。 这样就可以处理运行时故障。  
  
### <a name="character-arrays"></a>字符数组  
 单个`Char`和数组`Char`元素均扩大到`String`。 但是，`String`不会扩大到`Char()`。 若要将转换`String`值赋给`Char`数组中，您可以使用<xref:System.String.ToCharArray%2A>方法的<xref:System.String?displayProperty=fullName>类。</xref:System.String?displayProperty=fullName> </xref:System.String.ToCharArray%2A>  
  
### <a name="meaningless-values"></a>无意义的值  
 一般情况下，`String`值并不在其他数据类型，有意义且转换是人工，危险极低。 只要有可能，应限制使用`String`变量来为其设计的字符序列。 绝不应编写依赖于其他类型中的等效值的代码。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
