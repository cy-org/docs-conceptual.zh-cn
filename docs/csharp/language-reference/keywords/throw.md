---
title: "throw（C# 参考）"
ms.date: 2015-03-02
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- throw
- throw_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- throw statement [C#]
- throw expression [C#]
- throw keyword [C#]
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
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
ms.sourcegitcommit: 81117b1419c2a9c3babd6a7429052e2b23e08a70
ms.openlocfilehash: 77f44a43b80c4cf1f12baadaaf6861b3b53244d9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="throw-c-reference"></a>throw（C# 参考）
发出程序执行期间出现异常的信号。  
  
## <a name="remarks"></a>备注

`throw` 的语法为：

```csharp
throw [e]
```
`e` 是一个派生自 <xref:System.Exception?displayProperty=nameWithType> 的类的实例。 下例使用 `throw` 语句在传递给名为 `GetNumber` 的方法的参数与内部数组的有效索引不对应时引发 @System.IndexOutOfRangeException。

[!code-cs[csrefKeyword#1](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#1)]  

然后方法调用方使用 `try-catch` 或 `try-catch-finally` 块来处理引发的异常。 下例处理由 `GetNumber` 方法引发的异常。

[!code-cs[csrefKeyword#2](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#2)]  

## <a name="re-throwing-an-exception"></a>重新引发异常

`throw` 也可以用于 `catch` 块，以重新引发在 `catch` 块中处理的异常。  在这种情况下，`throw` 不采用异常操作数。 当方法将参数从调用方传递给其他库方法时，这是最有用的，库方法引发的异常必须传递给调用方。 例如，以下示例重新引发在尝试检索未初始化字符串的第一个字符时引发的 @System.NullReferenceException。 

[!code-cs[csrefKeyword#3](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-3.cs#3)]  

> [!IMPORTANT]
> 还可以使用 `catch` 块中的 `throw e` 语法来实例化传递给调用方的新异常。 在这种情况下，将不会保留可从 @System.Exception.Stacktrace 属性获得的原始异常的堆栈跟踪。
 
## <a name="the-throw-expression"></a>`throw` 表达式

从 C# 7 开始，`throw` 可以用作表达式和语句。 这允许在以前不支持的上下文中引发异常。 这些方法包括：

- [条件运算符](../operators/conditional-operator.md)。 下例使用 `throw` 表达式在向方法传递空字符串数组时引发 @System.ArgumentException。 在 C# 7 之前，此逻辑将需要显示在 `if`/`else` 语句中。

   [!code-cs[csrefKeyword#4](../../../../samples/snippets/csharp/language-reference/keywords/throw/conditional.cs#1)]  
  
- [null 合并运算符](../operators/null-conditional-operator.md)。 在以下示例中，如果分配给 `Name` 属性的字符串为 `null`，则将 `throw` 表达式与 null 合并运算符结合使用以引发异常。
 
   [!code-cs[csrefKeyword#5](../../../../samples/snippets/csharp/language-reference/keywords/throw/coalescing.cs#1)]  
 
- expression-bodied [lambda](../../lambda-expressions.md) 或方法。 下例说明了 expression-bodied 方法，由于不支持对 @System.DateTime 值的转换，该方法引发 @System.InvalidCastException。
 
   [!code-cs[csrefKeyword#6](../../../../samples/snippets/csharp/language-reference/keywords/throw/exp-bodied.cs#1)]  
 
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [C++ 中的 try、catch 和 throw 语句](../../../csharp/language-reference/keywords/try-catch.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [如何显式引发异常](https://msdn.microsoft.com/library/xhcbs8fz)

