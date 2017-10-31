---
title: "string（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- string
- string_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.assetid: 3037e558-fb22-494d-bca1-a15ade11b11a
caps.latest.revision: 31
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 56847aad4cb8b0427594a299df2306d21675506b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="string-c-reference"></a>string（C# 参考）
`string` 类型表示零个或多个 Unicode 字符的序列。 `string` 是 .NET Framework 中 <xref:System.String> 的别名。  
  
 尽管 `string` 为引用类型，定义相等运算符（`==` 和 `!=`）是为了比较 `string` 对象（而不是引用）的值。 这使得对字符串相等性的测试更为直观。 例如：  
  
```csharp  
string a = "hello";  
string b = "h";  
// Append to contents of 'b'  
b += "ello";  
Console.WriteLine(a == b);  
Console.WriteLine((object)a == (object)b);  
```  
  
 此时将显示“True”，然后显示“False”，因为字符串的内容是相等的，但 `a` 和 `b` 并不指代同一字符串实例。  
  
 + 运算符可连接字符串：  
  
```csharp  
string a = "good " + "morning";  
```  
  
 这将创建包含“good morning”的字符串对象。  
  
 字符串是不可变的，即：字符串对象在创建后，尽管从语法上看似乎可以更改其内容，但事实上并不可行。 例如，编写此代码时，编译器实际上会创建一个新的字符串对象来保存新的字符序列，且该新对象将赋给 b。 然后，字符串“h”便可进行垃圾回收。  
  
```csharp
string b = "h";  
b += "ello";  
```  
  
 [] 运算符可用于只读访问 `string` 的个别字符：  
  
```csharp  
string str = "test";  
char x = str[2];  // x = 's';  
```  
  
 字符串文本属于类型 `string` 且可编写为两种形式，带引号和 @-quoted。 带引号字符串括在双引号 (") 内。  
  
```csharp  
"good morning"  // a string literal  
```  
  
 字符串文本可包含任何字符文本。 包括转义序列。 下面的示例使用转义序列 `\\` 表示反斜杠，使用 `\u0066` 表示字母 f，以及使用 `\n` 表示换行符。  
  
```  
string a = "\\\u0066\n";  
Console.WriteLine(a);  
```  
  
> [!NOTE]
>  转义码 `\udddd`（其中 `dddd` 是一个四位数字）表示 Unicode 字符 U+`dddd`。 另外，还可识别八位 Unicode 转义码：`\Udddddddd`。  
  
 逐字字符串文本以 @ 开头，并且也括在双引号内。 例如:   
  
```csharp  
@"good morning"  // a string literal  
```  
  
 逐字字符串的优点是不处理转义序列，这样就可轻松编写完全限定的文件名等：  
  
```csharp  
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"  
```  
  
 若要在 @-quoted 字符串中包含双引号，双倍添加即可：  
  
```csharp  
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.  
```  
  
 另一种 @ 符号用法是使用属于 C# 关键字的引用 ([/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)) 标识符。  
  
 有关 C# 中的字符串的详细信息，请参阅[字符串](../../../csharp/programming-guide/strings/index.md)。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsTypes#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/string_1.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [Best Practices for Using Strings](../../../standard/base-types/best-practices-strings.md) （有关使用字符串的最佳做法）  
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [基本字符串操作](../../../standard/base-types/basic-string-operations.md)   
 [创建新字符串](../../../standard/base-types/creating-new.md)   
 [设置数值结果表的格式](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)

