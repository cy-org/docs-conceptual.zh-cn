---
title: "for（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- for
- for_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
caps.latest.revision: 39
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
ms.openlocfilehash: d65c198b0fd763bddae4832290af038b8992eb48
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="for-c-reference"></a>for（C# 参考）
通过使用 `for` 循环，可以重复运行一个语句或语句块，直到指定的表达式的计算结果为 `false` 为止。 这种类型的循环可用于循环访问数组，以及事先知道循环要在其中进行循环访问的次数的其他应用程序。  
  
## <a name="example"></a>示例  
 在下面的示例中，`i` 的值被写入控制台，并在循环的每次迭代过程中递增 1。  
  
 [!code-cs[csrefKeywordsIteration#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_1.cs)]  
  
 上一示例中的 `for` 语句执行以下操作。  
  
1.  首先，建立变量 `i` 的初始值。 无论循环重复多少次，此步骤都只发生一次。 可以将此初始化视为发生在循环过程之外。  
  
2.  若要计算条件 (`i <= 5`)，请将 `i` 的值与 5 相比较。  
  
    -   如果 `i` 小于或等于 5，则条件的计算结果为 `true`，并将发生以下操作。  
  
        1.  循环主体中的 `Console.WriteLine` 语句显示 `i` 的值。  
  
        2.  `i` 的值增加 1。  
  
        3.  循环返回到步骤 2 的起始位置以再次计算条件。  
  
    -   如果 `i` 大于 5，则条件的计算结果为 `false`，并退出循环。  
  
 请注意，如果 `i` 的初始值大于 5，则循环主体一次都不会运行。  
  
 每个 `for` 语句都定义初始化表达式、条件和迭代器部分。 这些部分通常确定循环进行循环访问的次数。  
  
```csharp  
for (initializer; condition; iterator)  
    body  
```  
  
 这些部分可实现以下目的。  
  
-   初始化表达式部分设置初始条件。 输入循环前，此部分中的语句仅运行一次。 此部分仅可包含以下两个选项之一。  
  
    -   本地循环变量的声明和初始化，如第一个示例所示 (`int i = 1`)。 变量对于循环来说是本地的，且不能从循环的外部进行访问。  
  
    -   以下列表中显示用逗号分隔的零个或多个语句表达式。  
  
        -   [赋值](../../../csharp/language-reference/operators/assignment-operator.md)语句  
  
        -   方法的调用  
  
        -   为 [increment](../../../csharp/language-reference/operators/increment-operator.md) 表达式添加前缀或后缀，如 `++i` 或 `i++`  
  
        -   为 [decrement](../../../csharp/language-reference/operators/decrement-operator.md) 表达式添加前缀或后缀，如 `--i` 或 `i--`  
  
        -   通过使用 [new](../../../csharp/language-reference/keywords/new-operator.md) 创建对象  
  
        -   [await](../../../csharp/language-reference/keywords/await.md) 表达式  
  
-   条件部分包含布尔表达式，计算该表达式可确定循环应该退出还是应该再次运行。  
  
-   迭代器部分定义循环主体的每次迭代后将执行的操作。 迭代器部分包含用逗号分隔的零个或多个以下语句表达式：  
  
    -   [赋值](../../../csharp/language-reference/operators/assignment-operator.md)语句  
  
    -   方法的调用  
  
    -   为 [increment](../../../csharp/language-reference/operators/increment-operator.md) 表达式添加前缀或后缀，如 `++i` 或 `i++`  
  
    -   为 [decrement](../../../csharp/language-reference/operators/decrement-operator.md) 表达式添加前缀或后缀，如 `--i` 或 `i--`  
  
    -   通过使用 [new](../../../csharp/language-reference/keywords/new-operator.md) 创建对象  
  
    -   [await](../../../csharp/language-reference/keywords/await.md) 表达式  
  
-   循环主体由一个语句、一个空语句或一个语句块（通过将零个或多个语句用大括号括起来而创建）构成。  
  
     可以使用关键字 [break](../../../csharp/language-reference/keywords/break.md) 中断 `for` 循环，或者可以使用关键字 [continue](../../../csharp/language-reference/keywords/continue.md) 继续执行到下一次迭代。 还可以使用 [goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句退出任何循环。  
  
 本主题中的第一个示例显示了一种最典型的 `for` 循环，它为各部分做出了以下选择。  
  
-   初始化表达式声明并初始化本地循环变量 `i`，用于维护循环的迭代计数。  
  
-   条件将针对已知的最终值 5 检查循环变量的值。  
  
-   迭代器部分使用后缀递增语句 `i++`，来计算循环的每次迭代。  
  
 下面的示例阐释了几种不太常见的选择：为初始化表达式部分中的外部循环变量赋值、同时在初始化表达式部分和迭代器部分中调用 `Console.WriteLine` 方法，以及更改迭代器部分中的两个变量的值。  
  
 [!code-cs[csrefKeywordsIteration#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_2.cs)]  
  
 定义 `for` 语句的所有表达式都是可选的。 例如，以下语句创建一个无限循环。  
  
 [!code-cs[csrefKeywordsIteration#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_3.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [for 语句 (C++)](/cpp/cpp/for-statement-cpp)   
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)

