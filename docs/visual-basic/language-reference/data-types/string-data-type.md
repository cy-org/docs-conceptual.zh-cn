---
title: "字符串数据类型 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.String
dev_langs:
- VB
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings, string data type
- literals, string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals
- data types [Visual Basic], assigning
- String literals
- identifier type characters, $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
caps.latest.revision: 19
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
ms.openlocfilehash: 9221a89a1fb46609b4b8550968e3a2bbe874772c
ms.lasthandoff: 03/13/2017

---
# <a name="string-data-type-visual-basic"></a>String 数据类型 (Visual Basic)
从 0 到 65535 之间的值中存储无符号的 16 位 （双字节） 码位的序列该范围。 每个*代码点*，或字符代码，表示单个 Unicode 字符。 一个字符串可以包含从 0 到二十亿 (2 ^31) 的 Unicode 字符。  
  
## <a name="remarks"></a>备注  
 使用`String`数据类型以保存多个字符的数组管理开销没有`Char()`，数组`Char`元素。  
  
 默认值为`String`是`Nothing`（空引用）。 请注意，这并不相同，则为空字符串 (值`""`)。  
  
## <a name="unicode-characters"></a>Unicode 字符  
 Unicode 第一个 128 个码位 (0-127) 对应的字母和标准的美式键盘上的符号。 这些第一个 128 个码位都与 ASCII 字符集定义相同。 第二个 128 个码位 (128 到 255) 表示特殊字符，如基于拉丁语字母、 重音、 货币符号和秒的小数部分。 Unicode 使用各种各样的符号的剩余的码位 (256-65535)。 这包括全球范围内的文本字符、 音调符号，以及数学和技术符号。  
  
 您可以使用方法，如<xref:System.Char.IsDigit%2A>和<xref:System.Char.IsPunctuation%2A>上中的单个字符`String`变量以确定其 Unicode 分类。</xref:System.Char.IsPunctuation%2A> </xref:System.Char.IsDigit%2A>  
  
## <a name="format-requirements"></a>格式要求  
 必须将括`String`文字用引号引起来 (`" "`)。 如果您必须作为一个字符串中字符包含引号，则使用两个连续的引号 (`""`)。 下面的示例阐释了这一点。  
  
```  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 请注意连续的引号表示字符串中的引号无关的引号开始和结束`String`文字。  
  
## <a name="string-manipulations"></a>字符串操作  
 一旦将分配到的字符串`String`变量时，该字符串是*不可变*，这意味着您不能更改它的长度或内容。 在修改以任何方式的字符串时，Visual Basic 创建一个新字符串和放弃上一个。 `String`变量然后指向新的字符串。  
  
 您可以操作的内容`String`变量使用各种字符串函数。 下面的示例阐释<xref:Microsoft.VisualBasic.Strings.Left%2A>函数</xref:Microsoft.VisualBasic.Strings.Left%2A>  
  
```  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 可能会用前导空格或尾随空格填充由另一个组件创建的字符串。 如果您收到这样的字符串，则可以使用<xref:Microsoft.VisualBasic.Strings.Trim%2A>， <xref:Microsoft.VisualBasic.Strings.LTrim%2A>，和<xref:Microsoft.VisualBasic.Strings.RTrim%2A>函数来删除这些空格。</xref:Microsoft.VisualBasic.Strings.RTrim%2A> </xref:Microsoft.VisualBasic.Strings.LTrim%2A> </xref:Microsoft.VisualBasic.Strings.Trim%2A>  
  
 有关字符串操作的详细信息，请参阅[字符串](../../../visual-basic/programming-guide/language-features/strings/index.md)。  
  
## <a name="programming-tips"></a>编程提示  
  
-   **负数。** 请记住字符持有的`String`是无符号，并且不能表示负值。 在任何情况下，不应使用`String`存放数值。  
  
-   **互操作注意事项。** 如果不是为.NET Framework 编写的组件与交互如自动化或 COM 对象，请记住，字符串字符具有不同的数据宽度 （8 位） 在其他环境中。 如果您将 8 位字符的字符串参数传递给此类组件，将其声明为`Byte()`，数组`Byte`元素，而不是`String`在新的 Visual Basic 代码。  
  
-   **类型字符。** 追加标识符类型字符`$`到任何标识符会将其强制为`String`数据类型。 `String`有没有文本类型字符。 但是，编译器将用引号引起来的文本 (`" "`) 作为`String`。  
  
-   **Framework 类型。** .NET Framework 中的对应类型是<xref:System.String?displayProperty=fullName>类。</xref:System.String?displayProperty=fullName>  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.String?displayProperty=fullName></xref:System.String?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何︰ 调用采用无符号的类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)

