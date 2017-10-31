---
title: "#<a name=\"if-c-reference\"></a>if（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#if'
dev_langs:
- CSharp
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
caps.latest.revision: 17
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
ms.openlocfilehash: f70dac98d5731370ae961f795b08a71946867d9b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="if-c-reference"></a>#if（C# 参考）
如果 C# 编译器遇到 `#if` 指令，最终是 [#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md) 指令，仅当定义指定的符号时，它才编译这些指令之间的代码。  与 C 和 C++ 不同的是，不能将数字的值分配给一个符号；C# 中的 #if 语句是一个布尔值，并仅测试是否定义该符号。 例如，  
  
```csharp
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
 仅可以使用运算符 [==](../../../csharp/language-reference/operators/equality-comparison-operator.md)（相等）、[!=](../../../csharp/language-reference/operators/not-equal-operator.md)（不相等）测试 [true](../../../csharp/language-reference/keywords/true.md) 或 [false](../../../csharp/language-reference/keywords/false.md)。 True 表示定义该符号。 语句 `#if DEBUG` 具有与 `#if (DEBUG == true)` 相同的含义。 可以使用运算符 [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) (and)、[&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) (or) 和 [!](../../../csharp/language-reference/operators/logical-negation-operator.md) (not) 评估是否已经定义了多个符号。 还可以用括号对符号和运算符进行分组。  
  
## <a name="remarks"></a>备注  
 `#if` 以及 [#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md)、[#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md)、[#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md)、[#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) 和 [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 指令，允许基于是否存在一个或多个符号包括或排除代码。 这在编译调试版本的代码或编译特定配置的代码时会很有用。  
  
 以 `#if` 指令开头的条件指令必须以 `#endif` 指令显式终止。  
  
 `#define` 允许你定义一个符号，这样一来，通过将该符号用作传递给 `#if` 指令的表达式，该表达式的计算结果为 `true`。  
  
 还可以通过 [/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md) 编译器选项来定义符号。 可以通过 [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 取消定义符号。  
  
 使用 `/define` 或 `#define` 定义的符号与具有相同名称的变量不冲突。 也就是说，变量名称不应传递给预处理器指令，且符号仅能由预处理器指令评估。  
  
 使用 `#define` 创建的符号的作用域是在其中定义它的文件。  
  
## <a name="example"></a>示例  
  
```csharp
// preprocessor_if.cs  
#define DEBUG#define MYTEST  
using System;  
public class MyClass   
{  
    static void Main()   
    {  
#if (DEBUG && !MYTEST)  
        Console.WriteLine("DEBUG is defined");  
#elif (!DEBUG && MYTEST)  
        Console.WriteLine("MYTEST is defined");  
#elif (DEBUG && MYTEST)  
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else  
        Console.WriteLine("DEBUG and MYTEST are not defined");  
#endif  
    }  
}  
```  
  
 **DEBUG 和 MYTEST 已定义**   
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)

