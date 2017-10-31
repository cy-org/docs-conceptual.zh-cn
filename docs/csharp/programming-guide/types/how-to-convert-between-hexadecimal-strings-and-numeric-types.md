---
title: "如何：在十六进制字符串与数值类型之间转换（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- hexadecimal strings [C#], converting to numeric type
- conversions [C#], hexidecimal strings
- strings [C#], converting hexadecimal strings
- hexadecimal strings [C#]
ms.assetid: 7115c49f-7d1d-40c3-8bd9-aae0cc1d46b6
caps.latest.revision: 19
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
ms.openlocfilehash: 312b18e6bf30ace166435e51b1b83937b5c6bf38
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-convert-between-hexadecimal-strings-and-numeric-types-c-programming-guide"></a>如何：在十六进制字符串与数值类型之间转换（C# 编程指南）
以下示例演示如何执行下列任务：  
  
-   获取[字符串](../../../csharp/language-reference/keywords/string.md)中每个字符的十六进制值。  
  
-   获取与十六进制字符串中的每个值对应的 [char](../../../csharp/language-reference/keywords/char.md)。  
  
-   将十六进制 `string` 转换为 [int](../../../csharp/language-reference/keywords/int.md)。  
  
-   将十六进制 `string` 转换为 [float](../../../csharp/language-reference/keywords/float.md)。  
  
-   将[字节](../../../csharp/language-reference/keywords/byte.md)数组转换为十六进制 `string`。  
  
## <a name="example"></a>示例  
 此示例输出 `string` 中每个字符的十六进制值。 首先，将 `string` 分析为字符数组。 然后，对每个字符调用 <xref:System.Convert.ToInt32%28System.Char%29>获取相应的数值。 最后，在 `string` 中将数字的格式设置为十六进制表示形式。  
  
 [!code-cs[csProgGuideTypes#30](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_1.cs)]  
  
## <a name="example"></a>示例  
 此示例分析十六进制值的 `string` 并输出对应于每个十六进制值的字符。 首先，调用 [Split(Char\[\])](xref:System.String.Split(System.Char[])) 方法以获取每个十六进制值作为数组中的单个 `string`。 然后，调用 <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29>将十六进制值转换为表示为 [int](../../../csharp/language-reference/keywords/int.md) 的十进制值。 示例中演示了 2 种不同方法，用于获取对应于该字符代码的字符。 第 1 种方法是使用 <xref:System.Char.ConvertFromUtf32%28System.Int32%29>，它将对应于整型参数的字符作为 `string` 返回。 第 2 种方法是将 `int` 显式转换为 [char](../../../csharp/language-reference/keywords/char.md)。  
  
 [!code-cs[csProgGuideTypes#31](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_2.cs)]  
  
## <a name="example"></a>示例  
 此示例演示了将十六进制 `string` 转换为整数的另一种方法，即调用 <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29> 方法。  
  
 [!code-cs[csProgGuideTypes#32](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_3.cs)]  
  
## <a name="example"></a>示例  
 下面的示例演示了如何使用 <xref:System.BitConverter?displayProperty=fullName> 类和 <xref:System.Int32.Parse%2A?displayProperty=fullName> 方法将十六进制 `string` 转换为 [float](../../../csharp/language-reference/keywords/float.md)。  
  
 [!code-cs[csProgGuideTypes#39](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_4.cs)]  
  
## <a name="example"></a>示例  
 下面的示例演示了如何使用 <xref:System.BitConverter?displayProperty=fullName> 类将[字节](../../../csharp/language-reference/keywords/byte.md)数组转换为十六进制字符串。  
  
 [!code-cs[csProgGuideTypes#38](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_5.cs)]  
  
## <a name="see-also"></a>请参阅  
 [标准数字格式字符串](../../../standard/base-types/standard-numeric-format-strings.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [如何：确定字符串是否表示数值](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)

