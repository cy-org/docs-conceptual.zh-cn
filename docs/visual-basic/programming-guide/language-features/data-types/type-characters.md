---
title: "键入的字符 (Visual Basic 中) |Microsoft 文档"
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
- '&H prefix for hexadecimal values'
- hexadecimal literals
- F literal type character
- '& identifier type character'
- type characters
- octal literals
- literals, hexadecimal
- '&O prefix for octal values'
- literals, default types
- defaults, literal types
- C literal type character
- type characters, literal
- $ identifier type character
- L literal type character
- UI literal type characters
- default literal types
- D literal type character
- literals, octal
- S literal type character
- '! identifier type character'
- US literal type characters
- '% identifier type character'
- data types [Visual Basic], type characters
- characters, identifier type
- type characters, identifier
- '# identifier type character'
- identifier type characters
- literal type characters
- I literal type character
- R literal type character
- '@ identifier type character'
- UL literal type characters
- literal types, default
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
caps.latest.revision: 22
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
ms.openlocfilehash: 6e112e7d221ef8e7a660094306bbb242c988e843
ms.lasthandoff: 03/13/2017

---
# <a name="type-characters-visual-basic"></a>类型字符 (Visual Basic)
除了声明语句中指定的数据类型，您可以强制使用某些编程元素的数据类型*键入字符*。 类型字符必须紧跟具有任何类型不允许插入字符的元素。  
  
 类型字符不是名称的元素的一部分。 类型字符定义的元素可以引用不带类型字符。  
  
## <a name="identifier-type-characters"></a>标识符类型字符  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供一组*标识符类型字符串*，您可以用于在声明中指定的变量或常量的数据类型。 下表显示可用的标识符类型字符及其用法的示例。  
  
|标识符类型字符|数据类型|示例|  
|-------------------------------|---------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 对于没有标识符类型字符串存在`Boolean`， `Byte`， `Char`， `Date`， `Object`， `SByte`， `Short`， `UInteger`， `ULong`，或`UShort`数据类型或任何复合数据类型，如数组或结构。  
  
 在某些情况下，您可以将附加`$`字符到[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]正常工作，例如`Left$`而不是`Left`，以获取返回的值类型为`String`。  
  
 在所有情况下，标识符类型字符必须紧跟在标识符名称。  
  
## <a name="literal-type-characters"></a>文本类型字符  
 一个*文字*是一种数据类型具有特定值的文本表示形式。  
  
### <a name="default-literal-types"></a>默认文本类型  
 文本的形式通常出现在您的代码中确定其数据类型。 下表显示这些默认类型。  
  
|文本形式|默认数据类型|示例|  
|-----------------------------|-----------------------|-------------|  
|数值，没有小数部分|`Integer`|`2147483647`|  
|数值，没有小数部分，对于来说太大`Integer`|`Long`|`2147483648`|  
|数值，小数部分|`Double`|`1.2`|  
|括在双引号内|`String`|`"A"`|  
|包含在数字符号|`Date`|`#5/17/1993 9:32 AM#`|  
  
### <a name="forced-literal-types"></a>强制文本类型  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供一组*文本类型字符*，这可用于强制文本采用一个数据类型不是它的形式表示。 通过将字符追加到文本末尾执行此操作。 下表显示可用的文本类型字符及其用法的示例。  
  
|文本类型字符|数据类型|示例|  
|----------------------------|---------------|-------------|  
|`S`|`Short`|`I = 347S`|  
|`I`|`Integer`|`J = 347I`|  
|`L`|`Long`|`K = 347L`|  
|`D`|`Decimal`|`X = 347D`|  
|`F`|`Single`|`Y = 347F`|  
|`R`|`Double`|`Z = 347R`|  
|`US`|`UShort`|`L = 347US`|  
|`UI`|`UInteger`|`M = 347UI`|  
|`UL`|`ULong`|`N = 347UL`|  
|`C`|`Char`|`Q = "."C`|  
  
 对于存在没有文本类型字符`Boolean`， `Byte`， `Date`， `Object`， `SByte`，或`String`数据类型或任何复合数据类型，如数组或结构。  
  
 文本也可以使用标识符类型字符 (`%`， `&`， `@`， `!`， `#`， `$`)，如可能是变量、 常量和表达式。 但是，文本类型字符 (`S`， `I`， `L`， `D`， `F`， `R`， `C`) 可仅与原义字符。  
  
 在所有情况下，文本类型字符必须紧跟的文字值。  
  
## <a name="hexadecimal-and-octal-literals"></a>十六进制和八进制文本  
 通常，编译器将解释整数文字采用十进制 (基数为 10) 数字系统。 您可以强制一个整数为十六进制 (基数为 16) 与`&H`前缀，并且您可以强制为八进制 (基数为 8) 与`&O`前缀。 跟在前缀的数字必须适合于数字系统。 下表阐释了这一点。  
  
|号码基|前缀|有效的数字值|示例|  
|-----------------|------------|------------------------|-------------|  
|十六进制（以 16 为基数）|`&H`|0-9 和 A-F|`&HFFFF`|  
|八进制（以 8 为基数）|`&O`|0-7|`&O77`|  
  
 您可以按照与文本类型字符前缀的文本。 下面的示例演示了此过程。  
  
```  
Dim counter As Short = &H8000S  
Dim flags As UShort = &H8000US  
```  
  
 在上一示例中，`counter`的十进制值为-32768 和`flags`32768 的十进制值。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)
