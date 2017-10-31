---
title: "显式数值转换表（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- conversions [C#], explicit numeric
- numeric conversions [C#], explicit
- explicit numeric conversion [C#]
- numeric data types [C#]
- types [C#], explicit numeric conversions
- type conversion [C#], explicit numeric
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0315810522be319a6bb565c99e1c8f7d1ba4701b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="explicit-numeric-conversions-table-c-reference"></a>显式数值转换表（C# 参考）
显式数值转换用于使用强制转换表达式将任何数值类型转换为任何其他数值类型，其中不存在任何隐式转换。 下表显示了这些转换。  
  
 有关转换的详细信息，请参阅[强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)。  
  
|From|到|  
|----------|--------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`Sbyte` 或 `char`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`sbyte`、`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`sbyte`、`byte`、`short` 或 `char`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`sbyte`、`byte`、`short`、`ushort`、`uint`、`ulong` 或 `char`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`sbyte`、`byte`、`short`、`ushort`、`int` 或 `char`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`ulong` 或 `char`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `char`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`sbyte`、`byte` 或 `short`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char` 或 `decimal`|  
|[double](../../../csharp/language-reference/keywords/double.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `decimal`|  
|[小数](../../../csharp/language-reference/keywords/decimal.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `double`|  
  
## <a name="remarks"></a>备注  
  
-   显式数值转换可能会导致精度降低或导致引发异常。  
  
-   将 `decimal` 值转换为整型类型时，此值会向零舍入到最接近的整数值。 如果生成的整数值处于目标类型的范围之外，则会引发 <xref:System.OverflowException>。  
  
-   从 `double` 或 `float` 值转换为整型类型时，会截断该值。 如果生成的整数值处于目标值范围之外，则结果会取决于溢出检查上下文。 在已检查的上下文中，引发 `OverflowException`；而在未检查的上下文中，结果是目标类型的未指定值。  
  
-   将 `double` 转换为 `float` 时，`double` 值舍入为最接近的 `float` 值。 如果 `double` 值太小或太大，无法匹配目标类型，结果将为零或无穷大。  
  
-   将 `float` 或 `double` 转换为 `decimal` 时，源值转换为 `decimal` 表示形式，并并五入到第 28 位小数后最接近的数（如果需要）。 根据源值的值，可能出现以下结果之一：  
  
    -   如果源值太小，无法表示为 `decimal`，结果则为零。  
  
    -   如果源值为 NaN（非数值）、无穷大或太大而无法表示为 `decimal`，则引发 `OverflowException`。  
  
-   将 `decimal` 转换为 `float` 或 `double` 时，`decimal` 值舍入到最接近的 `double` 或 `float` 值。  
  
 有关显式转换的详细信息，请参阅 C# 语言规范中的显式。 有关如何访问此规范的详细信息，请参阅 [C# 语言规范](../../../csharp/language-reference/language-specification/index.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [() 运算符](../../../csharp/language-reference/operators/invocation-operator.md)   
 [整型类型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)

