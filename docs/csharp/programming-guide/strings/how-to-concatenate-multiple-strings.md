---
title: "如何：串联多个字符串（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- joining strings [C#]
- concatenating strings [C#]
- strings [C#], concatenation
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
caps.latest.revision: 21
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
ms.openlocfilehash: b191a61258a496115a4d7045046f9b4a2dbee58c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-concatenate-multiple-strings-c-programming-guide"></a>如何：串联多个字符串（C# 编程指南）
串联是将一个字符串追加到另一字符串末尾的过程。 使用 `+` 运算符串联字符串文本或字符串常数时，编译器创建一个字符串。 不发生任何运行时串联。 但是，字符串变量仅可在运行时串联。 在这种情况下，你应当了解各种方法的性能影响。  
  
## <a name="example"></a>示例  
 如下示例演示如何将长字符串文本拆分为较短的字符串，从而提高源代码的可读性。 编译时将这些部分串联到一个字符串中。 无论涉及的字符串数量多少，均不存在运行时性能开销。  
  
 [!code-cs[csProgGuideStrings#30](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_1.cs)]  
  
## <a name="example"></a>示例  
 要串联字符串变量，可使用 `+` 或 `+=` 运算符，或者使用 <xref:System.String.Concat%2A?displayProperty=fullName>、<xref:System.String.Format%2A?displayProperty=fullName> 或 <xref:System.Text.StringBuilder.Append%2A?displayProperty=fullName> 方法。 `+` 运算符易于使用，有利于产生直观代码。 即使在一个语句中使用多个 + 运算符，字符串内容也仅会被复制一次。 但如果多次重复此操作，例如在循环中重复此操作，效率可能会受到影响。 例如，注意下面的代码：  
  
 [!code-cs[csProgGuideStrings#23](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_2.cs)]  
  
> [!NOTE]
>  在字符串串联操作中，C# 编译器将 null 字符串和空字符串视为相同，但不转换原始 null 字符串的值。  
  
 如果不串联大量字符串（例如，在循环中），此代码的性能开销可能并不显著。 这一点同样适用于 <xref:System.String.Concat%2A?displayProperty=fullName> 和 <xref:System.String.Format%2A?displayProperty=fullName> 方法。  
  
 但是，如果性能极为重要，则应始终使用 <xref:System.Text.StringBuilder> 类来串联字符串。 如下代码使用 <xref:System.Text.StringBuilder> 类的 <xref:System.Text.StringBuilder.Append%2A> 方法串联字符串，不会产生 `+` 运算符的链式效应。  
  
 [!code-cs[csProgGuideStrings#22](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_3.cs)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.String>   
 <xref:System.Text.StringBuilder>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)

