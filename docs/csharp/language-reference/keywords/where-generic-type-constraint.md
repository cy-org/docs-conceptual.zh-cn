---
title: "where（泛型类型约束）（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.assetid: d7aa871b-0714-416a-bab2-96f87ada4310
caps.latest.revision: 10
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
ms.openlocfilehash: 8e81640ee56ed672bb09242a070fdf167740874b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="where-generic-type-constraint-c-reference"></a>where（泛型类型约束）（C# 参考）
在泛型类型定义中，`where` 子句用于指定对下列类型的约束：这些类型可用作泛型声明中定义的类型形参的实参。 例如，可以声明一个泛型类 `MyGenericClass`，以使类型参数 `T` 实现 <xref:System.IComparable%601> 接口：  
  
```csharp  
public class MyGenericClass<T> where T:IComparable { }  
```  
  
> [!NOTE]
>  有关查询表达式中的 where 子句的详细信息，请参阅 [where 子句](../../../csharp/language-reference/keywords/where-clause.md)。  
  
 除了接口约束，`where` 子句还可以包括基类约束，以指出某个类型必须将指定的类作为基类（或者就是该类本身），才能用作该泛型类型的类型参数。 这样的约束一经使用，就必须出现在该类型参数的所有其他约束之前。  
  
 [!code-cs[csrefKeywordsContextual#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_1.cs)]  
  
 `where` 子句还可以包括构造函数约束。 可以使用 new 运算符创建类型参数的实例；但类型参数为此必须受构造函数约束 `new()` 的约束。 [new() 约束](../../../csharp/language-reference/keywords/new-constraint.md)可以让编译器知道：提供的任何类型参数都必须具有可访问的无参数（或默认）构造函数。 例如:   
  
 [!code-cs[csrefKeywordsContextual#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_2.cs)]  
  
 `new()` 约束出现在 `where` 子句的最后。  
  
 对于多个类型参数，每个类型参数都使用一个 `where` 子句，例如：  
  
 [!code-cs[csrefKeywordsContextual#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_3.cs)]  
  
 还可以将约束附加到泛型方法的类型参数，例如：  
  
```csharp  
public bool MyMethod<T>(T t) where T : IMyInterface { }  
```  
  
 请注意，对于委托和方法两者来说，描述类型参数约束的语法是一样的：  
  
```csharp  
delegate T MyDelegate<T>() where T : new()  
```  
  
 有关泛型委托的信息，请参阅[泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)。  
  
 有关约束的语法和用法的详细信息，请参阅[类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型简介](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [new 约束](../../../csharp/language-reference/keywords/new-constraint.md)   
 [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)

