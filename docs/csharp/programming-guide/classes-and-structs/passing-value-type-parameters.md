---
title: "传递值类型参数（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- method parameters [C#], value types
- parameters [C#], value
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
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
ms.openlocfilehash: a3377630fc4294831f6b9d66a69377aa42d973f1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="passing-value-type-parameters-c-programming-guide"></a>传递值类型参数（C# 编程指南）
一个[值类型](../../../csharp/language-reference/keywords/value-types.md)变量包含它直接与[引用类型](../../../csharp/language-reference/keywords/reference-types.md)变量相对的数据，其中包含对其数据的引用。 按值将值-类型变量传递给方法，意味着将变量副本传递给该方法。 在方法内发生的对该实参进行的任何更改不会影响存储在形参变量中的原始数据。 如果想用调用的方法来更改参数的值，必须使用 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 关键字，通过引用进行传递。 为简单起见，下面的示例使用 `ref`。  
  
## <a name="passing-value-types-by-value"></a>按值传递值类型  
 下面的示例演示按值传递值-类型参数。 变量 `n` 按值传递给方法 `SquareIt`。 在方法内发生的任何更改不会影响该变量的原始值。  
  
 [!code-cs[csProgGuideParameters#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_1.cs)]  
  
 变量 `n` 是值类型。 它包含其数据，值为 `5`。 调用 `SquareIt` 时，`n` 的内容复制到参数 `x` 中，这是该方法内的平方值。 但是在 `Main` 中，`n` 的值在调用 `SquareIt` 方法之后与之前相同。 在方法内发生的更改只影响本地变量 `x`。  
  
## <a name="passing-value-types-by-reference"></a>按引用传递值类型  
 下面的示例与上述示例相同，除了自变量是作为 `ref` 参数传递的。 `x` 在方法中更改时，基础自变量的值 `n` 也更改。  
  
 [!code-cs[csProgGuideParameters#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_2.cs)]  
  
 在此示例中，它传递的不是 `n` 的值；而是传递 `n` 的引用。 参数 `x` 不是 [int](../../../csharp/language-reference/keywords/int.md)；它是对 `int` 的引用，在这种情况下，是对 `n` 的引用。 因此，当 `x` 在方法中进行平方计算时，实际求平方值的就是 `x` 所指的 `n`。  
  
## <a name="swapping-value-types"></a>交换值类型  
 更改自变量值的一个常见示例是交换方法，其中将两个变量传递给方法，并由该方法交换其内容。 必须通过引用将自变量传递给交换方法。 否则，交换参数在方法中的本地副本，并且调用方法中不会发生更改。 下面的示例交换整数值。  
  
 [!code-cs[csProgGuideParameters#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_3.cs)]  
  
 调用 `SwapByRef` 方法时，在调用中使用 `ref` 关键字，如下面的示例中所示。  
  
 [!code-cs[csProgGuideParameters#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_4.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [传递引用类型参数](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)

