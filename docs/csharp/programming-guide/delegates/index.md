---
title: "委托（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: 30
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
ms.openlocfilehash: 1d3dc2252b086f9df9e64a059a53ec8792e11b45
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="delegates-c-programming-guide"></a>委托（C# 编程指南）
[委托](../../../csharp/language-reference/keywords/delegate.md)是一种引用类型，表示对具有特定参数列表和返回类型的方法的引用。 在实例化委托时，你可以将其实例与任何具有兼容签名和返回类型的方法相关联。 你可以通过委托实例调用方法。  
  
 委托用于将方法作为参数传递给其他方法。 事件处理程序就是通过委托调用的方法。 你可以创建一个自定义方法，当发生特定事件时，某个类（如 Windows 控件）就可以调用你的方法。 下面的示例演示了一个委托声明：  
  
 [!code-cs[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 可将任何可访问类或结构中与委托类型匹配的任何方法分配给委托。 该方法可以是静态方法，也可以是实例方法。 这样便能通过编程方式来更改方法调用，还可以向现有类中插入新代码。  
  
> [!NOTE]
>  在方法重载的上下文中，方法的签名不包括返回值。 但在委托的上下文中，签名包括返回值。 换句话说，方法和委托必须具有相同的返回类型。  
  
 将方法作为参数进行引用的能力使委托成为定义回调方法的理想选择。 例如，对比较两个对象的方法的引用可以作为参数传递到排序算法中。 由于比较代码在一个单独的过程中，因此可通过更常见的方式编写排序算法。  
  
## <a name="delegates-overview"></a>委托概述  
 委托具有以下属性：  
  
-   委托类似于 C++ 函数指针，但它们是类型安全的。  
  
-   委托允许将方法作为参数进行传递。  
  
-   委托可用于定义回调方法。  
  
-   委托可以链接在一起；例如，可以对一个事件调用多个方法。  
  
-   方法不必与委托类型完全匹配。 有关详细信息，请参阅[使用委托中的变体](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)。  
  
-   C# 2.0 版引入了[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)的概念，可以将代码块作为参数（而不是单独定义的方法）进行传递。 C# 3.0 引入了 Lambda 表达式，利用它们可以更简练地编写内联代码块。 匿名方法和 Lambda 表达式（在某些上下文中）都可编译为委托类型。 这些功能现在统称为匿名函数。 有关 lambda 表达式的详细信息，请参阅[匿名函数](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用委托](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [何时使用委托，而不是接口（C# 编程指南）](http://msdn.microsoft.com/en-us/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [使用委托中的变体](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
-   [如何：合并委托（多播委托）](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [如何：声明、实例化和使用委托](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapters"></a>重要章节  
 [C# 3.0 手册，第三版：为 C# 3.0 程序员提供的 250 多个解决方案](http://go.microsoft.com/fwlink/?LinkId=195395) 中的 [委托、事件和 Lambda 表达式](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Learning C# 3.0: Master the Fundamentals of C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195418) （学习 C# 3.0：掌握 C# 3.0 的基本知识）中的 [委托和事件](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Delegate>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)

