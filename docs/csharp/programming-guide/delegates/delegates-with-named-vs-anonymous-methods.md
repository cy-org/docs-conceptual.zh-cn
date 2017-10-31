---
title: "带有命名方法的委托与带有匿名方法的委托（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- delegates [C#], with named vs. anonymous methods
- methods [C#], in delegates
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
caps.latest.revision: 18
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
ms.openlocfilehash: f82519f42e75008fc78fe475b7e37040985a21a1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="delegates-with-named-vs-anonymous-methods-c-programming-guide"></a>带有命名方法的委托与带有匿名方法的委托（C# 编程指南）
[委托](../../../csharp/language-reference/keywords/delegate.md)可以与命名方法相关联。 使用命名方法实例化委托时，该方法作为参数传递，例如：  
  
 [!code-cs[csProgGuideDelegates#1](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_1.cs)]  
  
 这称为使用命名方法。 使用命名方法构造的委托可以封装[静态](../../../csharp/language-reference/keywords/static.md)方法或实例方法。 命名方法是在早期版本的 C# 中实例化委托的唯一方式。 但是，在创建新方法是不需要的开销这一情况下，C# 允许实例化委托并立即指定调用委托时委托将处理的代码块。 代码块可包含 Lambda 表达式或匿名方法。 有关详细信息，请参阅[匿名函数](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)。  
  
## <a name="remarks"></a>备注  
 作为委托参数传递的方法必须具有与委托声明相同的签名。  
  
 委托实例可以封装静态方法或实例方法。  
  
 尽管委托可以使用 [out](../../../csharp/language-reference/keywords/out.md) 参数，但不建议将该委托与多播事件委托配合使用，因为你无法知道将调用哪个委托。  
  
## <a name="example-1"></a>示例 1  
 以下是声明和使用委托的简单示例。 请注意，委托 `Del` 与关联的方法 `MultiplyNumbers` 具有相同的签名  
  
 [!code-cs[csProgGuideDelegates#2](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_2.cs)]  
  
## <a name="example-2"></a>示例 2  
 在下面的示例中，一个委托映射到静态方法和实例方法，并返回来自两种方法的具体信息。  
  
 [!code-cs[csProgGuideDelegates#3](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_3.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [如何：合并委托（多播委托）](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)   
 [事件](../../../csharp/programming-guide/events/index.md)

