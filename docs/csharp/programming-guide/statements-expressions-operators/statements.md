---
title: "语句（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
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
ms.openlocfilehash: 4df592821f9bebb318138cffac9045fdbec1e759
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="statements-c-programming-guide"></a>语句（C# 编程指南）
程序执行的操作采用语句表达。 常见操作包括声明变量、赋值、调用方法、循环访问集合，以及根据给定条件分支到一个或另一个代码块。 语句在程序中的执行顺序称为“控制流”或“执行流”。 根据程序对运行时所收到的输入的响应，在程序每次运行时控制流可能有所不同。  
  
 语句可以是以分号结尾的单行代码，也可以是语句块中的一系列单行语句。 语句块括在括号 {} 中，并且可以包含嵌套块。 以下代码演示了两个单行语句示例和一个多行语句块：  
  
 [!code-cs[csProgGuideStatements#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_1.cs)]  
  
## <a name="types-of-statements"></a>语句的类型  
 下表列出了 C# 中的各种语句类型及其关联的关键字，并提供指向包含详细信息的主题的链接：  
  
|类别|C# 关键字/说明|  
|--------------|---------------------------|  
|声明语句|声明语句引入新的变量或常量。 变量声明可以选择为变量赋值。 在常量声明中必须赋值。<br /><br /> [!code-cs[csProgGuideStatements#23](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_2.cs)]|  
|表达式语句|用于计算值的表达式语句必须在变量中存储该值。<br /><br /> [!code-cs[csProgGuideStatements#24](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_3.cs)]|  
|[选择语句](../../../csharp/language-reference/keywords/selection-statements.md)|选择语句用于根据一个或多个指定条件分支到不同的代码段。 有关详细信息，请参阅下列主题：<br /><br /> [if](../../../csharp/language-reference/keywords/if-else.md)、[else](../../../csharp/language-reference/keywords/if-else.md)、[switch](../../../csharp/language-reference/keywords/switch.md)、[case](../../../csharp/language-reference/keywords/switch.md)|  
|[迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)|迭代语句用于遍历集合（如数组），或重复执行同一组语句直到满足指定的条件。 有关详细信息，请参阅下列主题：<br /><br /> [do](../../../csharp/language-reference/keywords/do.md)、[for](../../../csharp/language-reference/keywords/for.md)、[foreach](../../../csharp/language-reference/keywords/foreach-in.md)、[in](../../../csharp/language-reference/keywords/foreach-in.md)、[while](../../../csharp/language-reference/keywords/while.md)|  
|[跳转语句](../../../csharp/language-reference/keywords/jump-statements.md)|跳转语句将控制转移给另一代码段。 有关详细信息，请参阅下列主题：<br /><br /> [break](../../../csharp/language-reference/keywords/break.md)、[continue](../../../csharp/language-reference/keywords/continue.md)、[default](../../../csharp/language-reference/keywords/switch.md)、[goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md)、[yield](../../../csharp/language-reference/keywords/yield.md)|  
|[异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)|异常处理语句用于从运行时发生的异常情况正常恢复。 有关详细信息，请参阅下列主题：<br /><br /> [throw](../../../csharp/language-reference/keywords/throw.md)、[try-catch](../../../csharp/language-reference/keywords/try-catch.md)、[try-finally](../../../csharp/language-reference/keywords/try-finally.md)、[try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)|  
|[Checked 和 unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)|Checked 和 unchecked 语句用于指定将结果存储在变量中、但该变量过小而不能容纳结果值时，是否允许数值运算导致溢出。 有关详细信息，请参阅 [checked](../../../csharp/language-reference/keywords/checked.md) 和 [unchecked](../../../csharp/language-reference/keywords/unchecked.md)。|  
|`await` 语句|如果用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符标记方法，则可以使用该方法中的 [await](../../../csharp/language-reference/keywords/await.md) 运算符。 在控制到达异步方法的 `await` 表达式时，控制将返回到调用方，该方法中的进程将挂起，直到等待的任务完成为止。 任务完成后，可以在方法中恢复执行。<br /><br /> 有关简单示例，请参阅[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)的“异步方法”一节。 有关详细信息，请参阅 [async 和 await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)。|  
|`yield return` 语句|迭代器对集合执行自定义迭代，如列表或数组。 迭代器使用 [yield return](../../../csharp/language-reference/keywords/yield.md) 语句返回元素，每次返回一个。 到达 `yield return` 语句时，会记住当前在代码中的位置。 下次调用迭代器时，将从该位置重新开始执行。<br /><br /> 有关详细信息，请参阅[迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)。|  
|`fixed` 语句|fixed 语句禁止垃圾回收器重定位可移动的变量。 有关详细信息，请参阅 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md)。|  
|`lock` 语句|lock 语句用于限制一次仅允许一个线程访问代码块。 有关详细信息，请参阅 [lock](../../../csharp/language-reference/keywords/lock-statement.md)。|  
|带标签的语句|可以为语句指定一个标签，然后使用 [goto](../../../csharp/language-reference/keywords/goto.md) 关键字跳转到该带标签的语句。 （参见下一行中的示例。）|  
|空语句|空语句只含一个分号。 不执行任何操作，可以在需要语句但不需要执行任何操作的地方使用。 以下示例演示了空语句的两种用法：<br /><br /> [!code-cs[csProgGuideStatements#25](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_4.cs)]|  
  
## <a name="embedded-statements"></a>嵌入式语句  
 某些语句（包括 [do](../../../csharp/language-reference/keywords/do.md)、[while](../../../csharp/language-reference/keywords/while.md)、[for](../../../csharp/language-reference/keywords/for.md) 和 [foreach](../../../csharp/language-reference/keywords/foreach-in.md)）后面始终跟有一条嵌入式语句。 此嵌入式语句可以是单个语句，也可以是语句块中括在括号 {} 内的多个语句。 甚至可以在括号 {} 内包含单行嵌入式语句，如以下示例所示：  
  
 [!code-cs[csProgGuideStatements#26](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_5.cs)]  
  
 未括在括号 {} 内的嵌入式语句不能作为声明语句或带标签的语句。 下面的示例对此进行了演示：  
  
 [!code-cs[csProgGuideStatements#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_6.cs)]  
  
 将该嵌入式语句放在语句块中以修复错误：  
  
 [!code-cs[csProgGuideStatements#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_7.cs)]  
  
## <a name="nested-statement-blocks"></a>嵌套语句块  
 语句块可以嵌套，如以下代码所示：  
  
 [!code-cs[csProgGuideStatements#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_8.cs)]  
  
## <a name="unreachable-statements"></a>无法访问的语句  
 如果编译器认为在任何情况下控制流都无法到达特定语句，将生成警告 CS0162，如下例所示：  
  
 [!code-cs[csProgGuideStatements#22](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_9.cs)]  
  
## <a name="related-sections"></a>相关章节  
  
-   [语句关键字](../../../csharp/language-reference/keywords/statement-keywords.md)  
  
-   [表达式](../../../csharp/programming-guide/statements-expressions-operators/expressions.md)  
  
-   [运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)

