---
title: "匿名方法（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- anonymous methods [C#]
- methods [C#], anonymous
- delegates [C#], anonymous methods
ms.assetid: a62441fa-f0a3-4acb-9aa6-93762a635275
caps.latest.revision: 31
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
ms.openlocfilehash: 92842becf26a15ab1a6f5e9621002abf71dc67bc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="anonymous-methods-c-programming-guide"></a>匿名方法（C# 编程指南）
在 2.0 之前的 C# 版本中，声明[委托](../../../csharp/language-reference/keywords/delegate.md)的唯一方式是使用[命名方法](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)。 C# 2.0 引入匿名方法，在 C# 3.0 及更高版本中，Lambda 表达式取代匿名方法作为编写内联代码的首选方式。 但是，本主题中有关匿名方法的信息也适用于 Lambda 表达式。 在有一种情况下，匿名方法提供 Lambda 表达式中没有的功能。 使用匿名方法可省略参数列表。 这意味着匿名方法可转换为具有多种签名的委托。 Lambda 表达式无法实现这一点。 有关 Lambda 表达式的详细信息，请参阅 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 创建匿名方法实际上是一种将代码块作为委托参数传递的方式。 这里是两个示例：  
  
 [!code-cs[csProgGuideDelegates#6](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#5](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_2.cs)]  
  
 由于使用匿名方法无需创建单独的方法，因此可减少对委托进行实例化的编码开销。  
  
 例如，在因不得不创建方法而可能出现非必要开销的情况下，指定代码块（而不是委托）很有用处。 开始新线程就是一个很好的示例。 此类创建一个线程，且还包含该线程执行的代码，而无需为委托创建其他方法。  
  
 [!code-cs[csProgGuideDelegates#7](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_3.cs)]  
  
## <a name="remarks"></a>备注  
 匿名方法的参数范围为匿名方法块。  
  
 如果目标在匿名方法块之外，匿名方法块内具有 [goto](../../../csharp/language-reference/keywords/goto.md)、[break](../../../csharp/language-reference/keywords/break.md) 或 [continue](../../../csharp/language-reference/keywords/continue.md) 等跳转语句是一种错误。 如果目标在匿名方法块之内，匿名方法块外具有 `goto`、`break` 或 `continue` 等跳转语句也是一种错误。  
  
 范围包含匿名方法声明的本地变量和参数称为此匿名方法的外部变量。 例如，在如下代码段中，`n` 是一个外部变量：  
  
 [!code-cs[csProgGuideDelegates#8](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_4.cs)]  
  
 创建委托时，对外部变量 `n` 的引用被视为已捕获。 不同于本地变量，已捕获的变量的生存期一直延伸至引用匿名方法的委托具有垃圾回收资格为止。  
  
 匿名方法无法访问外部范围的 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数。  
  
 无法在匿名方法块内访问任何不安全代码。  
  
 不允许在 [is](../../../csharp/language-reference/keywords/is.md) 运算符左侧使用匿名方法。  
  
## <a name="example"></a>示例  
 如下示例演示实例化委托的两种方式：  
  
-   将委托与匿名方法相关联。  
  
-   将委托与命名方法 (`DoWork`) 相关联。  
  
 在每一种情况下，调用委托时均显示一条消息。  
  
 [!code-cs[csProgGuideDelegates#4](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_5.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)

