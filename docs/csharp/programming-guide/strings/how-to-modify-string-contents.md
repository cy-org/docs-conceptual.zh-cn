---
title: "如何：修改字符串内容（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], modifying
ms.assetid: b6c20bba-ce22-43d7-ad1b-5ce65f714055
caps.latest.revision: 16
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
ms.openlocfilehash: 114b6fdabd235d7e57947e77b672352e28aff11e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-modify-string-contents-c-programming-guide"></a>如何：修改字符串内容（C# 编程指南）
由于字符串是不可变的，因此创建字符串对象后，（在不使用不安全代码的情况下）便不能再修改其值。 但是，可通过多种方法修改字符串的值并将结果存储到新的字符串对象。 <xref:System.String?displayProperty=fullName> 类提供作用于输入字符串并返回新字符串对象的方法。 在很多情况下，可以将新对象赋予保留原始字符串的变量。 <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName> 类提供其他一些以类似方式工作的方法。 <xref:System.Text.StringBuilder?displayProperty=fullName> 类提供一个可“就地”修改的字符缓冲区。 调用 <xref:System.Text.StringBuilder.ToString%2A?displayProperty=fullName> 方法可创建包含该缓冲区的当前内容的新字符串对象。  
  
## <a name="example"></a>示例  
 以下示例演示替换或删除指定字符串中的子字符串的各种方法。  
  
 [!code-cs[csProgGuideStrings#28](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_1.cs)]  
  
## <a name="example"></a>示例  
 若要使用数组表示法访问字符串中的各个字符，可以使用 <xref:System.Text.StringBuilder> 对象，该对象重载 `[]` 运算符，提供对其内部字符缓冲区的访问。 也可以使用 <xref:System.String.ToCharArray%2A> 方法将该字符串转换为字符数组。 以下示例使用 `ToCharArray` 创建该数组。 然后修改此数组中的某些元素。 之后再调用采用字符数组作为输入参数的字符串构造函数，创建新字符串。  
  
 [!code-cs[csProgGuideStrings#24](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_2.cs)]  
  
## <a name="example"></a>示例  
 以下示例针对的是某些非常罕见的情况，在这些情况下，建议使用不安全代码以类似于 C 样式字符数组的方式就地修改字符串。 此示例演示如何使用 fixed 关键字“就地”访问各个字符。 此外还演示对字符串进行不安全操作可能产生的一个副作用，此副作用是由于 C# 编译器在内部存储（暂存）字符串的方式而导致的。 通常，除非绝对必要，否则不应使用这种方法。  
  
 [!code-cs[csProgGuideStrings#29](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_3.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)

