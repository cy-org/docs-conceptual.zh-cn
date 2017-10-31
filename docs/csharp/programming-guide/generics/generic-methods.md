---
title: "泛型方法（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], methods
ms.assetid: 673eeea2-4b48-4faa-9c4e-2e89449221b9
caps.latest.revision: 27
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
ms.openlocfilehash: 14461773303bafc098f79c3686b1f76827f11005
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="generic-methods-c-programming-guide"></a>泛型方法（C# 编程指南）
泛型方法是通过类型参数声明的方法，如下所示：  
  
 [!code-cs[csProgGuideGenerics#22](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_1.cs)]  
  
 如下示例演示使用类型参数的 `int` 调用方法的一种方式：  
  
 [!code-cs[csProgGuideGenerics#23](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_2.cs)]  
  
 还可省略类型参数，编译器将推断类型参数。 如下 `Swap` 调用等效于之前的调用：  
  
 [!code-cs[csProgGuideGenerics#24](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_3.cs)]  
  
 类型推理的相同规则适用于静态方法和实例方法。 编译器可基于传入的方法参数推断类型参数；而无法仅根据约束或返回值推断类型参数。 因此，类型推理不适用于不具有参数的方法。 类型推理发生在编译时，之后编译器尝试解析重载的方法签名。 编译器将类型推理逻辑应用于共用同一名称的所有泛型方法。 在重载解决方案步骤中，编译器仅包含在其上类型推理成功的泛型方法。  
  
 在泛型类中，非泛型方法可访问类级别类型参数，如下所示：  
  
 [!code-cs[csProgGuideGenerics#25](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_4.cs)]  
  
 如果定义一个具有与包含类相同的类型参数的泛型方法，则编译器会生成警告 CS0693，因为在该方法范围内，向内 `T` 提供的参数会隐藏向外 `T` 提供的参数。 如果需要使用类型参数（而不是类实例化时提供的参数）调用泛型类方法所具备的灵活性，请考虑为此方法的类型参数提供另一标识符，如下方示例中 `GenericList2<T>` 所示。  
  
 [!code-cs[csProgGuideGenerics#26](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_5.cs)]  
  
 使用约束在方法中的类型参数上实现更多专用操作。 此版 `Swap<T>` 现名为 `SwapIfGreater<T>`，仅可用于实现 <xref:System.IComparable%601> 的类型参数。  
  
 [!code-cs[csProgGuideGenerics#27](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_6.cs)]  
  
 泛型方法可重载在数个泛型参数上。 例如，以下方法可全部位于同一类中：  
  
 [!code-cs[csProgGuideGenerics#28](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_7.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 有关详细信息，请参阅 [C# 语言规范](../../../csharp/language-reference/language-specification/index.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型简介](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)

