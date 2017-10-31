---
title: "泛型接口（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, generic interfaces
- generics [C#], interfaces
ms.assetid: a8fa49a1-6e78-4a09-87e5-84a0b9f5ffbe
caps.latest.revision: 28
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
ms.openlocfilehash: 2a9a994c339553b923b930660c0e129dd930de96
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="generic-interfaces-c-programming-guide"></a>泛型接口（C# 编程指南）
为泛型集合类或表示集合中的项的泛型类定义接口通常很有用处。 为避免对值类型的装箱和取消装箱操作，泛型类的首选项使用泛型接口，例如 <xref:System.IComparable%601>而不是 <xref:System.IComparable>。 .NET Framework 类库定义多个泛型接口，以将其用于 <xref:System.Collections.Generic> 命名空间中的集合类。  
  
 接口被指定为类型参数上的约束时，仅可使用实现接口的类型。 如下代码示例演示一个派生自 `GenericList<T>` 类的 `SortedList<T>` 类。 有关详细信息，请参阅[泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)。 `SortedList<T>` 添加约束 `where T : IComparable<T>`。 这可使 `SortedList<T>` 中的 `BubbleSort` 方法在列表元素上使用泛型 <xref:System.IComparable%601.CompareTo%2A> 方法。 在此示例中，列表元素是一个实现 `IComparable<Person>` 的简单类 `Person`。  
  
 [!code-cs[csProgGuideGenerics#29](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_1.cs)]  
  
 可将多个接口指定为单个类型上的约束，如下所示：  
  
 [!code-cs[csProgGuideGenerics#30](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_2.cs)]  
  
 一个接口可定义多个类型参数，如下所示：  
  
 [!code-cs[csProgGuideGenerics#31](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_3.cs)]  
  
 适用于类的继承规则也适用于接口：  
  
 [!code-cs[csProgGuideGenerics#32](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_4.cs)]  
  
 泛型接口如为逆变（即，仅使用自身的类型参数作为返回值），则可继承自非泛型接口。 在 .NET Framework 类库中，<xref:System.Collections.Generic.IEnumerable%601> 继承自 <xref:System.Collections.IEnumerable>，因为 <xref:System.Collections.Generic.IEnumerable%601> 在 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 的返回值和 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 属性 Getter 中仅使用 `T`。  
  
 具体类可实现封闭式构造接口，如下所示：  
  
 [!code-cs[csProgGuideGenerics#33](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_5.cs)]  
  
 只要类形参列表提供接口所需的所有实参，泛型类即可实现泛型接口或封闭式构造接口，如下所示：  
  
 [!code-cs[csProgGuideGenerics#34](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_6.cs)]  
  
 控制方法重载的规则对泛型类、泛型结构或泛型接口内的方法一样。 有关详细信息，请参阅[泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型简介](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [接口](../../../csharp/language-reference/keywords/interface.md)   
 [泛型](~/docs/standard/generics/index.md)

