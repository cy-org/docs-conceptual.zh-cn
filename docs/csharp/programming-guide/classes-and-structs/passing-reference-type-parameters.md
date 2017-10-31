---
title: "传递引用类型参数（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- method parameters [C#], reference types
- parameters [C#], reference
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
caps.latest.revision: 14
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
ms.openlocfilehash: 3f57dc9f0de6fae6da3ec8e6e6cfdc3a21baeaea
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="passing-reference-type-parameters-c-programming-guide"></a>传递引用类型参数（C# 编程指南）
[引用类型](../../../csharp/language-reference/keywords/reference-types.md)的变量不直接包含其数据；它包含对其数据的引用。 如果按值传递引用类型参数，则可能会按引用更改指向的数据，例如类成员的值。 但是，不能更改引用本身的值；也就是说，不能使用相同引用为新类分配内存，并将其保留在程序块外部。 为此，请使用 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 关键字传递参数。 为简单起见，下面的示例使用 `ref`。  
  
## <a name="passing-reference-types-by-value"></a>按值传递引用类型  
 以下示例演示将引用类型参数 `arr` 按值传递给方法 `Change`。 由于该参数是对 `arr` 的引用，因此可以更改数组元素的值。 但是，只有在方法内才能将参数重新分配给其他内存位置，且不会影响原始变量 `arr`。  
  
 [!code-cs[csProgGuideParameters#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_1.cs)]  
  
 在前面的示例中，数组 `arr` 属于引用类型，传递给不含 `ref` 参数的方法。 在这种情况下，将向该方法传递一个指向 `arr` 的引用副本。 输出表明，此方法可以更改数组元素的内容，在本示例中将 `1` 更改为了 `888`。 但是，通过在 `Change` 方法内使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符来分配一份新的内存可使变量 `pArray` 引用新的数组。 因此，此后的任意更改都不会影响创建于 `Main` 内的原始数组 `arr`。 实际上，本示例创建了两个数组，一个在 `Main` 方法内，另一个在 `Change` 方法内。  
  
## <a name="passing-reference-types-by-reference"></a>按引用传递引用类型  
 除了 `ref` 关键字添加到方法标头和调用，以下示例与上述示例相同。 方法中所作的任何更改都会影响调用程序中的原始变量。  
  
 [!code-cs[csProgGuideParameters#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_2.cs)]  
  
 方法内所作的所有更改都将影响 `Main` 中的原始数组。 事实上，将使用 `new` 运算符重新分配原始数组。 因此，调用 `Change` 方法后，对 `arr` 的任何引用都将指向 `Change` 方法中创建的五元素数组。  
  
## <a name="swapping-two-strings"></a>交换两个字符串  
 按引用传递引用类型参数的一个很好的示例是交换字符串。 在示例中，`str1` 和 `str2`两个字符串在 `Main` 中初始化，然后传递给 `SwapStrings` 方法，作为由 `ref` 关键字修改的参数。 这两个字符串在该方法以及 `Main` 内交换。  
  
 [!code-cs[csProgGuideParameters#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-reference-type-parameters_3.cs)]  
  
 在此示例中，需要按引用传递参数，以影响调用程序中的变量。 如果同时从方法标头和方法调用中删除 `ref` 关键字，调用程序中不会发生任何更改。  
  
 有关字符串的详细信息，请参阅[字符串](../../../csharp/language-reference/keywords/string.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)   
 [ref](../../../csharp/language-reference/keywords/ref.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)

