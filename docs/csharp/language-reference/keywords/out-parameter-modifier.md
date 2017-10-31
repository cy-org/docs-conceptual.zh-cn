---
title: "out 参数修饰符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], out
- out parameters [C#]
ms.assetid: 3fce0dc5-03f4-4faa-bd61-36c41bc6baf1
caps.latest.revision: 9
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
ms.sourcegitcommit: 59e445ac27f07c85d9e98c5f595cf5f935f75443
ms.openlocfilehash: 9a0a488c6f444608a335cd990847774fb6fe9e3f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="out-parameter-modifier-c-reference"></a>out 参数修饰符（C# 参考）
`out` 关键字通过引用传递参数。 它与 [ref](../../../csharp/language-reference/keywords/ref.md) 关键字相似，只不过 `ref` 要求在传递之前初始化变量。 若要使用 `out` 参数，方法定义和调用方法均必须显式使用 `out` 关键字。 例如:   
  
 [!code-cs[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/out/out-1.cs)]  

> [!NOTE] 
> `out` 关键字也可与泛型类型参数结合使用，以指定该类型参数是协变参数。 有关在此上下文中使用 `out` 关键字的详细信息，请参阅 [out（泛型修饰符）](../../../csharp/language-reference/keywords/out-generic-modifier.md)。
  
 作为 `out` 参数传递的变量在方法调用中传递之前不必进行初始化。 但是，被调用的方法需要在返回之前赋一个值。  
  
 尽管 `ref` 和 `out` 关键字会导致不同的运行时行为，它们并不被视为编译时方法签名的一部分。 因此，如果唯一的不同是一个方法采用 `ref` 参数，而另一个方法采用 `out` 参数，则无法重载这两个方法。 例如，以下代码将不会编译：  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
但是，如果一个方法采用 `ref` 或 `out` 参数，而另一个方法采用其他参数，则可以完成重载，如：  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../../samples/snippets/csharp/language-reference/keywords/out/out-3.cs)]  
  
 属性不是变量，因此不能作为 `out` 参数传递。  
  
 有关传递数组的信息，请参阅[使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 你不能将 `ref` 和 `out` 关键字用于以下几种方法：  
  
-   异步方法，通过使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符定义。  
  
-   迭代器方法，包括 [yield return](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  

## <a name="declaring-out-arguments"></a>声明 `out` 参数   

 如果希望方法返回多个值，可以声明具有多个 `out` 参数的方法。 下面的示例使用 `out` 返回具有单个方法调用的三个变量。 注意，第三个参数赋 null 值。 这使得方法可以有选择地返回值。  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../../samples/snippets/csharp/language-reference/keywords/out/out-4.cs)]  

 [重试模式](/visualstudio/code-quality/ca1021-avoid-out-parameters#try-pattern-methods.md)会返回一个 `bool`，指示某个操作是成功还是失败，并在 `out` 参数中返回该操作生成的值。 许多分析方法（如 [DateTime.TryParse](xref:System.DateTime.TryParse(System.String,System.DateTime@)) 方法）都采用此模式。
   
## <a name="calling-a-method-with-an-out-argument"></a>调用具有 `out` 参数的方法

在 C# 6 及更早版本中，必须先在单独的语句中声明变量，然后才能将其作为 `out` 参数传递。 下面的示例先声明了变量 `number`，然后再将它传递给将字符串转换为数字的 [Int32.TryParse](xref:System.Int32.TryParse(System.String,System.Int32@)) 方法。

 [!code-cs[csrefKeywordsMethodParams#5](../../../../samples/snippets/csharp/language-reference/keywords/out/out-5.cs)]  

从 C# 7 开始，可以在方法调用的参数列表而不是单独的变量声明中声明 `out` 变量。 这使得代码更简洁可读，还能防止在方法调用之前无意中向该变量赋值。 下面的示例与上一个示例基本相同，不同之处在于它在对 [Int32.TryParse](xref:System.Int32.TryParse(System.String,System.Int32@)) 方法的调用中定义了 `number` 变量。

 [!code-cs[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/out/out-6.cs)]  
   
在上一个示例中，`number` 变量被强类型化为 `int`。 你也可以声明一个隐式类型本地变量，如以下示例所示。

 [!code-cs[csrefKeywordsMethodParams#7](../../../../samples/snippets/csharp/language-reference/keywords/out/out-7.cs)]  
   
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)

