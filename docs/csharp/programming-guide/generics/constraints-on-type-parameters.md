---
title: "类型参数的约束（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], type constraints
- type constraints [C#]
- type parameters [C#], constraints
- unbound type parameter [C#]
ms.assetid: 141b003e-1ddb-4e1c-bcb2-e1c3870e6a51
caps.latest.revision: 41
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
ms.openlocfilehash: e91ae026bd89a6dd30b4c9233da4dd897928291e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="constraints-on-type-parameters-c-programming-guide"></a>类型参数的约束（C# 编程指南）
定义泛型类时，可以对客户端代码能够在实例化类时用于类型参数的几种类型施加限制。 如果客户端代码尝试使用约束所不允许的类型来实例化类，则会产生编译时错误。 这些限制称为约束。 通过使用 `where` 上下文关键字指定约束。 下表列出了六种类型的约束：  
  
|约束|描述|  
|----------------|-----------------|  
|where T：结构|类型参数必须是值类型。 可以指定除 <xref:System.Nullable> 以外的任何值类型。 有关详细信息，请参阅[使用可以为 null 的类型](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)。|  
|where T：类|类型参数必须是引用类型；这同样适用于所有类、接口、委托或数组类型。|  
|where T：new()|类型参数必须具有公共无参数构造函数。 与其他约束一起使用时，`new()` 约束必须最后指定。|  
|where T：\<基类名称>|类型参数必须是指定的基类或派生自指定的基类。|  
|where T：\<接口名称>|类型参数必须是指定的接口或实现指定的接口。 可指定多个接口约束。 约束接口也可以是泛型。|  
|where T：U|为 T 提供的类型参数必须是为 U 提供的参数或派生自为 U 提供的参数。|  
  
## <a name="why-use-constraints"></a>使用约束的原因  
 如果要检查泛型列表中的某个项，确定它是否有效，或者将它与其他某个项进行比较，则编译器必须保证它需要调用的运算符或方法将受到客户端代码可能指定的任何类型参数的支持。 通过对泛型类定义应用一个或多个约束获得这种保证。 例如，基类约束告诉编译器，仅此类型的对象或派生自此类型的对象可用作类型参数。 编译器有了此保证后，就能够允许在泛型类中调用该类型的方法。 通过使用 `where` 上下文关键字应用约束。 以下代码示例演示可通过应用基类约束添加到（[泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)中的）`GenericList<T>` 类的功能。  
  
 [!code-cs[csProgGuideGenerics#11](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_1.cs)]  
  
 约束使得泛型类能够使用 `Employee.Name` 属性，因为类型 T 的所有项都保证是 `Employee` 对象或是从 `Employee` 继承的对象。  
  
 可以对同一类型参数应用多个约束，并且约束自身可以是泛型类型，如下所示：  
  
 [!code-cs[csProgGuideGenerics#12](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_2.cs)]  
  
 通过约束类型参数，可以增加约束类型及其继承层次结构中的所有类型所支持的允许操作和方法调用的数量。 因此，在设计泛型类或方法时，如果要对泛型成员执行除简单赋值之外的任何操作或调用 `System.Object` 不支持的任何方法，则必须对该类型参数应用约束。  
  
 在应用 `where T : class` 约束时，请避免对类型参数使用 `==` 和 `!=` 运算符，因为这些运算符仅测试引用标识而不测试值相等性。 即使在用作参数的类型中重载这些运算符也是如此。 下面的代码说明了这一点；即使 <xref:System.String> 类重载 `==` 运算符，输出也为 false。  
  
 [!code-cs[csProgGuideGenerics#13](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_3.cs)]  
  
 出现这种情况是因为，编译器在编译时仅知道 T 是引用类型，因此必须使用对所有引用类型都有效的默认运算符。 如果必须测试值相等性，建议的方法是同时应用 `where T : IComparable<T>` 约束，并在将用于构造泛型类的任何类中实现该接口。  
  
## <a name="constraining-multiple-parameters"></a>约束多个参数  
 可以对多个参数应用多个约束，对一个参数应用多个约束，如下例所示：  
  
 [!code-cs[csProgGuideGenerics#64](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_4.cs)]  
  
## <a name="unbounded-type-parameters"></a>未绑定的类型参数  
 没有约束的类型参数（如公共类 `SampleClass<T>{}` 中的 T）称为未绑定的类型参数。 未绑定的类型参数具有以下规则：  
  
-   不能使用 `!=` 和 `==` 运算符，因为无法保证具体的类型参数能支持这些运算符。  
  
-   可以在它们与 `System.Object` 之间来回转换，或将它们显式转换为任何接口类型。  
  
-   可以将它们与 [null](../../../csharp/language-reference/keywords/null.md) 进行比较。 将未绑定的参数与 `null` 进行比较时，如果类型参数为值类型，则该比较将始终返回 false。  
  
## <a name="type-parameters-as-constraints"></a>类型参数作为约束  
 在具有自己类型参数的成员函数必须将该参数约束为包含类型的类型参数时，将泛型类型参数用作约束非常有用，如下例所示：  
  
 [!code-cs[csProgGuideGenerics#14](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_5.cs)]  
  
 在上述示例中，`T` 在 `Add` 方法的上下文中是一个类型约束，而在 `List` 类的上下文中是一个未绑定的类型参数。  
  
 类型参数还可在泛型类定义中用作约束。 请注意，必须在尖括号中声明此类型参数以及任何其他类型参数：  
  
 [!code-cs[csProgGuideGenerics#15](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_6.cs)]  
  
 类型参数作为泛型类的约束的作用非常有限，因为编译器除了假设类型参数派生自 `System.Object` 以外，不会做其他任何假设。 如果要在两个类型参数之间强制继承关系，可以将类型参数用作泛型类的约束。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型简介](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [泛型类](../../../csharp/programming-guide/generics/generic-classes.md)   
 [new 约束](../../../csharp/language-reference/keywords/new-constraint.md)

