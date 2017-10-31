---
title: "while（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- while_CSharpKeyword
- while
dev_langs:
- CSharp
helpviewer_keywords:
- while keyword [C#]
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
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
ms.openlocfilehash: ed531c83dba02b38576bf8354b1ff92f075048bc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="while-c-reference"></a>while（C# 参考）
`while` 语句执行一条语句或一个语句块，直到指定的表达式的计算结果为 `false` 为止。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsIteration#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_1.cs)]  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsIteration#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_2.cs)]  
  
## <a name="example"></a>示例  
 因为 `while` 表达式的测试在每次执行循环之前开始，所以 `while` 循环执行零次或多次。 这不同于 [do](../../../csharp/language-reference/keywords/do.md) 循环，该循环执行一次或多次。  
  
 [break](../../../csharp/language-reference/keywords/break.md)、[goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句将控制转移到循环外时，`while` 循环可能终止。 若要将控制传递到下一个迭代，而不退出循环，则使用 [continue](../../../csharp/language-reference/keywords/continue.md) 语句。 注意前面三个示例的输出差异，具体取决于 `int n` 递增的位置。 在以下示例中，未生成任何输出。  
  
 [!code-cs[csrefKeywordsIteration#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_3.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [while Statement (C++)](/cpp/cpp/while-statement-cpp) （while 语句 (C++)）  
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)

