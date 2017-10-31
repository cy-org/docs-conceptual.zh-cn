---
title: "类型转换函数 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.CUShort"
  - "vb.csng"
  - "vb.CDate"
  - "CByte"
  - "CSng"
  - "vb.CDec"
  - "CBool"
  - "CStr"
  - "vb.CULng"
  - "CDec"
  - "CVErr"
  - "CDbl"
  - "CShort"
  - "vb.CObj"
  - "vb.CVErr"
  - "CULng"
  - "vb.cdbl"
  - "vb.cbool"
  - "CObj"
  - "CDate"
  - "CLng"
  - "vb.cstr"
  - "vb.cbyte"
  - "vb.clng"
  - "vb.CChar"
  - "CUShort"
  - "vb.CUInt"
  - "vb.cint"
  - "vb.CShort"
  - "CInt"
  - "CUInt"
  - "CChar"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "四舍六入五成双"
  - "Boolean 数据类型, 转换"
  - "Byte 数据类型, 转换"
  - "CBool 函数"
  - "CByte 函数"
  - "CChar 函数"
  - "CDate 函数"
  - "CDbl 函数"
  - "CDec 函数"
  - "Char 数据类型, 转换"
  - "CInt 函数"
  - "CLng 函数"
  - "转换, 类型转换函数"
  - "CSByte 函数"
  - "CSng 函数"
  - "CStr 函数"
  - "CUInt 函数"
  - "CULng 函数"
  - "货币数据类型, 转换函数"
  - "CUShort 函数"
  - "数据类型转换, 函数"
  - "数据类型 [Visual Basic], 转换"
  - "日期数据类型, 转换"
  - "日期, 转换"
  - "Decimal 数据类型, 转换"
  - "Double 数据类型, 转换"
  - "双精度数字"
  - "小数"
  - "Integer 数据类型, 转换"
  - "整数, 类型转换函数"
  - "Long 数据类型, 转换"
  - "数字, 转换"
  - "数字, 倒圆"
  - "返回值, 数据类型"
  - "舍入数, 四舍六入五成双"
  - "舍入数, 类型转换"
  - "Short 数据类型, 转换"
  - "Single 数据类型, 转换"
  - "单精度数, 转换"
  - "字符串转换, 转换函数"
  - "String 数据类型, 转换"
  - "文本, 转换"
  - "时间, 转换"
  - "类型转换, 函数"
  - "类型转换, Visual Basic 与 .NET Framework 的比较"
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 类型转换函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

这些函数采用内联方式编译，即转换代码是计算表达式的代码的一部分。  有时实现该转换时不需要调用某个过程，这将提高性能。  每个函数都将表达式强制转换为一种特定的数据类型。  
  
## 语法  
  
```  
CBool(expression)  
CByte(expression)  
CChar(expression)  
CDate(expression)  
CDbl(expression)  
CDec(expression)  
CInt(expression)  
CLng(expression)  
CObj(expression)  
CSByte(expression)  
CShort(expression)  
CSng(expression)  
CStr(expression)  
CUInt(expression)  
CULng(expression)  
CUShort(expression)  
```  
  
## 组成部分  
 `expression`  
 必选。  源数据类型的任何表达式。  
  
## 返回值数据类型  
 函数名确定它返回的值的数据类型，如下表所示。  
  
|函数名|返回数据类型|`expression` 参数范围|  
|---------|------------|-----------------------|  
|`CBool`|[Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|任何有效的 `Char`、`String` 或数值表达式。|  
|`CByte`|[Byte 数据类型](../../../visual-basic/language-reference/data-types/byte-data-type.md)|0 到 255（无符号）；舍入小数部分。<sup>1</sup>|  
|`CChar`|[Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)|任何有效的 `Char` 或 `String` 表达式；只转换 `String` 的第一个字符；值可以为 0 到 65535（无符号）。|  
|`CDate`|[日期数据类型](../../../visual-basic/language-reference/data-types/date-data-type.md)|任何有效的日期和时间表示法。|  
|`CDbl`|[Double 数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md)|负值取值范围为 \-1.79769313486231570E\+308 到 \-4.94065645841246544E\-324；正值取值范围为 4.94065645841246544E\-324 到 1.79769313486231570E\+308。|  
|`CDec`|[Decimal 数据类型](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|对于零变比数值，即无小数位数值，为 \+\/\-79,228,162,514,264,337,593,543,950,335。  对于具有 28 位小数位的数字，范围是  \+\/\-7.9228162514264337593543950335。  最小的可用非零数是 0.0000000000000000000000000001 \(\+\/\-1E\-28\)。|  
|`CInt`|[Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)|\-2,147,483,648 到 2,147,483,647；舍入小数部分。<sup>1</sup>|  
|`CLng`|[Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md)|\-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807；舍入小数部分。<sup>1</sup>|  
|`CObj`|[Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md)|任何有效的表达式。|  
|`CSByte`|[SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|\-128 到 127；舍入小数部分。<sup>1</sup>|  
|`CShort`|[Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)|\-32,768 到 32,767；舍入小数部分。<sup>1</sup>|  
|`CSng`|[Single 数据类型](../../../visual-basic/language-reference/data-types/single-data-type.md)|负值的取值范围为 \-3.402823E\+38 到 \-1.401298E\-45；正值的取值范围为 1.401298E\-45 到 3.402823E\+38。|  
|`CStr`|[String 数据类型](../../../visual-basic/language-reference/data-types/string-data-type.md)|`CStr` 的返回值取决于 `expression` 参数。  请参见 [返回 CStr 函数的值](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md)。|  
|`CUInt`|[UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|0 到 4,294,967,295（无符号）；舍入小数部分。<sup>1</sup>|  
|`CULng`|[Ulong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|0 到 18,446,744,073,709,551,615（无符号）；舍入小数部分。<sup>1</sup>|  
|`CUShort`|[Ushort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|0 到 65,535（无符号）；舍入小数部分。<sup>1</sup>|  
  
 <sup>1</sup> 小数部分可能要进行称为“四舍六入五成双”的特殊类型舍入。  有关更多信息，请参见“备注”。  
  
## 备注  
 通常，在 <xref:System.Convert> 类或在独立类型结构或类中，应优先使用 Visual Basic 类型转换函数，其次使用 .NET Framework 方法（例如 `ToString()`）。  Visual Basic 函数设计用于优化与 Visual Basic 代码之间的交互，并且这些函数使源代码更简短、更易阅读。  另外，.NET Framework 转换方法产生的结果不一定与 Visual Basic 函数产生的结果相同，例如当将 `Boolean` 转换为 `Integer` 的时候。  有关更多信息，请参见 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。  
  
## 行为  
  
-   **强制转换。**通常，可以使用数据类型转换函数将运算结果强制转换为某一特定数据类型而非默认数据类型。  例如，在通常发生单精度、双精度或整型运算的情况下，使用 `CDec` 强制执行小数运算。  
  
-   **转换失败。**如果传递给函数的 `expression` 超出要转换成的数据类型的范围，将发生 <xref:System.OverflowException>。  
  
-   **小数部分。**将一个非整数值转换为整型时，整数转换函数（`CByte`、`CInt`、`CLng`、`CSByte`、`CShort`、`CUInt`、`CULng` 和 `CUShort`）将移除小数部分，并将该值舍入为最接近的整数。  
  
     如果小数部分正好是 0.5，整数转换函数将其舍入为最接近的偶数整数。  例如，将 0.5 舍入为 0，并同时将 1.5 和 2.5 舍入为 2。  这有时称为*“四舍六入五成双”*，其目的是弥补在将许多这样的数字相加时可能会累积的偏量。  
  
     `CInt` 和 `CLng` 与 <xref:Microsoft.VisualBasic.Conversion.Int%2A> 和 <xref:Microsoft.VisualBasic.Conversion.Fix%2A> 函数不同，这些函数截断而不是舍入一个数字的小数部分。  此外，`Fix` 和 `Int` 总是返回与传入的数据类型相同的值。  
  
-   **日期\/时间转换。**使用 <xref:Microsoft.VisualBasic.Information.IsDate%2A> 函数确定是否可以将一个值转换为日期和时间。  `CDate` 能够识别日期文本和时间文本，但不能识别数值。  若要将 Visual Basic 6.0 `Date` 值转换为 Visual Basic 2005 或更高版本中的 `Date` 值，可以使用 <xref:System.DateTime.FromOADate%2A?displayProperty=fullName> 方法。  
  
-   **中性日期\/时间值。** [日期数据类型](../../../visual-basic/language-reference/data-types/date-data-type.md) 始终包含日期和时间信息。  为进行类型转换，Visual Basic 将 1\/1\/0001（公元 1 年 1 月 1 日）作为日期的“中性值”，将 00:00:00（午夜）作为时间的中性值。  如果将 `Date` 值转换为字符串，`CStr` 的结果字符串中将不包含中性值。  例如，如果将 `#January 1, 0001 9:30:00#` 转换为字符串，结果为“9:30:00 AM”；日期信息被删除了。  但是，原始的 `Date` 值中仍包含该日期信息，并且可通过某些函数（如 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> 函数）恢复该日期信息。  
  
-   **区域差异。**涉及字符串的类型转换函数根据应用程序的当前区域设置进行转换。  例如，`CDate` 依据系统的区域设置来识别日期的格式。  必须以正确的顺序为区域设置提供日、月、年数据，否则可能无法正确解释日期。  系统无法识别包含星期几的字符串（如“Wednesday”）的长日期格式。  
  
     如果需要以区域设置指定的格式之外的格式在值的字符串表示形式之间转换，则不能使用 Visual Basic 类型转换函数。  如果进行转换，请使用该值类型的 `ToString(IFormatProvider)` 方法和 `Parse(String, IFormatProvider)` 方法。  例如，将字符串转换为 `Double` 时，使用 <xref:System.Double.Parse%2A?displayProperty=fullName>，将 `Double` 类型的值转换为字符串时，使用 <xref:System.Double.ToString%2A?displayProperty=fullName>。  
  
## CType 函数  
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)采用第二个参数 `typename`，并且将 `expression` 强制转换为 `typename`，其中 `typename` 可以是存在有效转换的任何数据类型、结构、类或接口。  
  
 有关 `CType` 与其他类型转换关键字的比较，请参见 [DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md) 和 [TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md)。  
  
## CBool 示例  
 下面的示例使用 `CBool` 函数将表达式转换为 `Boolean` 值。  如果表达式的计算结果为非零值，`CBool` 将返回 `True`；否则返回 `False`。  
  
 [!code-vb[VbVbalrFunctions#1](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_1.vb)]  
  
## CByte 示例  
 下面的示例使用 `CByte` 函数将表达式转换为 `Byte`。  
  
 [!code-vb[VbVbalrFunctions#2](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_2.vb)]  
  
## CChar 示例  
 下面的示例使用 `CChar` 函数将 `String` 表达式的第一个字符转换为 `Char` 类型。  
  
 [!code-vb[VbVbalrFunctions#3](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_3.vb)]  
  
 `CChar` 的输入参数必须是 `Char` 或 `String` 数据类型。  由于 `CChar` 不能接受数值数据类型，因此无法使用 `CChar` 将数字转换为字符。  下面的示例获取一个表示码位（字符代码）的数字，然后将其转换为对应的字符。  它使用 <xref:Microsoft.VisualBasic.Interaction.InputBox%2A> 函数获取数字字符串，并使用 `CInt` 将该字符串转换为 `Integer` 类型，然后使用 `ChrW` 将该数字转换为 `Char` 类型。  
  
 [!code-vb[VbVbalrFunctions#4](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_4.vb)]  
  
## CDate 示例  
 下面的示例使用 `CDate` 函数将字符串转换为 `Date` 值。  通常，建议不要使用硬编码的日期和时间作为字符串（如下例所示）。  而应使用日期文本和时间文本，如 \#Feb 12、1969\# 和 \#4:45:23 PM\#。  
  
 [!code-vb[VbVbalrFunctions#5](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_5.vb)]  
  
## CDbl 示例  
 [!code-vb[VbVbalrFunctions#6](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_6.vb)]  
  
## CDec 示例  
 下面的示例使用 `CDec` 函数将一个数值转换为 `Decimal`。  
  
 [!code-vb[VbVbalrFunctions#7](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_7.vb)]  
  
## CInt 示例  
 下面的示例使用 `CInt` 函数将一个值转换为 `Integer`。  
  
 [!code-vb[VbVbalrFunctions#8](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_8.vb)]  
  
## CLng 示例  
 下面的示例使用 `CLng` 函数将多个值转换为 `Long`。  
  
 [!code-vb[VbVbalrFunctions#9](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_9.vb)]  
  
## CObj 示例  
 下面的示例使用 `CObj` 函数将一个数值转换为 `Object`。  `Object` 变量本身只包含一个四字节的指针，该指针指向赋给该变量的 `Double` 值。  
  
 [!code-vb[VbVbalrFunctions#10](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_10.vb)]  
  
## CSByte 示例  
 下面的示例使用 `CSByte` 函数将一个数值转换为 `SByte`。  
  
 [!code-vb[VbVbalrFunctions#11](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_11.vb)]  
  
## CShort 示例  
 下面的示例使用 `CShort` 函数将一个数值转换为 `Short`。  
  
 [!code-vb[VbVbalrFunctions#12](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_12.vb)]  
  
## CSng 示例  
 下面的示例使用 `CSng` 函数将多个值转换为 `Single`。  
  
 [!code-vb[VbVbalrFunctions#13](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_13.vb)]  
  
## CStr 示例  
 下面的示例使用 `CStr` 函数将一个数值转换为 `String`。  
  
 [!code-vb[VbVbalrFunctions#14](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_14.vb)]  
  
 下面的示例使用 `CStr` 函数将 `Date` 值转换为 `String` 值。  
  
 [!code-vb[VbVbalrFunctions#15](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_15.vb)]  
  
 `CStr` 始终以符合当前区域设置的标准短格式呈现 `Date` 值，如“6\/15\/2003 4:35:47 PM”。  但是，`CStr` 会取消日期的“中性值”1\/1\/0001 和时间的“中性值”00:00:00。  
  
 有关由 `CStr` 返回的值的详细信息，请参见 [返回 CStr 函数的值](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md)。  
  
## CUInt 示例  
 下面的示例使用 `CUInt` 函数将一个数值转换为 `UInteger`。  
  
 [!code-vb[VbVbalrFunctions#16](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_16.vb)]  
  
## CULng 示例  
 下面的示例使用 `CULng` 函数将一个数值转换为 `ULong`。  
  
 [!code-vb[VbVbalrFunctions#17](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_17.vb)]  
  
## CUShort 示例  
 下面的示例使用 `CUShort` 函数将一个数值转换为 `UShort`。  
  
 [!code-vb[VbVbalrFunctions#18](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_18.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Int%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Fix%2A>   
 <xref:Microsoft.VisualBasic.Strings.Format%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Hex%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Oct%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Str%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Val%2A>   
 [转换函数](../../../visual-basic/language-reference/functions/conversion-functions.md)   
 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)