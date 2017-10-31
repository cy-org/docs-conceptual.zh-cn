---
title: "do（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- do_CSharpKeyword
- do
dev_langs:
- CSharp
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
caps.latest.revision: 22
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
ms.openlocfilehash: 58a9361c440bc1b17c5ab929ff7b45ba71ce50a4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="do-c-reference"></a>do（C# 参考）
`do` 语句重复执行一个语句或语句块，直到指定的表达式计算为 `false` 值。 循环体必须括在大括号 `{}` 内，除非它由单个语句组成。 在这种情况下，大括号是可选的。  
  
## <a name="example"></a>示例  
 在下面的示例中，只要变量 `x` 小于 5，`do-while` 循环语句就开始执行。  
  
 [!code-cs[csrefKeywordsIteration#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/do_1.cs)]  
  
 与 [while](../../../csharp/language-reference/keywords/while.md) 语句不同的是，`do-while` 循环会在计算条件表达式之前执行一次。  
  
 在 `do-while` 块中的任何点，都可使用 [break](../../../csharp/language-reference/keywords/break.md) 语句跳出循环。 可通过使用 [continue](../../../csharp/language-reference/keywords/continue.md) 语句直接步入 `while` 表达式计算语句。 如果 `while` 表达式计算结果为 true，则继续执行循环中的第一个语句。 如果表达式的计算结果为 false，则继续执行 `do-while` 循环后的第一个语句。  
  
 `do-while` 循环还可以通过 [goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句退出。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [do-while 语句 (C++)](/cpp/cpp/do-while-statement-cpp)   
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)

