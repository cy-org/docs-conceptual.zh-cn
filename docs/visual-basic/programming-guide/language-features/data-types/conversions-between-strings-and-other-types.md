---
title: "字符串和其他类型 (Visual Basic 中) 之间的转换 |Microsoft 文档"
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
- data type conversion, string
- conversions, type
- string conversion
- conversions, data type
- type conversion, string
- regional options
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
caps.latest.revision: 16
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
ms.openlocfilehash: 2d0a5fc7327ecd6339b5021e1b4cb87cc54bd2bc
ms.lasthandoff: 03/13/2017

---
# <a name="conversions-between-strings-and-other-types-visual-basic"></a>字符串和其他类型之间的转换 (Visual Basic)
您可以将数值转换`Boolean`，或日期/时间值到`String`。 您也可以反向执行转换，从为数字、 字符串值`Boolean`，或`Date`— 字符串的内容可以被解释为目标数据类型的有效值。 如果无法转换，将发生运行时错误。  
  
 所有这些分配，在任一方向的转换收缩转换。 You should use the type conversion keywords (`CBool`, `CByte`, `CDate`, `CDbl`, `CDec`, `CInt`, `CLng`, `CSByte`, `CShort`, `CSng`, `CStr`, `CUInt`, `CULng`, `CUShort`, and `CType`). <xref:Microsoft.VisualBasic.Strings.Format%2A>和<xref:Microsoft.VisualBasic.Conversion.Val%2A>函数为您提供更多控制权字符串和数字之间的转换。</xref:Microsoft.VisualBasic.Conversion.Val%2A> </xref:Microsoft.VisualBasic.Strings.Format%2A>  
  
 如果已定义的类或结构，您可以定义类型之间的转换运算符`String`和类或结构的类型。 有关详细信息，请参阅[如何︰ 定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)。  
  
## <a name="conversion-of-numbers-to-strings"></a>数字转换为字符串  
 您可以使用`Format`函数将数字转换为带格式的字符串，其中可以包括不仅相应的数字，但格式化符号，如货币符号 (如`$`)，千位分隔符或*数字分组符号*(如`,`)，和小数点分隔符 (如`.`)。 `Format`根据相应的符号将自动使用**区域选项**Windows 中指定的设置**控制面板**。  
  
 请注意，串联 (`&`) 运算符可以将数字转换为字符串隐式，如以下示例所示。  
  
```  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## <a name="conversion-of-strings-to-numbers"></a>字符串转换为数字  
 您可以使用`Val`函数来显式转换为数字的字符串中的数字。 `Val`读取字符串，直到它遇到数字、 空格、 选项卡上，换行符或句点以外的字符。 序列"< O"和"< H"alter 数字系统的基数和终止扫描。 在停止读取，直到`Val`将所有合适的字符转换为数字值。 例如，下面的语句返回的值`141.825`。  
  
 `Val("   14   1.825 miles")`  
  
 当[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将字符串转换为数字值，它使用**区域选项**Windows 中指定的设置**控制面板**来解释千位分隔符、 小数分隔符和货币符号。 这意味着转换可能成功下一项但不是能是其他设置。 例如，`"$14.20"`是可以接受的英语 （美国） 区域设置中但不是在法语区域设置。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [如何︰ 将对象转换为另一种类型在 Visual Basic 中](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [基于 .NET Framework 的国际应用程序简介](https://docs.microsoft.com/visualstudio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)
